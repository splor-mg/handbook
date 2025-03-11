---
date: 2025-03-10
authors: [carloshob]
draft: false
comments: true
categories:
  - Live Code - Volumes LOA
---

# 🚀 Live Code - Volumes LOA - Encontro 2025-03-10

O projeto de live code envolvendo os volumes da LOA tem como objetivos a revisão e reestruturação do projeto, além da disseminação e documentação dos conhecimentos gerados.

<!-- more -->

[No encontro do dia 10/03](https://github.com/splor-mg/handbook/issues/51) revisamos alguns conceitos centrais, conforme [documentação](https://rstudio.github.io/renv/articles/renv.html), a saber: 

  - **`renv::restore()`**

    **Instala os pacotes** no ambiente do projeto a partir do `renv.lock`, garantindo que as versões sejam exatamente as registradas no lockfile. Se um pacote já estiver instalado na versão correta, ele não será reinstalado. Esse comando é útil para reproduzir o ambiente de um projeto em outro sistema ou para reverter atualizações.

  - **`renv::install()`**
  
    **Instala um ou mais pacotes** no ambiente do projeto, podendo buscar de fontes como CRAN, GitHub, Bioconductor, entre outros. Utiliza um cache global para evitar downloads repetidos e otimizar a instalação. **Não altera automaticamente o `renv.lock`**, sendo **necessário um `renv::snapshot()`** para registrar a mudança. Diferencia-se do `restore` já que **não consulta o lockfile** (`renv.lock`) diretamente, apesar de poder impactá-lo ao adicionar pacotes que não estavam registrados. Ele também instala dependências definidas no arquivo `DESCRIPTION`.

  - **`renv::update()`**

    **Atualiza os pacotes do ambiente do projeto para suas versões mais recentes** disponíveis nos repositórios configurados. Isso pode incluir pacotes de CRAN, GitHub e outras fontes. Também pode atualizar o próprio renv. Após a atualização, recomenda-se testar o código e, caso esteja funcionando, é **necessário executar `renv::snapshot()`** para registrar as novas versões no `renv.lock`.

  - **`renv::snapshot()`**

    **Atualiza o `renv.lock`** com metadados sobre os **pacotes instalados no ambiente do projeto**, garantindo que o estado atual possa ser reproduzido posteriormente com `renv::restore()`. Esse comando é essencial para controle de versões e colaboração, pois permite que outros usuários reconstruam o ambiente do projeto com as versões exatas dos pacotes.

Por fim, identificamos uma dependência no pacote `readxl`, o `cpp11`, que é incompatível com a versão fixada do R (3.6.3). A versão [1.4.0](https://readxl.tidyverse.org/news/index.html#readxl-145) do `readxl` foi a que fez a transição do `Rcpp` para o `cpp11`.


🔍 Confira a gravação do encontro:

![type:video](https://www.youtube.com/embed/watch?v=lqHMfwh_0pQ)
