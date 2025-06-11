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

Nesse sentido, a AID  e a Diretora Central de Planejamento, Programação e Normas (DCPPN) está empenhada em uma sequência de reuniões para tratar de temas como filosofia Doc as Code, Git, GitHub, Markdow, dentre outros. :rocket:

Acompanhe os encontros gravados abaixo:

## 1º encontro
🔍 Em breve estará aqui a gravação do encontro.

## 2º encontro

<iframe width="560" height="315" src="https://www.youtube.com/embed/9WYeziycXXE?si=F-3dgv0idzX508eJ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

### O que foi tratado nesse encontro

#### Como incluir um novo post no blog do Handbook
- [x] criar issue no repositório (Handbook)
- [x] abrir codespace e realizar setup do projeto
- [x] criar nova branch
- [x] Editar arquivo Authors
- [x] incluir post no blog do handbook 
- [x] Ligar o servidor e conferir alterações 
- [x] Enviar alterações para o repositótio (commit + Push) 
- [x] Abrir Pull Request e colocar @raianecardoso como revisora.

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
#### Mostrar como o Git funciona:
- [x] iniciar repositório em uma pasta com `git init`
- [x] mostrar alterações com `git status`
- [x] mostrar commits com `git add` + `git commit` 
- [x] mostrar a mágica do `git reset --hard <ID do commit>`
- [x] mostrar fluxo de trabalho: `git status` + `git pull origin <branch name>``+ `git add` + `git commit`  + `git push origin <branch name>`

#### Fazer atividade de alterar um post no handbook  + Incluir vídeo no youtube

- [x] Incluir vídeo no YouTube
- [x] Preparar texto resumo com o GPT 
- [x] Abrir o repositório usando codespaces
- [x] abrir nova branch 
- [x] alterar post 
- [x] commitar mudanças 
- [x] Enviar alterações para o repositório
- [x] Abrir PR

Fique ligado, pois logo teremos novos encontros! 