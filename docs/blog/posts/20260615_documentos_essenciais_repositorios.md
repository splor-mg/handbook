---
date: 2026-06-15
authors: [mathpitanguy]
draft: false
comments: true
categories:
  - Estágio
---

# Definição de documentos essenciais para os repositórios da SPLOR

Repositórios organizacionais, sejam eles abertos à comunidade ou de uso interno, ganham em clareza e consistência quando seguem um conjunto mínimo de documentos padrão. Três arquivos cumprem esse papel de forma consolidada no ecossistema GitHub: `LICENSE.md`, `CONTRIBUTING.md` e `CODE_OF_CONDUCT.md`. Neste post vamos descrever para que serve cada um, onde devem ficar e como redigi-los.

<!-- more -->

### Localização dos arquivos

A localização desses arquivos determina como o GitHub consegue reconhecê-los automaticamente e exibi-los nos lugares certos da interface, como o cabeçalho do repositório, o formulário de issues e pull requests, e o perfil de comunidade do projeto.

O GitHub aceita os três arquivos na raiz do repositório, além de locais alternativos.

- `LICENSE` ou `LICENSE.md` na raiz.
- `CONTRIBUTING.md` na raiz, em `docs/` ou em `.github/`.
- `CODE_OF_CONDUCT.md` na raiz, em `docs/` ou em `.github/`.

Na nossa organização, optamos por centralizar os três arquivos em um repositório especial chamado `.github`. Os arquivos colocados ali funcionam como padrão para todos os repositórios que não tiverem sua própria versão, evitando retrabalho e garantindo consistência entre os projetos.

Esses três documentos, junto com o README, comunicam expectativas, organizam contribuições e protegem juridicamente tanto quem mantém quanto quem usa o projeto[^1].

### CONTRIBUTING.md

??? note "Para que serve o CONTRIBUTING.md"
    O arquivo `CONTRIBUTING.md` é o ponto de entrada para quem quer colaborar com o projeto. Ele concentra em um único lugar as informações que, sem ele, ficariam dispersas em conversas repetidas.[^1]

    O documento geralmente apresenta:

    - Como reportar um bug ou abrir uma issue (idealmente apontando para templates de issue e pull request).
    - Como sugerir uma nova funcionalidade.
    - Como configurar o ambiente de desenvolvimento e rodar os testes localmente.
    - O tipo de contribuição que é bem-vinda.
    - Canais de comunicação com a equipe de manutenção.

    No início do projeto, o arquivo pode ser simples. O essencial é explicar como abrir issues e quais requisitos técnicos, como testes, uma contribuição precisa atender. Com o tempo, é comum incorporar perguntas frequentes, o que evita que as mesmas dúvidas se repitam.

    Vale linkar o CONTRIBUTING a partir do README, para que mais pessoas o encontrem. Quando colocado na raiz, em `docs/` ou em `.github/`, o GitHub passa a exibi-lo automaticamente sempre que alguém abre uma issue ou pull request.

    [Acessar nosso modelo de CONTRIBUTING.md](https://github.com/splor-mg/.github/blob/main/CONTRIBUTING.md){ .md-button }

### CODE_OF_CONDUCT.md

??? note "Para que serve o CODE_OF_CONDUCT.md"
    O `CODE_OF_CONDUCT.md` define os padrões de comportamento esperados dentro da comunidade do projeto. Ele sinaliza que o ambiente é inclusivo e respeitoso com todas as contribuições, e descreve os procedimentos para lidar com problemas entre participantes, incluindo a quem reportar uma violação e quais consequências ela pode ter.[^1][^2]


    No GitHub, é possível adicionar o arquivo de duas formas:

    - Usando um template, ao criar o arquivo `CODE_OF_CONDUCT.md`, o GitHub oferece a opção "Choose a code of conduct template", com modelos prontos, como o Contributor Covenant, já formatados para preenchimento dos dados do projeto. Essa é a única forma que marca o item "Código de conduta" como completo no perfil de comunidade do repositório.

    - Manualmente, caso o modelo desejado não esteja entre os templates oferecidos, basta colar o texto escolhido diretamente no arquivo. Se o texto usado for de autoria de outra pessoa ou organização, é importante seguir as diretrizes de atribuição da fonte original.

    [Acessar nosso modelo de CODE_OF_CONDUCT.md](https://github.com/splor-mg/.github/blob/main/CODE_OF_CONDUCT.md){ .md-button }

### LICENSE.md

??? note "Para que serve o LICENSE.md"
    A licença é o documento que garante juridicamente que outras pessoas podem usar, copiar, modificar e contribuir de volta com o projeto sem represálias, e também protege quem mantém o projeto de situações jurídicas complicadas. Sem uma licença explícita, os direitos de uso ficam indefinidos.[^1]

    #### Alguns exemplos

    - **Apache 2.0**: Quem recebe o código pode modificá-lo, integrá-lo a um produto proprietário e distribuí-lo fechado, sem nenhuma obrigação de abrir o resultado. Oferece liberdade máxima para quem usa o código, mas não garante que o ecossistema permaneça aberto. Inclui proteção de patentes.[^4]

    - **GPL 3.0**: Qualquer obra derivada deve ser distribuída sob a mesma licença, o que impede que alguém pegue o código, modifique e o feche. A liberdade aqui é garantida para o código em si, não para quem o utiliza. Também inclui proteção de patentes, uma vantagem que a MIT não tem.[^3]

    - **MIT**: Permite uso, modificação e distribuição sem quase nenhuma restrição, inclusive em produtos fechados. Não exige abertura de obras derivadas e, diferente da Apache 2.0, não traz uma cláusula explícita de concessão de patentes. Ideal para bibliotecas técnicas onde o objetivo é maximizar o alcance sem qualquer fricção.[^6]

    - **AGPL 3.0**: Complementa a GPL ao fechar a chamada "brecha SaaS". Enquanto na GPL a obrigação de abrir o código é disparada pela distribuição, na AGPL ela passa a ser disparada também pelo uso em rede. Se alguém rodar uma versão modificada do código em um servidor e oferecer o serviço pela internet, também é obrigado a disponibilizar o código-fonte dessa versão. É a licença mais restritiva do conjunto e a mais indicada para APIs e sistemas web onde se quer evitar que terceiros monetizem o projeto sem contribuir de volta.[^5]

    #### Recomendação

    Depois de analisar o cenário, a GPL 3.0 se mostrou a mais adequada como padrão para os repositórios da organização, por reforçar a reciprocidade e manter o ecossistema aberto.

    Ainda assim, nem todo repositório tem a mesma natureza. Bibliotecas pensadas para ampla adoção, integrações com produtos de terceiros ou projetos acadêmicos podem se beneficiar de uma licença permissiva, como a MIT ou a Apache 2.0. Já sistemas web e APIs onde se quer evitar que terceiros monetizem o projeto sem contribuir de volta podem justificar o uso da AGPL 3.0. A escolha da licença deve ser avaliada caso a caso, considerando o propósito e o público de cada repositório.

    A escolha não precisa ser feita do zero. Ao criar um repositório no GitHub, já é possível selecionar uma licença pronta a partir de um seletor integrado, e sites como o [Choose a License](https://choosealicense.com) ajudam a comparar as opções mais populares.


[^1]: GitHub Open Source Guides, [Starting an Open Source Project](https://opensource.guide/starting-a-project/)
[^2]: GitHub Docs, [Adding a code of conduct to your project](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/adding-a-code-of-conduct-to-your-project)
[^3]: FOSSA Blog, [Open Source Software Licenses 101: GPL v3](https://fossa.com/blog/open-source-software-licenses-101-gpl-v3/)
[^4]: Apache Software Foundation, [Apache License v2.0 and GPL Compatibility](https://www.apache.org/licenses/GPL-compatibility.html)
[^5]: Revenera, [What Is the AGPL License? Requirements, Risks & Compliance](https://www.revenera.com/software-composition-analysis/glossary/what-is-the-agpl-license)
[^6]: Revenera, [What Is the MIT License? Terms, Uses & Compliance](https://www.revenera.com/software-composition-analysis/glossary/what-is-an-mit-license)