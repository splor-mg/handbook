---
date: 2025-03-17
authors: [carloshob]
draft: false
comments: true
categories:
  - Live Code - Volumes LOA
---

# 🕊️ Live Code - Volumes LOA - Encontro 2025-03-17

[O encontro do dia 17/03](https://github.com/splor-mg/handbook/issues/65) marcou a retomada da paz na AID e alinhamento para **fixação de versões**, visando evitar conflitos de dependência em relação à versão 3.6.3 do R. Decidimos suspender a utilização da função `renv::update` porquanto a versão do R estiver fixada.

<!-- more -->

Entendemos que, enquanto a versão do R estiver fixada em 3.6.3, a utilização da função `renv::update`, que atualiza todos os pacotes e dependências independentemente das definições no arquivo `DESCRIPTION`, teria grande potencial para continuar gerando conflitos de dependências, como ocorreu com o pacote [`cpp11`](https://github.com/splor-mg/handbook/issues/61), o que poderia inviabilizar o processo inicial de automatização na produção das imagens Docker.



🔍 Confira a gravação do encontro:

![type:video](https://www.youtube.com/embed/cxEkzgGnbSE)
