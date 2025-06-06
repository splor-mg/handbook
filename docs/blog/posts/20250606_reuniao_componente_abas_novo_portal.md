---
date: 2025-06-06
authors: [raianecardoso]
draft: false
comments: true
categories:
  - Solução Sigplan/Sisor
---

# Reunião sobre o novo Sigplan: Componente Abas

Reunião que tratou sobre as propostas de alteração no componente abas (TABs) para o novo sistema.

<!-- more -->

## Confira a gravação do encontro: 

<iframe width="560" height="315" src="https://www.youtube.com/embed/F-Guij_myJI?si=S6HglUk398q6oXGL" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## Confira o resumo do encontro:

## 🎯 Objetivo da Reunião
Apresentar o protótipo funcional de um novo componente de **abas** (*tabs*) desenvolvido para ser integrado ao sistema existente.

---

### 🧩 Demonstração do Protótipo
- O palestrante mostrou a implementação parcial do componente, ainda em fase final de ajustes de estilo (CSS).
- O novo componente se chama **`app-tabs`** e foi desenvolvido com base em **Angular**.
- Estrutura dos arquivos:
  - `.html`, `.css`, `.spec.ts`, `.test.ts` e `.ts`
- Exibição dinâmica das abas via `*ngFor`, com base em um array de objetos com `id` e `nome`:
  - `id`: usado para a lógica interna
  - `nome`: exibido visualmente ao usuário

---

### 🧪 Funcionamento
- Seleção da aba inicial com base no conteúdo do array.
- Escuta de eventos de mudança de aba utilizando bindings e flags booleanas.
- Componente antigo de título isolado (`app-card`) pode continuar sendo utilizado quando não houver abas.

---

### 🎨 Estilo e Aparência
- Ajustes de CSS ainda pendentes:
  - Tamanho e peso da fonte
  - Arredondamento dos elementos
  - Espaçamento e background
- Sugestão de copiar os estilos diretamente do protótipo para manter consistência visual.
- Posição do título (esquerda ou direita) ainda será decidida.

---

### 🤝 Colaboração
- Troca de arquivos, links e comentários entre os participantes para facilitar os ajustes visuais.
- O componente será reutilizado em outras telas, como **Indicadores** e **Ações**.
- Comentários no código foram deixados para futuras edições.

---

### ✅ Encaminhamentos
- Finalizar os ajustes de CSS com base no protótipo.
- Confirmar com Felipe a posição do título (esquerda ou direita).
- Realizar o *merge* da branch após finalização dos ajustes.
- Padronizar o estilo das fontes e aplicar os arredondamentos propostos.

---
