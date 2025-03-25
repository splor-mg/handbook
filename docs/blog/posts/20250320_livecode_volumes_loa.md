---
date: 2025-03-20
authors: [carloshob]
draft: false
comments: true
categories:
  - Live Code
  - Volumes LOA
---

#  🚀Live Code - Volumes LOA - Encontro 2025-03-20

As discussão agora se volta para o tratamento das informações de **token** (usuário e senha) no momento da construção da imagem Docker. Precisamos dessa etapa para que os pacotes da DCAF no Bitbucket estejam disponíveis durante a construção da imagem.


<!-- more -->

[No encontro do dia 20/03](https://github.com/splor-mg/handbook/issues/69) vimos que, apesar de os segredos estarem [bem definidos na organização](https://github.com/organizations/splor-mg/settings/secrets/actions) e utilizados corretamente no wordflow do  [Actions](https://github.com/splor-mg/volumes-docker/actions/workflows/publish_image.yaml), isso não foi suficiente para que o workflow conseguisse recuperar tais informações durante a construção da imagem Docker.

Percebemos ainda a fragilidade que representa passar os dados sensíveis, como usuário e senha, tanto por argumento do [comando que inicia a construção da imagem docker](https://github.com/splor-mg/volumes-docker/blob/4f70d4e1272928fd4ec4e4f6c68dcc7886e42e73/.github/workflows/publish_image.yaml#L50-L64), quanto por meio da criação temporária de ambiente R.

As alternativa abordada nesse encontro foi a de utilização do **docker tooklit** para passar o token relacionado ao Bitbucket para o dockerfile.

🔍 Confira a gravação do encontro:

![type:video](https://www.youtube.com/embed/p0L6xfj4VpA)
