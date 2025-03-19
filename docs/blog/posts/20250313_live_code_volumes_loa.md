---
date: 2025-03-13
authors: [carloshob]
draft: false
comments: true
categories:
  - Live Code - Volumes LOA
---

# 🚀 Live Code - Volumes LOA - Encontro 2025-03-13

[No encontro do dia 13/03](https://github.com/splor-mg/handbook/issues/61) a conversa esquentou para cima da **fixação de versões de pacotes R**, superação da dependência do **`cpp11`** e, novamente 🤯, as funções do gerenciador **`renv`**. @gabrielbdornas e @carloshob quase perderam a linha! 😂

<!-- more -->

Para o dia seguimos na tentativa de resolver a incompatibilidade do pacote `cpp11` com a versão fixada do R (3.6.3). Inicialmente, foi testada a fixação da versão do pacote `readxl` para 1.3.1 por meio do campo `Imports`no arquivo `DESCRIPTION` - haja vista essa versão do `readxl` não utilizar o pacote `cpp11.

 No entanto, o Actions continuou enfrentando os mesmos erros de incompatibilidade. Uma das principais hipóteses é que as funções do pacote `renv` (`renv::install`, `renv::update` e `renv::snapshot`), utilizadas para garantir a identicação e instalação das versões mais recentes das dependências do projeto, estão sobrepondo-se à fixação de versão definida no `DESCRIPTION`.
 
 Isso fez retomar a dicussão a respeito dos [conceitos das funções do pacote `renv`](/20250310_live_code_volumes_loa.md) revisitados no encontro anterior.


🔍 Confira a gravação do encontro:

![type:video](https://www.youtube.com/embed/CQFdfFHoKgM)
