---
date: 2026-05-06
authors: [raianecardoso]
draft: false
comments: true
categories:
  - Datamart
---

#  Banco de Dados do projeto Datamart

O [projeto Datamart](https://splor-mg.github.io/handbook/linha_do_tempo/datamart/) da SPLOR tem como objetivo organizar e unificar os dados orçamentários de Minas Gerais, que hoje estão dispersos em diversos repositórios, em um único banco de dados com o histórico orçamentário desde 2002, chamado **Datamart**.

<!-- more -->

A ideia é que, além de padronizar os processos de extração e consolidação destes dados, esse projeto possa oferecer uma ferramenta de consulta self-service de acesso aos dados do banco de forma direta, confiável e sem depender de intermediários técnicos.

Neste post, iremos documentar o processo decisório e o passo a passo de construção do banco de dados de produção.

## Construção do banco com o Django

O [Django](https://www.djangoproject.com/) é um framework escrito em Python, utilizado principalmente para o desenvolvimento de aplicações web. Uma das grandes vantagens de utilizar o Django é que ele fornece uma estrutura pronta para lidar com rotas, autenticação, formulários e, em especial, integração com banco de dados, o que torna o desenvolvimento rápido e seguro.

Para este projeto específico, uma das principais funcionalidades do Django é o seu sistema de _ORM (Object-Relational Mapping)_, que permite trabalhar com o banco de dados utilizando código Python, sem a necessidade de escrever SQL diretamente na maior parte do tempo. Além disso, o Django é responsável por criar e manter a estrutura do banco de dados utilizando um sistema chamado _migrations_.

As _migrations_ são arquivos que descrevem alterações na estrutura do banco ao longo do tempo, como:

- Criação de tabelas.
- Alteração de colunas.
- Remoção de campos.
- Criação de relacionamentos entre tabelas.

Essas alterações são definidas a partir dos [models](https://docs.djangoproject.com/en/6.0/topics/db/models/) de cada aplicação.

!!! Fluxo

    === "Definição dos models"
        As tabelas do banco são descritas em Python, dentro do arquivo `models.py`
        ``` python
        class Produto(models.Model):
          nome = models.CharField(max_length=100)
          preco = models.DecimalField(max_digits=10, decimal_places=2)
        ```

    === "Criação das migrations"
        Quando há mudanças nos models, o Django gera um arquivo de migration com o comando:
        ``` python
        python manage.py makemigrations
        ```

    === "Aplicação das migrations"
        Para efetivar as mudanças no banco, utiliza-se:
        ``` markdown
        python manage.py migrate
        ```

### A organização dos dados da Splor

A proposta é que o Datamart seja um [banco de dados relacional](https://aws.amazon.com/pt/rds/what-is-a-relational-database/?trk=faq_card), cujo os esquemas e relacionamentos entre os dados estejam predefinidos, neste caso, nos models do Django. Assim, como tarefa inicial, foi necessário definir como organizar e compatibilizar os dados da Splor, atualmente distribuídos em _datapackages_ para a estrutura  do Django.

Cada _datapackage_ corresponde à um conjunto de dados, como [dados_siafi](https://github.com/splor-mg/dados-armazem-siafi/blob/main/datapackage.yaml), [dados_aux_classificadores](https://github.com/splor-mg/dados-orcamentarios/blob/main/datapackages/dados_aux_classificadores/datapackage.yaml), [dados_reestimativa](https://github.com/splor-mg/dados-reestimativa/blob/main/datapackage.yaml), os quais, por sua vez, possuem tabelas específicas relacionadas entre si.

Para transportar esse lógica para Django, definiu-se que o [projeto Django](https://docs.djangoproject.com/pt-br/6.0/glossary/#term-project) seria o Datamart e que cada _datapackage_ seria um app do projeto Datamart. Assim, cada app possui a seu model, que, por sua vez, define e descreve as tabelas.

??? question "Projeto vs. App"

    __Qual a diferença entre um projeto e um app no Django?__ __Um app__ é uma aplicação web que executa algo, por exemplo: um sistema de blog, uma base de dados de registros públicos ou uma pequena aplicação de enquete. __Um projeto__ é uma coleção de configurações e apps para um website específico. Um projeto pode conter múltiplos apps. Um app pode estar em múltiplos projetos.

Assim, temos:

```
Projeto: datamat

App: dados_siafi
- Receita
- Despesa
- UO

App: dados_classificador
- Acao
- ElementoItem
- UO
```
??? note "Veja no projeto"

    (inserir imagem)

O Django, seguindo o fluxo de criação dos arquivos de migração e de aplicação dessa migração ao banco dade dados, cria as tabelas assim:
```
dados_siafi_receita
dados_siafi_despesa
dados_siafi_uo

dados_classificador_acao
dados_classificador_elementoitem
dados_classificador_uo
```
Ou seja:
```
<nome_da_app>_<nome_do_model>
```
Então, neste exemplo, existem duas tabelas diferentes para UO:
```
dados_siafi_uo
dados_classificador_uo
```
Mesmo tendo o mesmo nome de model (UO), elas são independentes, o que irá ajudar a manter a integridade dos dados.

Quanto ao banco de dados, é importante destacar que quando é feita a instalação do Django, por padrâo, também é feita a instalação local da instância de banco de dados SQLite. No entanto, o SQLite apresenta certas limitações e o próprio Django recomenda a utilização do PostgreSQL[^1] em projetos mais robustos em produção.

Tal mudança, para o ambiente de produção, exige a configuração de um servidor, a instalação da ferramenta PostgreSQL e, por fim, a configuração do projeto para conexão com a nova instância de banco de dados. Estas etapas serão descritas nas seções seguir.

## Servidor

Um servidor é um computador configurado para fornecer serviços, dados ou aplicações para outros computadores através de uma rede. Diferente de um computador pessoal, ele é projetado para ficar disponível continuamente, respondendo a requisições de clientes, como aplicações web ou sistemas que precisam acessar um banco de dados.

No ambiente de produção, o banco de dados ficará hospedado em um servidor para garantir disponibilidade, segurança e acesso remoto controlado. Neste projeto, esse servidor não é uma máquina física dedicada, é uma máquina virtual, que é um computador criado por software dentro da infraestrutura de um provedor de nuvem.

A máquina virtual será contratada na Microsoft Azure, que é uma plataforma de computação em nuvem contratada pelo governo. Isso permite criar e gerenciar servidores de forma flexível, sem a necessidade de adquirir hardware físico. Com a Azure, é possível definir recursos como memória, processamento e armazenamento conforme a necessidade do projeto, além de configurar rede, segurança e acesso remoto. A equipe da AID possui acesso à plataforma Azure, por meio do seu assessor chefe, que é o responsável pela criação e configuração desta máquina.

Dessa forma, o banco de dados PostgreSQL ficará instalado nessa máquina virtual, funcionando como um servidor acessível que receberá as requisições de alteração do banco de dados e consultas. Ou seja, após a criação da máquina será feita a instalação do PostgreSQL, a criação do banco de dados e a configuração de conexão com a aplicação responsável pelas migrações - tema que será tratado mais abaixo.

??? Info "Definições da máquina"

    O estudo para definição da máquina ideal para hospedagem do banco ainda será feito e pode ser acompanhado neste [issue](https://github.com/splor-mg/datamart/issues/4). Após tais definições, o processo será descrito nesse post.

### Passo a passo de acesso à máquina virtual

1. O acesso é feito via terminal.
2. É necessário ter a chave de acesso, que é um arquivo criptografado `.pem`. Uma dica é salvar esse arquivo na sua pasta `.ssh`.
3. Rodar o seguinte comando no terminal:

=== "Comando"

    ``` zsh
    ssh -i caminho/para/sua-chave.pem usuario@ip-do-servidor
    ```

=== "Exemplo"

    ``` zsh
    ssh -i ~/Downloads/minha-chave.pem metabase_ssh_key@192.168.1.45
    ```

### Pulo do gato: Configurando o `~/.ssh/config` :black_cat:

O arquivo ~/.ssh/config é um arquivo de configuração do cliente SSH. Ele permite definir parâmetros de conexão para servidores remotos, evitando a necessidade de informar todas as opções manualmente a cada acesso. Na prática, esse arquivo funciona como um atalho configurado, em vez de executar um comando longo com várias opções, você define essas opções uma única vez no arquivo e depois acessa o servidor usando apenas um nome.

#### Onde fica o arquivo

- **Linux / macOS**: ~/.ssh/config
- **Windows (Git Bash ou WSL)**: ~/.ssh/config
- **Windows (PowerShell)**: C:\Users\seu-usuario\.ssh\config

Se o arquivo não existir, ele pode ser criado manualmente.

#### Estrutura do arquivo

Cada servidor é definido por um bloco que começa com Host. Exemplo:
``` zsh
Host minha-vm
    HostName 192.168.1.45
    User metabase_ssh_key
    IdentityFile ~/.ssh/Metabase_key.pem
```
O que significa cada campo:

- **Host**: nome que você escolhe para identificar a conexão. Esse nome será usado no comando `ssh`.
- **HostName**: endereço real do servidor (IP ou domínio).
- **User**: usuário utilizado para autenticação na máquina remota.
- **IdentityFile**: caminho para o arquivo `.pem` (chave privada usada no acesso).

### Como isso simplifica o acesso

- Sem o arquivo de configuração:
``` zsh
ssh -i ~/.ssh/Metabase_key.pem metabase_ssh_key@192.168.1.45
```

- Com o config:
``` zsh
ssh minha-vm
```

### Uso de proxy (ambiente corporativo)

Em redes corporativas, o acesso externo pode exigir a utilização de um endereço de proxy autenticada[^2]. Nesse caso, adiciona-se a diretiva ProxyCommand:

``` zsh
Host minha-vm
    HostName 192.168.1.45
    User metabase_ssh_key
    IdentityFile ~/.ssh/Metabase_key.pem
    ProxyCommand connect -H <endereço_proxy_autenticada> %h %p
```

O ProxyCommand define como a conexão SSH deve ser encaminhada através do proxy. Os parâmetros `%h` e `%p` representam, respectivamente, o host e a porta de destino. Quando a proxy é configurada, ao rodar o comando no terminal para acessar a vm será solicitada a sua senha de rede, que é a mesma senha de login no computador no caso da Cidade Administrativa.

??? failure "UNPROTECTED PRIVATE KEY FILE"

    Ao tentar acessar a vm, você pode encontrar o erro **"UNPROTECTED PRIVATE KEY FILE Permissions 0644 ... are too open"**. Ele significa que a sua chave `.pem` está com permissões muito abertas, e o SSH se recusa a usá-la por segurança.

    Para resolver execute este comando no terminal **dentro da pasta onde está a chave**:
    ```zsh
    chmod 400 <sua-chave>.pem
    ```
    Isso vai deixar a chave com permissão somente leitura para você, que é o exigido pelo SSH. Depois disso, tente novamente.

Com acesso à máquina, o próximo passo é instalação e configuração do PostgresSQL, seguida da criação do banco.

## PostgreSQL

O PostgreSQL é um sistema de gerenciamento de banco de dados relacional (SGBD) de código aberto. Ele é usado para armazenar, organizar e consultar dados de forma estruturada, utilizando SQL (Structured Query Language).

Diferente de soluções mais simples, como o SQLite, o PostgreSQL é projetado para aplicações que exigem maior controle, consistência e escalabilidade, nesse sentido escolhemos usar o PostgresSQL em ambiente de desenvolvimento e de produção.

??? "Confira como instalar o PostgreSQL"

    - **Windows**
        - Acesse: [postgres.org](https://www.postgresql.org/download/windows/)
        - Baixe o instalador (via EnterpriseDB)
        - Durante a instalação:
            - Defina uma senha para o usuário postgres
            - Porta padrão: 5432
    - **Mac (Homebrew)**
    ```
      brew install postgresql
      brew services start postgresql
    ```
    - **Linux (Ubuntu/Debian)**
    ```
        sudo apt update
        sudo apt install postgresql postgresql-contrib
    ```

??? "Confira como criar um banco e um usuário"

    - Após instalar, abra o terminal:
        - `psql -U postgres`
    - Se pedir senha, use a que você definiu durante o processo de instalação.
    - Agora execute:
            ```sql
            -- Cria um novo banco de dados chamado "meu_banco"
            CREATE DATABASE meu_banco;
            -- Cria um novo usuário chamado "meu_usuario" com senha de acesso
            CREATE USER meu_usuario WITH PASSWORD 'minha_senha';
            -- Define a codificação padrão do usuário como UTF-8
            ALTER ROLE meu_usuario SET client_encoding TO 'utf8';
            -- Define o nível padrão de isolamento de transações
            ALTER ROLE meu_usuario SET default_transaction_isolation TO 'read committed';
            -- Define o fuso horário padrão das conexões do usuário como UTC
            ALTER ROLE meu_usuario SET timezone TO 'UTC';
            -- Concede ao usuário todas as permissões sobre o banco criado
            GRANT ALL PRIVILEGES ON DATABASE meu_banco TO meu_usuario;
            ```
    - Saia com:
        - `\q`

### Passo a passo de criação e configuração do PostgreSQL na máquina virtual

Este guia descreve como instalar, configurar e preparar o banco de dados no servidor, evitando problemas de acesso como perda de autenticação.

#### Passo 1: Instalar o PostgreSQL

Considerando que a VM é uma máquina Ubuntu:
```zsh
sudo apt update
sudo apt install postgresql postgresql-contrib
```

#### Passo 2: Acessar o PostgreSQL como administrador
``` zsh
sudo -u postgres psql
```

#### Passo 3: Criar banco e usuário dentro do psql
```sql
CREATE DATABASE datamart;
CREATE USER meu_usuario WITH PASSWORD 'minha_senha';
GRANT ALL PRIVILEGES ON DATABASE datamart TO meu_usuario;
```

#### Passo 4: Definir senha para o usuário postgres ainda dentro do psql
```sql
ALTER USER postgres WITH PASSWORD 'senha_forte';
```
Isso evita perda de acesso ao alterar o método de autenticação.

#### Passo 5: Saia com
```zsh
\q
```
#### Passo 6: Localize o arquivo de configuração de autenticação
```zsh
sudo -u postgres psql -c "SHOW hba_file;"
```
??? Info "Exemplo de saída"

    ```zsh
    /etc/postgresql/14/main/pg_hba.conf
    ```

#### Passo 7: Editar o arquivo `pg_hba.conf`

Configuração recomendada pois evita bloqueio de acesso.

1. Acesse o arquivo:
```zsh
sudo nano /etc/postgresql/14/main/pg_hba.conf
```

2. Substitua ou ajuste as linhas locais para o seguinte:
```
# Permite acesso administrativo sem senha via sistema
local   all             postgres                                peer

# Exige senha para outros usuários locais (Django, apps)
local   all             all                                     scram-sha-256

# Conexões via TCP (localhost)
host    all             all             127.0.0.1/32            scram-sha-256
host    all             all             ::1/128                 scram-sha-256

```
Essa configuração é importante porque mantém acesso administrativo com `sudo -u postgres psql` e evita bloqueio total ao exigir senha apenas para outros usuários. Além disso, permite conexão segura para aplicações, como Django.

#### Passo 8: Salvar e reiniciar o PostgreSQL
```zsh
sudo systemctl restart postgresql
```

#### Passo 9: Testar acesso

- Acesso administrativo:
```zsh
sudo -u postgres psql
```
- Acesso com usuário e senha:
```zsh
psql -h localhost -U meu_usuario -d datamart -W
```
#### Passo 10: (Opcional) Permitir acesso externo

Se for necessário acessar o banco fora da VM:

- Editar postgresql.conf:
```zsh
sudo nano /etc/postgresql/*/main/postgresql.conf
```
- Alterar:
```
listen_addresses = '*'
Adicionar no pg_hba.conf:
host    all    all    0.0.0.0/0    scram-sha-256
```
- Reiniciar:
```zsh
sudo systemctl restart postgresql
```
- Liberar porta na nuvem
No painel da Microsoft Azure, liberar a porta 5432 apenas para IPs confiáveis.


___
[^1]: Ver [Migrations](https://docs.djangoproject.com/en/6.0/topics/migrations/#module-django.db.migrations).
[^2]: As informações de proxy autenticada, ou não, da Cidade Administrativa estão disponíveis no [Bitwarden](https://splor-mg.github.io/handbook/gestao_splor/governanca/bitwarden_cofre_senhas/?h=bit#recursos-adicionais), que é o gestor de credenciais da Assessoria de Inteligência de Dados.
