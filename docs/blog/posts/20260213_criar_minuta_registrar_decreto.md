---
date: 2026-02-13
authors: [hslinhares, guilhermemelof]
draft: false
comments: true
categories:
  - GRP
---
# 🖥 Tutorial: Criação e Registro de Decreto no GRP

**Apresentado por:** Henrique de Souza Linhares e Guilherme de Melo Ferreira (SEPLAG)

Este tutorial demonstra o fluxo completo para a elaboração de um decreto orçamentário (GRP), desde o login no sistema até o registro final após a publicação. Abaixo, resumimos os passos essenciais apresentados no vídeo.

---

## 1. Acesso e Navegação Inicial

* Faça o login no sistema.
* Acesse a **Central de Planejamento** (clicando no ícone da lupa).
* No menu, vá para a aba **Programação Orçamentária** > **Alterar Orçamento**.
* Selecione a opção **Minuta de Decreto**.

## 2. Criação da Minuta (Manter Minuta)

1.  Clique em **Manter Minuta de Decreto** e, em seguida, no botão **Novo**.
2.  **Selecione o tipo de decreto** (Suplementar, Especial ou Extraordinário).
    * *Nota: A maioria dos casos será "Suplementar".*
3.  **Selecione as solicitações:** Marque quais solicitações devem entrar no decreto. É possível selecionar todas de uma vez ou escolher manualmente uma a uma.
4.  Clique em **Gerar Minuta**.
5.  Revise os dados (o modelo é gerado automaticamente) e insira um comentário, se necessário.
6.  Clique em **Enviar Minuta para Análise**.

## 3. Análise da Minuta

1.  Volte para o menu **Alterar Orçamento** > **Minuta de Decreto**.
2.  Clique em **Analisar Minuta**.
3.  Pesquise pela minuta gerada e clique no ícone **Analisar** (botão à direita).
4.  Na tela de decisão, selecione **Encaminhar para publicação**.
5.  Insira um comentário final e clique em **Concluir**.

## 4. Registro do Decreto (Pós-Publicação)

> **Atenção:** Esta etapa simula o retorno do Diário Oficial. Em produção, isso geralmente é feito no dia seguinte.

1.  Retorne ao menu **Minuta de Decreto** > **Manter Minuta**.
2.  Pesquise pela minuta (ela aparecerá listada).
3.  Clique no ícone de **"+" (Mais)** para registrar a minuta.
4.  **Identificação do Decreto:** Insira o número de identificação conforme saiu no Diário Oficial.
    * *Dica:* Em ambiente de testes ou na falta do número, costuma-se usar a data atual (ex: 12/02/2026).
5.  Clique em **Registrar**.

---

### ⚠️ Observações Importantes

* **Origem de Crédito (SIAFI):** Foi esclarecido que, neste novo processo, **não há mais a necessidade** de informar a origem de crédito.
* **Ambiente de Produção vs. Teste:** Na prática (produção), a etapa de **Registro** só deve ser feita após a confirmação da publicação no Diário Oficial. Se não houver publicação, deve-se aguardar.🔍 Confira a gravação do encontro:

![type:video](https://www.youtube.com/embed/WzmzJpMUIOc)
