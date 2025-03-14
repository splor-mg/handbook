---
date: 2025-03-10-13
authors: [carloshob]
draft: false
comments: true
categories:
  - Live Code - Volumes LOA
---

# 🚀 Live Code - Volumes LOA - Encontro 2025-03-13

O projeto de live code envolvendo os volumes da LOA tem como objetivos a revisão e reestruturação do projeto, além da disseminação e documentação dos conhecimentos gerados.

<!-- more -->

[No encontro do dia 13/03](https://github.com/splor-mg/handbook/issues/61) seguimos na tentativa de resolver a incompatibilidade do pacote `cpp11` com a versão fixada do R (3.6.3). Inicialmente, foi testada a fixação da versão do pacote `readxl` para 1.3.1 por meio do campo `Imports`no arquivo `DESCRIPTION`.

 No entanto, o Actions continuou enfrentando os mesmos erros de incompatibilidade. Uma das principais hipóteses é que as funções do pacote `renv` (`renv::install`, `renv::update` e `renv::snapshot`), utilizadas para garantir a identicação e instalação das versões mais recentes das dependências do projeto, estão sobrepondo-se à fixação de versão definida no `DESCRIPTION`. .
 
 Isso fez retomar a dicussão a respeito dos [conceitos das funções do pacote `renv`](/20250310_live_code_volumes_loa.md) revisitados no encontro anterior. 


🔍 Confira a gravação do encontro:

![type:video](https://www.youtube.com/embed/watch?v=CQFdfFHoKgM)
