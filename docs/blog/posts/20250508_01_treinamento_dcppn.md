---
date: 2025-05-08
authors: [raianecardoso]
draft: false
comments: true
categories:
  - Treinamento
---

# Treinamento DCPPN

A equipe da Assessoria de Inteligência de Dados (AID) acredita que o compartilhamento de conhecimento é central para que o desenvolvimento e consolidação de melhorias se tornem uma realidade nas mais diversas equipes e organizações.


<!-- more -->

Nesse sentido, a AID  e a Diretora Central de Planejamento, Programação e Normas (DCPPN) está empenhada em uma sequência de reuniões para tratar de temas como filosofia Doc as Code, Git, GitHub, Markdown, dentre outros. :rocket:

Acompanhe os encontros gravados abaixo:

## 1º encontro

<iframe width="560" height="315" src="https://www.youtube.com/embed/W1ixJnWQaP4?si=Fn2I_m5zSTAzaqV-" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

### O que foi tratado nesse encontro

- Apresentação da Filosofia _Docs as Code_
- Apresentação das ferramentas Git e GitHub
- Criação de Conta no GitHub
- Inclusão de membros na organização Splor
- Criação de repositórios
- Edição do projeto usando o Codespace

## 2º encontro

<iframe width="560" height="315" src="https://www.youtube.com/embed/9WYeziycXXE?si=F-3dgv0idzX508eJ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

### O que foi tratado nesse encontro

#### Como incluir um novo post no blog do Handbook
- Criar issue no repositório (Handbook)
- Abrir Codespace e realizar setup do projeto
- Criar nova branch: `git checkout -b <nome da nova branch>`
- Editar arquivo Authors
- Incluir post no blog do handbook 
- Ligar o servidor e conferir alterações: `poetry run mkdocs serve`
- Enviar alterações para o repositótio: `git commit` + `git push origin <nome da branch criada>` 
- Abrir Pull Request e colocar @raianecardoso como revisora

#### Informações de Setup do Repositório
Considerando que utilizamos o `poetry ` para gerenciar as dependências do projeto, é necessário  instalar a ferramenta, via terminal, com o auxílio do `pipx`, que é um gerenciador de pacotes.

- Instalar pipx: [official pipx installation instructions](https://pipx.pypa.io/stable/installation/)
```
sudo apt update
sudo apt install pipx
pipx ensurepath
```
- Instalar Poetry: [official poetry installation instructions](https://python-poetry.org/docs/#installation)
```
pipx install poetry
```
- Após a instalação do Poetry, Instalar das dependências do projeto:
```
poetry install
```
- Ligar o servidor local
```
poetry run task serve
```

## 3º encontro
O terceiro encontro não foi gravado, pois se tratou de uma sessão de tira dúvidas. 

## 4º encontro

<iframe width="560" height="315" src="https://www.youtube.com/embed/Fu44-25Sdk8?si=bzYS97uCgZB0iK_4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

### O que foi tratado nesse encontro

#### Como o Git funciona:
- [x] Iniciar repositório em uma pasta com `git init`
- [x] Alterações com `git status`
- [x] Realizar commits com `git add [nome doc alterado]` ou `git add` + `git commit` 
- [x] mostrar a mágica do `git reset --hard <ID do commit>`
- [x] mostrar fluxo de trabalho: `git status` + `git pull origin <branch name>`+ `git add` + `git commit` + `git push origin <nome da branch>`

#### Alteração de um post no handbook com vídeo

- [x] Incluir vídeo no YouTube
- [x] Preparar texto resumo com o GPT em markdown
- [x] Abrir o repositório usando Codespaces
- [x] Abrir nova branch: `git checkout -b <nome da nova branch>` 
- [x] Alterar post
- [x] Commitar mudanças: `git add [nome doc alterado]` ou `git add` + `git commit`
- [x] Enviar alterações para o repositório: `git push origin <nome da branch criada>`
- [x] Abrir PR no GitHub

## 5º encontro
O quinto encontro não foi gravado, pois foi foram feitas as mesmas atividades do 4º encontro na intenção de fixar as etapas do processo de trabalho.
