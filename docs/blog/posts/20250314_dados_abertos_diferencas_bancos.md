---
date: 2025-03-14
authors: [carloshob]
draft: false
comments: true
categories:
  - Dados Abertos MG
---

# 📂 Análise dos diferentes bancos de dados publicados da receita pública

No Estado de Minas Gerais, os dados de receita são disponibilizados por meio de diferentes plataformas, cada uma com particularidades em relação ao nível de detalhamento e à estrutura de apresentação. Os principais repositórios são o [Portal de Dados Abertos MG](https://dados.mg.gov.br/) e o [Portal da Transparência](https://www.transparencia.mg.gov.br/).


<!-- more -->


## 🔍 Principais Diferenças Identificadas

| Característica               | `datapackages-AID` | Portal da Transparência | DadosMG - Receita Pública |
|---------------------------------|--------------------|--------------------------|---------|
| **Detalhamento por Mês**      | ✅ Sim            | ❌ Não                 | ❌ Não  |
| **Detalhamento por UO**        | ✅ Sim            | ❌ Não                 | ❌ Não  |
| **Classificação Completa**   | ✅ Sim            | ❌ Parcial              | ❌ Parcial |
| **Estrutura da Receita**       | Código detalhado | Categoria/Origem         | Categoria/Origem |


## 📊 Comparativo entre os bancos de dados de receita

Os dados da receita pública são divulgados através de diferentes fontes, cada uma possuindo características específicas:

### **1. Dados do Portal da Transparência**
Os dados disponibilizados no [Portal da Transparência](https://www.transparencia.mg.gov.br/receitas/) relacionados à receita pública indicam conjuntos de dados de [Receita](https://www.transparencia.mg.gov.br/receitas/estado-receita) Orçamentária, [Dívida Ativa](https://www.fazenda.mg.gov.br/empresas/Consulta-Divida-Ativa/Relatorios/), contendo relação montantes de crédito do Estado_, [Reunúncias e Desonerações](https://www.transparencia.mg.gov.br/receitas/renuncias-e-desoneracoes) da receita e [Arrecadação por Município](https://www.fazenda.mg.gov.br/governo/receita_estado/evolucao_receita_cnae/).  

A respeito do conjunto de dados da Receita Orçamentária, ele traz a execução orçamentária da em um nível de agregamento maior, sem incluir informações de `mês` e `unidade orçamentária`. Além disso, a classificação da receita é organizada tão somente por **categoria** e **origem**, sem detalhamento doss demais subcampos.


### **2. Dados do Portal de Dados Abertos (DadosMG)**
O [DadosMG](https://dados.mg.gov.br/) disponibiliza um conjunto de dados da receita denominado [Receita Pública](https://www.dados.mg.gov.br/dataset/receita) e contém informações semelhante às do `datapackages-AID`, porém com menor granularidade. Um dos pontos identificados é que o código de **classificação da receita** foi particionado em seus subcampos (Categoria, Origem, Espécie, Desdobramento...), o que pode gerar uma pretensão equivocada de interpretação isolada desses códigos, eventualmente prejudicando a análise das tabelas fato. Isso, pois os subcampos dos códigos de natureza da receita, uma vez que não são de registro único/primário, somente fazem sentido quando associados à sua matriz de classificação.


### **3. Dados AID (datapackages-AID)**
Os dados extraídos do `datapackages-AID` possuem um nível detalhado de informação, contendo variáveis como:
- **Ano e Mês** do exercício financeiro;
- **Unidade Orçamentária** vinculada ao registro;
- **Fonte de Recurso**;
- **Código de Natureza de Receita** completo;
- **Valores Previstos e Executados**.


## 📄 Considerações Finais

Os diferentes bancos de dados da receita possuem propósitos distintos: enquanto o `datapackages-AID` apresenta maior detalhamento, permitindo análises mais precisas, o Portal da Transparência e o DadosMG oferecem visões mais agregadas, que podem ser mais acessíveis para o público geral.

A publicação dos dados da receita conforme o `datapackages-AID` no portal DadosMG contribuirá significativamente para a melhoria da disponibilidade e qualidade das informações. Isso permitirá que todas as informações já disponibilizadas atualmente sejam mantidas e, ao mesmo tempo, aumentará a granularidade dos dados, incluindo variáveis importantes como `mês`, `unidade orçamentária` e a `classificação` completa da receita. Dessa forma, a análise e a transparência da execução orçamentária do Estado serão aprimoradas, possibilitando estudos mais detalhados e embasados.


