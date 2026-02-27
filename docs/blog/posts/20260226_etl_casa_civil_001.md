---
date: 2026-02-26
authors: [gabrielbdornas]
draft: false
comments: true
categories:
  - ETL
---

# ETL - Reunião 006.1

Bom, pela falta de um nome melhor, resolvi documentar estes encontros como "ETL".
Iremos apresentar os processos de ETL da SPLOR, e também discutir suas possíveis melhorias[^1].

[^1]: Também estamos discutindo estas melhorias/simplificações [neste Issue](https://github.com/splor-mg/atividades/issues/148).

<!-- more -->

??? note "Gravação do encontro"

    Este post tenta fazer um grande resumo do que foi conversado, mas se preferir, pode acompanhar tudo na íntegra!

    ![type:video](https://www.youtube.com/embed/NSFcQLo-15Y)

No encontro do dia 26/02/2026 a conversa foi com a equipe da Casa Civil (SCC), mais especificamente com nosso colega Gabriel Aguiar.
A ideia era apresentar as ferramentas que estamos desenvolvendo (AID) para nosso novo processo de ETL.

## Extract - Contexto explor

??? note "Gerenciamento de dependências (Poetry)"

    ```
    # Iniciar um novo projeto com estrutura de pastas pronta
    poetry new nome-do-projeto

    # Iniciar o Poetry em uma pasta já existente
    poetry init

    # Instalar dependências (ex: bibliotecas para variáveis de ambiente e testes)
    poetry add python-dotenv taskipy pytest

    # Ativar o ambiente virtual criado pelo Poetry
    # Necessário instalar o plugin https://github.com/python-poetry/poetry-plugin-shell
    poetry shell
    ```

- Explicamos um pouco sobre como construímos nossos [datapackages](https://datapackage.org/overview/introduction/), dando como exemplo o repositório [dados-armazem-siafi-2026](https://github.com/splor-mg/dados-armazem-siafi-2026).
  - Em geral, repositórios iniciados com [dados](https://github.com/orgs/splor-mg/repositories?q=dados) em nossa organização são datapackages.
  - `resources` [com mais de um arquivo](https://datapackage.org/standard/data-resource/#multiple-files) são utilizados em casos de arquivos muito grande. [Aqui um exemplo nosso](https://github.com/splor-mg/dados-armazem-siafi-2026/blob/ebce4711696e6807ffef1f013aaead830df1bee3/datapackage.yaml#L7-L10).
  - A propriedade customizada `target` nos nossos schemas serve para o processo de transformação, onde, basicamente, transformamos o nome dos campos.
- Mostramos o pacote [frictionless-py](https://framework.frictionlessdata.io/blog/2022/08-22-frictionless-framework-v5.html) para validações do conjunto.
- Mostramos a utilização do pacote [dpetl](https://pypi.org/project/dpetl/) que está sendo construído para padronizar o processo de ETL com base na utilização de [datapackages](https://datapackage.org/overview/introduction/) (atualmente apenas o comando `dpetl extract` está funcionando).

## Outras Referências

- [Rubular - regex](https://rubular.com/).
- [Template django](https://demos.themeselection.com/sneat-html-django-admin-template-free/).
- [Metabase](https://www.metabase.com/).

## 🏁 Conclusão e Próximos Passos

Esta reunião foi fundamental para trocar experiências e tentar criar um processo de ETL em comum entre AID e SCC.
