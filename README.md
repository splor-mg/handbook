# Handbook SPLOR-MG

Esse repositório é o ponto para centralização da coleta de informações da SPLOR-MG.
Ele foi criado utilizando a ferramenta [MkDocs](https://www.mkdocs.org/) e o tema [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).
Esta documentação é gerada estaticamente e pode ser visualizada localmente ou implantada em um servidor.

## Requisitos

Certifique-se de ter instalado:

- [Python](https://www.python.org/) 3.8+
- [Poetry](https://python-poetry.org/)

## Configuração Inicial

Siga os passos abaixo para configurar o projeto localmente:

1. Clone o repositório:

   ```sh
   git clone git@github.com:splor-mg/handbook.git
   cd handbook
   ```

1. Instale as dependências do projeto com Poetry:

   ```sh
   poetry install
   ```

1. Inicie o servidor de desenvolvimento:

   ```sh
   poetry run task serve
   ```

O site estará disponível em [http://127.0.0.1:8000/](http://127.0.0.1:8000/).

## Build e Deploy

Para publicar atualizações da documentação no GitHub Pages:

```sh
poetry run task gh-deploy
```

Qualquer modificação na pasta `docs` ou nos arquivo `mkdocs.yml` é [publicada automaticamente](https://github.com/splor-mg/handbook/blob/0dc1d15d90df6f90a2255e02d7e184b168cf34cf/.github/workflows/publish_github_pages.yml#L3-L11) para a [página estática do projeto](https://splor-mg.github.io/handbook/) no GitHub Pages.

## Contribuição

Sinta-se à vontade para abrir issues e pull requests com sugestões e melhorias.

---

Qualquer dúvida, entre em contato!
