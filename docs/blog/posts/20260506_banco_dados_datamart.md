---
date: 2026-05-06
authors: [raianecardoso]
draft: true
comments: true
categories:
  - Datamart
---

#  Construção do Banco de Dados do projeto Datamart

O projeto Datamart da SPLOR tem como objetivo organizar e unificar os dados orçamentários de Minas Gerais, que hoje estão dispersos em diversos repositórios, em um único banco de dados com o histórico orçamentário desde 2002, chamado **Datamart**.

<!-- more -->

A ideia é que, além de padronizar os processos de extração e consolidação destes dados, esse projeto possa oferecer uma ferramenta de consulta self-service de acesso aos dados do banco de forma direta, confiável e sem depender de intermediários técnicos.

Neste post, iremos documentar o processo decisório e o passo a passo de construção do banco de dados de produção

## PostgreSQL

O PostgreSQL é um sistema de gerenciamento de banco de dados relacional (SGBD) de código aberto. Ele é usado para armazenar, organizar e consultar dados de forma estruturada, utilizando SQL (Structured Query Language).

Diferente de soluções mais simples, como o SQLite, o PostgreSQL é projetado para aplicações que exigem maior controle, consistência e escalabilidade, nesse sentido escolhemos usar o PostgresSQL em ambiente de desnvolvimento e de produção.

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
    - Se pedir senha, use a que você definiu.
    - Agora execute:
        - `CREATE DATABASE meu_banco`
        - `CREATE USER meu_usuario WITH PASSWORD 'minha_senha'`
        - `ALTER ROLE meu_usuario SET client_encoding TO 'utf8'`
        - `ALTER ROLE meu_usuario SET default_transaction_isolation TO 'read committed'`
        - `ALTER ROLE meu_usuario SET timezone TO 'UTC'`
        - `GRANT ALL PRIVILEGES ON DATABASE meu_banco TO meu_usuario`
    - Saia com:
        - `\q`

## Servidor
