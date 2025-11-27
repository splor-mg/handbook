---
date: 2025-11-27
authors: [gabrielbdornas]
draft: false
comments: true
categories:
  - Mkdocs
---

# Nova LOA - Reunião 001

Bom, pela falta de um nome melhor, resolvi documentar estes encontros como "Nova LOA".
Iremos gerar os volumes da LOA de uma maneira diferente?
Não sabemos.

A única coisa que sabemos é que pretendemos.
E é exatamente esta discussão que você, caro colega da SPLOR, poderá acompanhar neste(s) post(s).

<!-- more -->

No encontro do dia 27/11/2025 Vivi e eu falamos de tudo um pouco.
Para aqueles que imaginaram que o assunto principal foi a LOA, propeamente dita, se enganou.
Estamos focados no início do início, que é a melhor organização de nossos dados.

## Gravação do encontro

Este post tenta fazer um grande resumo do que foi conversado, mas se preferir, pode acompanhar tudo na íntegra!

![type:video](https://www.youtube.com/embed/xz7W_47pdKE)

## Definição da Dinâmica e Foco

* Combinamos que os encontros não terão um roteiro rígido. Vamos ajustando o andamento do trabalho a medida que os problemas forem aparecendo. O objetivo inicial será mostrar Vivi como o processo de ETL está acontecendo hoje.
* Mostrando como o processo de ETL está acontecendo hoje poderemos direcionar os estudos de Python, fazendo com ele fique mais interessante.

## Análise do Processo ETL Atual

Mostrei para Vivi a análise/comparação que comecei a fazer nos nossos repositórios, com focando na padronização.
Registrei esse estudo em um [comentário deste Issue](https://github.com/splor-mg/atividades/issues/148#issuecomment-3587256329), ja aberto há algum tempo!

### Fase de Extração (E - Extract)

* **Conceito:** É o processo de buscar o dado na fonte.
* **Situação Atual:** A extração é feita a partir de **diversas fontes** (BO, SISOR, planilhas no Sharepoint, etc.), o que complica a padronização.
* **Problemas do BO:** O sistema BO só aceita envio via e-mail, e os anexos não podem ter mais de **25 MB**. Arquivos de execução, especialmente em Dezembro, frequentemente excedem esse limite, exigindo um **processo manual**[^1].

[^1]: Outro problema, menor, seria apagar os e-mails recebidos de tempos em tempo, evitando, assim, que a caixa fique cheia. Registrei uma alternativa para isso [neste comentário](https://github.com/splor-mg/dados-armazem-siafi-2025/issues/33#issuecomment-3587331719).

* **Alternativas Propostas:**
    * **Web Scraping (Robozinho Python):** Um script que acessa a página do BO e baixa a consulta desejada. Isso eliminaria a dependência do e-mail e, consequentemente, resolveria o problema do limite de tamanho do anexo. Além disso, tem o potencial de permitir a unificação dos repositórios anuais em um único script, reduzindo a manutenção (preciso tentar explicar isso melhor no futuro).
    * **Busca por API:** Investigar se o BO possui uma API, similar ao SISOR, para buscar os dados diretamente (brilhante ideia da Vivi).
    * **Migração de R para Python:** A primeira e mais simples melhoria seria reescrever os scripts de extração que estão em **R** para **Python**, padronizando a linguagem e simplificando a estrutura de arquivos.

### Fase de Transformação (T - Transform)

* **Conceito:** Processo de homogeneizar os dados de diferentes fontes, que chegam com nomes de colunas distintos. Pode incluir criação de colunas, separação de campos ou alteração de tipo de dado (ex: de texto para número).
* **Situação Atual:** Atualmente, os códigos de transformação se limitam, na grande maioria dos casos, a **renomear colunas**.

### Fase de Carregamento (L - Load)
* **Conceito:** Onde o dado, agora normalizado, é carregado para ser consumido.
* **Situação Atual:** Hoje, os dados são basicamente armazenados em repositórios do **GitHub**.
* **Opções em Análise:** Repensar o destino dos dados, avaliando:
    * **Banco de Dados Relacional (SQL)**.
    * **Neo4j** (Banco de dados de grafo).
    * **CKAN** (Portal de Dados Abertos).
* **Decisão:** Não bater o martelo sobre a tecnologia final agora, focando inicialmente na extração e transformação.

## Divisão de Tarefas e Cronograma (Projeto LOA)

* O projeto de repensar a LOA **não terá um prazo rígido**, devido à complexidade, ao prazo de entrega da LOA (setembro) e à mudança de governo em 2026. A ideia seria criar um processo que possa coexistir com o modelo antigo durante um tempo.

* **Tarefas Prioritárias:**
    1.  **Homogeneização/Padronização do ETL** dos repositórios.
    2.  **Pesquisa teórica** (como outros estados entregam os volumes da LOA).
* **Divisão de Trabalho:**
    * **Viviane/Gabriel:** Focar na análise e padronização do processo **ETL**.
    * **Tuliana:** Entrar na parte de **pesquisa teórica** sobre a LOA a partir de fevereiro, após as férias.

## 🛠️ Demonstração Prática: Estrutura do Repositório e Variáveis de Ambiente

Colocamos um pouco de mão na massa, usando como referência o repositório *[dados-armazen-siaf-25](https://github.com/splor-mg/dados-armazem-siafi-2025)*.

### Estrutura de Chamada em Cascata

Neste repositório, a extração de dados envolve a chamada de múltiplos arquivos:

1.  O arquivo **`Makefile`** define o target `extract`.
2.  O target `make extract` chama o arquivo **`main.py`**.
3.  O `main.py` chama a função `extract_resource` do arquivo **`scripts/extract.py`**.
4.  O `scripts/extract.py` (em Python) chama o script **`extract.R`** (em R).

O objetivo é simplificar essa cascata, trazendo tudo para Python, como já é feito com a função de `transform`.

### Gerenciamento de Variáveis de Ambiente (`.env`)

Foi demonstrado como o Git ignora arquivos com informações sensíveis, como o **`.env`**.

* **`.env`** Armazena **variáveis de ambiente** (ex: chaves secretas, tokens de e-mail) que o script precisa para rodar[^2].

[^2]: **VENV (Ambiente Virtual):** Ambiente isolado do Python para gerenciar dependências de pacotes. Não se confunde com `.env`.

* **`.gitignore`:** O arquivo `.env` é incluído no `.gitignore` para que suas informações secretas **não sejam rastreadas** pelo Git e, portanto, não apareçam publicamente no GitHub.
* **Uso no Python:** A biblioteca `python-dotenv` é usada para carregar as variáveis do arquivo `.env` para o ambiente do script.

Exemplo do Arquivo `.env` (Conteúdo Secreto):

```git
# .env file
GMAIL_R_KEY=qualquercoisa
```

Exemplo de Código no `main.py` (para ler a variável):

```python
from dotenv import load_dotenv
import os

load_dotenv()

gmail_key = os.getenv("GMAIL_R_KEY")

# O script tenta acessar a variável. Se não existir o arquivo .env,
# ele retorna None, resultando em um erro de autenticação.
# função print() usada somente para fins didáticos,
# # já que se a variável está no .env eu não vou querer mostrá-la
print(f"Chave do Gmail: {gmail_key}")
```

## 🔜 Próximos Passos (Dever de Casa para Vivi)

[Tentar migrar o script de extração atual (em R) para Python](https://github.com/splor-mg/dados-armazem-siafi-2025/issues/33).

Para testar o Script:

- Clonar ou dar pull/fetch no repositório [dados-armazen-siaf-2025](github.com/splor-mg/dados-armazem-siafi-2025).
- Acessar a `33_extract_python` (criada por mim durante o encontro).
- Criar o arquivo `.env` localmente.
- Solicitar ao Henrique a chave de e-mail (`GMAIL_R_KEY`) necessária para a extração.
- Testar o novo script Python com o comando `make extract` e verificar se os arquivos são salvos na pasta data_raw[^3].

[^3]: Será que isso vai mesmo [funcionar](https://github.com/splor-mg/dados-armazem-siafi-2025/blob/42123c15314103c49f78bb381c72fb1b23449b3d/.gitignore#L5)?
