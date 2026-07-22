---
date: 2026-07-22
authors: [mariaefod]
draft: false
comments: true
categories:
  - Treinamento
---

# Guia de acesso ao servidor

Neste guia, apresentamos o passo a passo para solicitar acesso ao servidor da Prodemge e realizar a primeira conexão.

<!-- more -->


## 1. Solicitar fixação do IP

Para fixar o IP, é necessário enviar e-mail para o endereço `central.seplag@positivo.com.br`, solicitando a fixação do IP.

!!! note "Modelo de e-mail"

    Prezados, boa tarde,

    Solicito fixação de IP, para acesso da máquina ao servidor 200.198.9.184.

    Estação:

    Patrimônio:

    Hostname:

    IP:

    MAC:

    Atenciosamente,

Para consultar as informações da máquina Windows, siga o passo a passo:

  1. Pressione `Windows` + `R`

  2. Digite `cmd` e pressione `enter`

  3. No Prompt de Comando, execute `ipconfig /all`

Preencha as informações solicitadas no e-mail utilizando os dados da sua máquina:

  - **Estação**: número de identificação da estação de trabalho (G 01 0001)

  - **Patrimônio**: número do patrimônio da máquina (10000000-0)

  - **Hostname**: valor exibido como "Nome do host", na seção "Configuração de IP do Windows" (A00A0000A000000)

  - **IP**: valor exibido como "Endereço IPv4", na seção "Adaptador Ethernet Ethernet" (10.000.000.00(Preferencial))

  - **MAC**: valor exibido como "Endereço Físico", na seção "Adaptador Ethernet Ethernet" (00-A0-00-0A-00-00)


## 2. Solicitar acesso ao servidor

Após a conclusão do chamado de fixação do IP, a chefia deverá solicitar à Prodemge a liberação de acesso da máquina ao servidor 200.198.9.184.

!!! note "Modelo de e-mail"

    Prezados, boa tarde,

    Solicito criar pedido na Prodemge para liberação de acesso da máquina ao servidor. Informo que o IP já foi fixado.

    IP de destino: 200.198.9.184

    Porta/Serviço: RDP – 3389

    Estação:

    Patrimônio:

    Hostname:

    IP:

    MAC:

    Atenciosamente,


## 3. Verificar se o servidor está em uso

Antes de acessar o servidor, verifique no grupo do Teams da equipe se há algum usuário conectado.

Isso porque, o servidor permite apenas uma sessão por vez. Portanto, ao realizar uma nova conexão, o usuário atualmente conectado será desconectado automaticamente.

Portanto, sempre avise no grupo quando for acessar o servidor.

Caso ainda não esteja no grupo, peça a um dos membros da equipe para ser incluído, antes de acessar o servidor.
.

## 4. Conectar-se ao servidor

Após liberação do acesso, tente acessar seguindo o passo a passo:

  1. Procure, no Windows, pelo aplicativo "Conexão de Área de Trabalho Remota"

  2. Clique em "Mostrar Opções"

  3. No campo "Computador:" informe o IP `200.198.9.184`

  4. No campo "Nome de usuário:" informe o usuário

  5. Clique em "Conectar"

  6. Na nova tela que abrir, informe a senha e clique em "OK"

**Observação**: Você pode solicitar as credenciais de acesso a algum membro da equipe ou consultar no Bitwarden da assessoria.
