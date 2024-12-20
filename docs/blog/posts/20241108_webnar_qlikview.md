---
date: 2024-11-01
authors: [hslinhares]
draft: false
comments: true
categories:
  - Webnar Inteligência.MG
---

# Webnar Inteligência.MG #2 - Qlikview

A ferramenta de BI `Qlikview` tem sido utilizada há vários anos na SPLOR em painéis de dados de grande importância para a execução das atividades, como o painel da `Reestimativa` e o `Relatório Operacional`, que trazem tempestividade e confiabilidade no acesso a informação.
Com este webnar a Assessoria de Inteligência de Inteligência de Dados tem o objetivo principal de incentivar e auxiliar a construção de painéis de forma descentralizada por toda equipe SPLOR. Para isso é feito um `overview` dos principais pontos de uso ferramenta, começando do zero, desde a instalação até a construção final de um painel.

<!-- more -->

Pontos discorridos no webnar:

- como instalar e autenticar o qlikview;
- carregamento de dados de tabela e web;
- transformação de dados no script do qlikview;
- modelagem linktable;
- versionamento do script;
- layout: criação e edição de painéis;
- variáveis, setanalysis, disparadores.


[Baixar material utilizado no Webnar](https://github.com/splor-mg/reprex/tree/main/reprex/20241107T105702)


Bibliografia sugerida:

Barry Harmsen, Miguel Garcia-QlikView 11 for Developers-Packt Publishing (2012);

Stephen Redmond-QlikView for Developers Cookbook-Packt Publishing (2013);

[Manual Set Analysis](https://community.qlik.com/t5/Brasil/Manual-Set-Analysis-Completo-em-Portugu%C3%AAs-BR/td-p/1488633)

[Nota sobre modelagem linktable](https://splor-mg.github.io/notas/main/20231804T160439/)

Citações interessantes:

```
"So how do we incorporate two or more fact tables into one data model and treat them as two separate logical tables while, at the same time, avoiding the synthetic key issue? At first sight, it can seem like both options are mutually exclusive, but there is a workaround which is to create a Link Table. As its name implies, a link table essentially 'links' two or more fact tables by taking all common fields out of the original tables and placing them into a new one (the link table). The new link table contains all possible combination of values for that set of fields and, through a unique key, is associated to the original tables."

— Barry Harmsen, Miguel Garcia, QlikView 11 for Developers, Packt Publishing (2012).
```

```
"Sometimes we are faced with a situation where things are not quite easy. There may be multiple fact tables with multiple associations to other tables that cause the 'dreaded' synthetic key."

— Stephen Redmond, QlikView for Developers Cookbook, Packt Publishing (2013
```

```
"Probably, the most common situation that requires more complex data modeling is where we have more than one fact table—a table containing a number that we might use in a calculation—all of which have several common key fields linking to other dimension tables. There are several ways to deal with this situation; by far the easiest way is to simply concatenate the fact tables together to form one large fact table."

— Stephen Redmond, QlikView for Developers Cookbook, Packt Publishing (2013)
```




Assista a gravação do encontro:

![type:video](https://www.youtube.com/embed/jYE_N9s7D60)
