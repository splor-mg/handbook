---
date: 2024-11-26
authors: [gabrielbdornas]
draft: false
comments: true
categories:
  - Volumes LOA
---

# Publicação volumes LOA - Parte 1

A equipe da Assessoria de Inteligêcia de Dados acredita que o compartilhamento de conhecimento é central para que o desenvolvimento e consolidação de melhorias se tornem uma realidade nas mais diversas equipes e organizações.

Nesse contexto, o trabalho de publicação dos volumes da LOA no ano de 2024.
Este post mostra a primeira parte deste trabalho.

<!-- more -->

## Primeiro vídeo

1. [Link vídeo](https://cecad365-my.sharepoint.com/personal/m752587_ca_mg_gov_br/_layouts/15/stream.aspx?id=%2Fpersonal%2Fm752587%5Fca%5Fmg%5Fgov%5Fbr%2FDocuments%2FGrava%C3%A7%C3%B5es%2FGera%C3%A7%C3%A3o%20volumes%20LOA%202025%20%28c%5F%20virada%20de%20ano%29%2D20240916%5F140432%2DGrava%C3%A7%C3%A3o%20de%20Reuni%C3%A3o%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ee83d2fc2%2D0f05%2D450f%2Dae44%2D186687de958f)[^1].

1. Gravação pequena.
1. Mostra criação da conta [DockerHub](https://hub.docker.com/) da SPLOR[^2].
1. Repositório [volumes-docker](https://github.com/splor-mg/volumes-docker) responsável pela criação da imagem docker utilizada na geração dos volumes da [LOA](https://github.com/splor-mg/volumes-loa) e do [PPAG](https://github.com/splor-mg/volumes-PPAG).

    - Resgata versões e dependências necessárias para rodar o projeto.
    - Sem estas versões projeto não funciona, o que significa que o código fonte não pode sofrer atualização de versões das ferramentas utilizadas.

## Segundo vídeo

1. [Link vídeo](https://cecad365-my.sharepoint.com/personal/m752587_ca_mg_gov_br/_layouts/15/stream.aspx?id=%2Fpersonal%2Fm752587%5Fca%5Fmg%5Fgov%5Fbr%2FDocuments%2FGrava%C3%A7%C3%B5es%2FGera%C3%A7%C3%A3o%20volumes%20LOA%202025%20%28c%5F%20virada%20de%20ano%29%2D20240916%5F141937%2DGrava%C3%A7%C3%A3o%20de%20Reuni%C3%A3o%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E75267edf%2Dd667%2D4a42%2D833d%2D80f17ad6257a)[^1].
1. No repositório [volumes-docker](https://github.com/splor-mg/volumes-docker) local rodar comando responsável por buildar a imagem docker a ser utilizada.
    - Comando descrito no [`READMDE.md`](https://github.com/splor-mg/volumes-docker/blob/main/README.md`) do projeto.
    - Comando `make image=ploa2025 relatorios=v0.7.64 execucao=v0.5.22 reest=v0.2.6`
    - Necessário arquivo `.env` com secrets.
    - No vídeo, Francisco atualiza a versão do pacote relatórios.
    - A imagem gerada deve ser encaminhada para o DockerHub (esta ação não foi automatizada).
    - [Erro apresentado durante processo](https://github.com/splor-mg/volumes-docker/issues/30) não reconhecendo a flag `--secret` no Windows.
    - `/home/rstudio` é o diretório dentro do container criado a partir da imagem docker onde o processo de geração dos volumes ocorrerá.
1. Arquivo [data.toml](https://github.com/splor-mg/volumes-loa/blob/main/data.toml) do repositório volumes-loa é a lista de dependências de datapackages.
1. Repositório local [volumes-loa](https://github.com/splor-mg/volumes-loa) será usado para ligar container via comando `make docker`. Ou seja, ele usa os arquivos/scripts deste repositório dentro do container.
1. Conferir se a versão da imagem utilizada para gerar o container é a mais atualizada no dockerhub.
1. Orientações [`README.md`](https://github.com/splor-mg/volumes-loa/blob/main/README.md) do repositório volumes-loa é, atualmente, a melhor referência dos passos a serem seguidos. Foi criado [este issue](https://github.com/splor-mg/volumes-loa/issues/131) como referência para os próximos anos. Possível fonte para um Issue template.
1. Atualização dados repositório [dados-volumes-loa](https://github.com/splor-mg/dados-volumes-loa).
    - `make extract` para extrair arquivos pasta Sharepoint para repositório.
    - Não entendi como o script (python ou R) baixa arquivos no Sharepoint.
    - Alguns arquivos não foram encontrados e para não ficar travado neste erro os arquivos de 2023 foram utilizados. Para isso foi aberto [este issue](https://github.com/splor-mg/dados-volumes-loa/issues/3).
    - Caminho para arquivos no Sharepoint aceitou espaços.
    - `make validate` valida os arquivos baixados. No vídeo alguns arquivos apresentaram nomes de colunas diferentes. [Este issue foi aberto](https://github.com/splor-mg/dados-volumes-loa/issues/4).
1. Daniel sugere iniciar a geração dos volumes do último para o primeiro. Orientação registrada no [`README.md`](https://github.com/splor-mg/volumes-loa/blob/da3a1d9dc153718ffb75aa3ecb3c46122e3d011b/README.md?plain=1#L75-L86). Francisco mostra a geração de volume por volume (apaga o volume e gera novamente, exemplo `make rm vol=6` e `make v6`).
1. [volumes-loa](https://github.com/splor-mg/volumes-loa) tem um target `make check` para testes (checa diferenças entre volumes gerados e novas gerações). Check não funcionará na geração do próximo ano (somente quando primeiro volume do próximo ano for finalizado).

## Achados diversos

- [New codeblock shortcut](https://github.blog/changelog/2021-04-09-new-codeblock-shortcut/) no Github: ++ctrl+e++.
- Frase Francisco: Não precisamos ter medo de modificar o projeto [volumes-loa](https://github.com/splor-mg/volumes-loa), mas não vamos atualizá-lo ativamente.
- Utilizar `1. ` para todos os itens de uma lista markdown ordenada, simplificando a manutenção.
- Andrey comenta que arquivos `.Rnw` são arquivos `R` misturados com `latex`.

[^1]: Por conter informações sensíveis este vídeo não está aberto a todos. Caso precise, entre em contato com os responsáveis da equipe solicitando acesso
[^2]: Informações de acesso disponível no repo privado [acessos-aid](https://github.com/splor-mg/acessos-aid/blob/50ce50e6d194d77270a9c053cc090a823e25969d/acessos.csv?plain=1#L2).
