---
date: 2026-02-13
authors: [hslinhares, guilhermemelof]
draft: false
comments: true
categories:
  - GRP
---
# Tutorial: Solicitação de Alteração Orçamentária (Remanejamento) no GRP

**Apresentado por:** Henrique de Souza Linhares e Guilherme de Melo Ferreira (SEPLAG)

Dando continuidade à série sobre o GRP, este tutorial ensina como registrar uma **Solicitação de Alteração Orçamentária**. O vídeo simula um remanejamento de crédito (anulação de uma dotação para suplementar outra) utilizando dados de uma operação real já realizada no SIAFI (sistema operacional).

Abaixo, o passo a passo detalhado:
<!-- more -->
---

## 1. Preparação: Liberação da Unidade Orçamentária (UA)

Antes de iniciar a solicitação, é necessário liberar a unidade para realizar alterações.

1.  Faça login no GRP (perfil de Órgão Central/Planejamento).
2.  Acesse o menu **Alterar Orçamento** > **Primeira Liberação de Alteração Orçamentária**.
3.  Clique em **Adicionar Novo**.
4.  **Preencha os dados:**
    * **Unidade Orçamentária:** Digite o código da UA (Ex: 20171 - FAOP).
    * **Data Fim:** Defina até o final do ano para evitar ter que refazer este passo.
5.  Clique no ícone de confirmação (Check verde).
    * *Mensagem:* "Inclusão efetuada com sucesso". Agora a UA está apta.

## 2. Registro da Solicitação

1.  Vá ao menu **Alterar Orçamento** > **Solicitação de Alteração Orçamentária** > **Registrar/Adequar Solicitação**.
2.  Clique em **Novo**.

### A. Preenchimento do Cabeçalho
*Preencha os campos obrigatórios (asterisco vermelho).*

* **Tipo de Solicitação:** Crédito Suplementar.
    * *Dica Importante:* Aguarde o carregamento do sistema ("Aguarde") após selecionar cada campo para evitar erros.
* **Instrumento de Entrada:** Sem instrumento (para Fonte 10).
* **Transposição:** Não.
* **Lei Autorizativa:** LOA (Sim).
* **Artigo:** Geralmente Artigo 9º (opcional, mas recomendado).

### B. Inclusão da Suplementação (Para onde vai o recurso)
1.  Clique em **Adicionar Novo** na seção de Suplementação.
2.  Preencha a dotação de destino:
    * **UA e Programa de Trabalho:** (Ex: Ação 2417 - Estagiários).
    * **Classificação:** Categoria, Grupo (3), Modalidade (90).
    * **Fonte:** Grupo da Fonte 11 (para Fonte 10) e Código 5010.
    * **IP:** 1.
    * **Tipo:** Remanejamento.
3.  Insira o **Valor** total a ser suplementado.
4.  Confirme no ícone de Check.

### C. Inclusão da Anulação (De onde sai o recurso)
1.  Role até a parte de Anulação e clique em **Adicionar Novo**.
2.  Preencha a dotação de origem (Ex: Ação 2500 ou DPO).
3.  Insira as classificações (GND, Modalidade, Fonte).
    * *Atenção:* Aguarde o sistema carregar o **Saldo Disponível** da ação antes de prosseguir.
4.  Insira o **Valor** a ser anulado desta dotação.
5.  Confirme.
    * *Nota:* Se houver mais de uma origem, repita o processo "Adicionar Novo" até cobrir o valor total da suplementação.

### D. Finalização
1.  No final da página, insira a **Justificativa** detalhando o motivo do remanejamento.
2.  Salve a solicitação.

## 3. Análise da Solicitação (Nível 1)

Após criar a solicitação, ela precisa ser validada tecnicamente (Nível DCMF).

1.  Acesse o menu **Alterar Orçamento** > **Solicitação de Alteração Orçamentária** > **Analisar Solicitação**.
2.  Selecione a opção **Análise Nível 1**.
3.  Localize a solicitação criada na lista.
4.  No campo **Agente Decisório**, selecione a unidade responsável (Ex: DCMF).
5.  Clique no ícone de confirmação (Check) para aprovar e finalizar.

---

### 🔗 Próximos Passos
Após a solicitação ser criada e analisada, o próximo passo lógico é a transformação dessa solicitação em um Decreto.

> **Assista também:** Confira nosso tutorial sobre **[Como criar e registrar a Minuta de Decreto](#)** para ver a etapa final deste processo.
![type:video](https://www.youtube.com/embed/NJH91Tuzn1s)
