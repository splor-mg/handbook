---
date: 2025-07-16
authors: [gabrielbdornas]
draft: false
comments: true
categories:
  - Mkdocs
---

# Guia de estilo de nossas páginas

Imagine poder acompanhar cada mudança em seus documentos como se fosse uma linha do tempo, sabendo exatamente quem alterou, o quê e quando alterou. 
Melhor ainda!
Imagine sugerir melhorias de forma simples e colaborativa, como fazemos em redes sociais. 
É exatamente isso que conseguimos usando uma filosofia conhecida como [Docs as Code](https://www.writethedocs.org/guide/docs-as-code/).

Neste post definiremos algumas regras simples, mas muito efetivas, para manter o padrão entre as páginas deste ou qualquer outro conteúdo criado a partir desta filosofia.

<!-- more -->

E, porque seguir estas recomendações?
Simples...

Você já se frustrou tentando encontrar aquela documentação importante que alguém atualizou, mas ninguém sabe quando ou onde? 
Ou já teve dificuldade para entender quem fez determinada alteração em um documento e por quê? 
Nós também! 
Por isso, seguimos as convenções propostas aqui.

## Mkdocs e Material

Para tornar tudo que foi dito até aqui realidade, a principal ferramenta utilizada é o [MkDocs](https://www.mkdocs.org/), com seu tema [Material](https://squidfunk.github.io/mkdocs-material/)[^1].
Em conjunto, eles transformam textos simples escritos em [Markdown](https://www.markdownguide.org/basic-syntax/) em páginas web bonitas e organizadas. 

O melhor de tudo? 
Não precisa ser um especialista em tecnologia para contribuir.
Se você sabe escrever um e-mail, já tem o básico necessário para começar a utilizar!

## Estilo dos arquivos `.md`

- Cabeçalhos:
    - Somente primeira letra maiúscula[^2].
    - Título da página definido com [heading level 1](https://www.markdownguide.org/basic-syntax/#:~:text=%23-,Heading%20level%201,-%3Ch1%3EHeading%20level) (`#`).
    - Demais cabeçalhos da página definidos com [heading level 2](https://www.markdownguide.org/basic-syntax/#:~:text=%23%23-,Heading%20level%202,-%3Ch2%3EHeading%20level) (`##`).
    - Não utilizar [heading level 3](https://www.markdownguide.org/basic-syntax/#:~:text=%23%23-,Heading%20level%202,-%3Ch2%3EHeading%20level) (`###`) em diante. 
    Para estes casos utilize listas.

- Parágrafos:
    - Somente primeira letra maiúscula[^2].
    - A separação entre parágrafos deverá ser feita com a utilização de uma linha em branco entre um bloco de frases.

- Frases:
    - Para simplificar o processo de revisão dos arquivos `.md`, incluir cada frase em uma linha.
    - Utilizar vírgula (`,`) para agrupar ideias, evitando, ao máximo hífens (`-`) e parênteses (`(` e `)`).
    - Sempre finalizar a linha com pontuação, seja ela qual for.

- Listas:
    - Somente primeira letra maiúscula[^2].
    - Sempre finalizados com pontos (`.`) e não com ponto e vírgula (`;`) ou sem ponto (`.`).

- Nomenclatura de arquivos e pastas:
    - Arquivos e pastas deverão ser nomeados, como regra geral, no padrão [snake_small_case](https://en.wikipedia.org/wiki/Snake_case).
    - Quando houver um padrão específico já estabelecido no repositório, este deverá prevalecer, em consonância com o princípio de consistência interna mencionado na [PEP-0008](https://peps.python.org/pep-0008/#naming-conventions).
    > _New modules and packages (including third party frameworks) should be written to these standards, but where an existing library has a different style, **internal consistency is preferred** (Naming Conventions - PEP-0008)._
    - Para arquivos que carregam múltiplas informações distintas no nome, como prefixo, sufixo, tipo de documento, autoria, ano, etc., pode-se combinar `snake_case` e `kebab-case` para melhorar a legibilidade.
    Sugestão de utilizar `snake_case` (`_`) para separar diferentes "campos" do nome e hífens (`-`) para separar palavras dentro de um mesmo campo.
    Exemplos:
     - `adr-001_definicao-estrutura-tabelas.md` -> padrão: `[adr]-[número]_[nome-resumido]`.
     - `dispensa-licitacao_parecer-juridico_age_2022.pdf` -> padrão `[tema]_[tipo-documento]_[autoria]_[data-elaboração]`.
    - Arquivos e pastas em projetos `mkdocs` deverão ser criados, preferencialmente, dentro da pasta `docs`.
    - Arquivos do post deverão iniciar com data no padrão `yyyymmaa`[^3] (Exemplo: `20250716_nome_post_reduzido.md`).

## Conclusão

Seguir este guia de estilo é fundamental para manter a consistência e qualidade da nossa documentação.
Com estas regras simples, conseguimos criar conteúdo mais organizado, profissional e fácil de manter.
Lembre-se que documentação é uma forma de comunicação, e quanto mais clara e padronizada ela for, melhor será para todos os envolvidos.
A adoção destas práticas nos ajuda a construir uma base sólida para o crescimento e evolução contínua dos nossos projetos.

[^1]: Use e abuse da documentação do tema [Material](https://squidfunk.github.io/mkdocs-material/) para criar páginas cada vez mais atrativas.
[^2]: Com exceção de nomes próprios e ou siglas.
[^3]: Ano com quatro dígitos, mês e dia com do dois. Exemplo `20231025`.
