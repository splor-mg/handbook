---
date: 2025-02-27
authors: [gabrielbdornas]
draft: false
comments: true
categories:
  - Markdown
---

# Seções Recolhíveis em Markdown

[👉 Publicado por Emmanuel Gautier em 17 de setembro de 2023](https://www.emmanuelgautier.com/blog/markdown-collapsible-section), com pequenas adaptações nossas.

Como desenvolvedores, sabemos que uma estrutura bem organizada em Markdown, como em um `README.md`, pode fazer uma grande diferença na interação de usuários e outros desenvolvedores com nossos projetos.
Uma maneira interessante de aprimorar seu Markdown é adicionando seções recolhíveis.

<!-- more -->

Essas seções ajudam a manter seu documento organizado e de fácil navegação.
Neste guia rápido, mostraremos como criar seções recolhíveis em seu Markdown no **GitHub** (1).
{ .annotate }

1. :man_raising_hand_tone5: Você também pode usar Markdown recolhível fora do GitHub em outros softwares compatíveis (GitLab, VS Code, Jupyter Notebooks, etc.).
O tema mkdocs Material tem algo parecido chamado [admonitions](https://squidfunk.github.io/mkdocs-material/reference/admonitions/?h=admo), vale a pena conferir.

## O que são seções recolhíveis em Markdown?

Seções recolhíveis(1) permitem ocultar e revelar conteúdo conforme necessário.
{ .annotate }

1. :man_raising_hand_tone5: Do Inglês **Collapsible**.

Isso é especialmente útil, por exemplo, quando seu `README.md` ou comentário em algum Issue GitHub se torna extenso e você deseja mantê-lo limpo e facilmente navegável.

## Criando uma seção recolhível

Você pode criar seções recolhíveis em Markdown usando as tags HTML `<details>` e `<summary>`. Veja o exemplo abaixo:

```html
<details>
  <summary>Clique para expandir</summary>

  Este é o conteúdo da seção recolhível. Você pode incluir qualquer texto formatado em Markdown, listas ou código aqui.

</details>
```

**Explicação:**

- `<details>`: Esta é a tag HTML que define a seção recolhível. Ela atua como um contêiner para o conteúdo que você deseja ocultar ou revelar.
- `<summary>`: Dentro da tag `<details>`, você usa a tag `<summary>` para especificar o texto que os usuários verão antes de expandir a seção.
Isso serve como um rótulo clicável para abrir ou fechar a seção.
- `"Clique para expandir"`: Este é o texto que aparece como o resumo.
Você pode personalizá-lo para fornecer uma indicação clara do que está oculto na seção.
Por exemplo, você pode usar emojis, como `"🔍 Clique para ver detalhes."`
- **Conteúdo**: Entre as tags `<details>` e `</details>`, você coloca o conteúdo que deseja ocultar ou revelar.
Isso pode incluir qualquer texto formatado em Markdown, listas, blocos de código ou até mesmo outras seções recolhíveis.
