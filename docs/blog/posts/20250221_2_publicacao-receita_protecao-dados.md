---
date: 2025-02-21
authors: [carloshob]
draft: false
comments: true
categories:
  - Dados Abertos MG
---

# 📑 Publicação das Bases da Receita - Análise sobre Proteção de Dados

A análise acerca proteção de dados na publicação das bases da receita pública orçamentária tem como objetivo identificar e mitigar riscos relacionados à exposição de informações sensíveis, garantindo a conformidade com as normas de privacidade e transparência. Esse processo envolve a avaliação criteriosa dos dados a serem disponibilizados, assegurando que nenhuma informação que possa comprometer a privacidade de indivíduos ou entidades seja divulgada indevidamente. A implementação de mecanismos de anonimização e controle é essencial para equilibrar a abertura de dados com a segurança das informações, promovendo o acesso público sem comprometer direitos fundamentais.

> 🧠 _"Em um mundo onde os dados são constantemente coletados, a privacidade se torna um pré-requisito para a liberdade. Sem ela, os indivíduos perdem a capacidade de moldar suas próprias vidas."_
> – Shoshana Zuboff, The Age of Surveillance Capitalism (2019).




<!-- more -->

## 🎓  Estudo Sobre Dados Sensíveis

As principais normas que regulamentam a publicização de dados são:

- **📜 Lei da Transparência** - [Lei Complementar Federal n. 131, de 27 de maio de 2009](https://www.planalto.gov.br/ccivil_03/leis/lcp/lcp131.htm)  
- **📜 Lei de Acesso à Informação (LAI)** - [Lei Federal n. 12.527, de 18 de novembro de 2011](https://www.planalto.gov.br/ccivil_03/_ato2011-2014/2011/lei/l12527.htm)  
- **📜 Decreto de Acesso à Informação (DAI)** - [Decreto Federal n. 7.724, de 16 de maio de 2012](https://www.planalto.gov.br/ccivil_03/_ato2011-2014/2012/decreto/d7724.htm)  
- **📜 Lei Geral de Proteção de Dados (LGPD)** - [Lei Federal n. 13.709, de 14 de agosto de 2018](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm)  

---

### 📂 CNPJ e Dados de Pessoa Jurídica

O CNPJ é um dado público por natureza, conforme estabelecido pela [Lei nº 8.934/1994](https://www.planalto.gov.br/ccivil_03/leis/l8934.htm), que regula o Cadastro Nacional da Pessoa Jurídica (CNPJ). Portanto, a publicização do CNPJ de empresas que recebem pagamentos do Estado é permitida, desde que esteja relacionada à execução orçamentária e à transparência das despesas públicas.

> [DAI](https://www.planalto.gov.br/ccivil_03/_ato2011-2014/2012/decreto/d7724.htm)

> _Art. 7º É dever dos órgãos e entidades promover, independente de requerimento, a divulgação em seus sítios na Internet de informações de interesse coletivo ou geral por eles produzidas ou custodiadas, observado o disposto nos arts. 7º e 8º da Lei nº 12.527, de 2011._
>
> _(...)_
>
> _V - licitações realizadas e em andamento, com editais, anexos e resultados, além dos **contratos firmados e notas de empenho** emitidas; (...)_

---

### 👤 Nome e CPF de Pessoas Físicas Beneficiadas com Pagamentos Públicos

A publicação de nomes e CPF de pessoas físicas que foram destinatárias de pagamentos públicos é um tema sensível, já que, enquanto exercentes de sua cidadania, seus dados pessoais têm proteção garantida pela LGPD e o direito à privacidade previsto na Constituição Federal.

No entanto, ainda assim, **não é consensual** a proibição de publicação dessa informação caso a pessoa física seja contratante com a Administração Pública ou a ela vinculada.

Feitas essas ponderações, considerando que o **direito à intimidade** é de relevante proteção no ordenamento jurídico brasileiro, acredito que o mais sensato seja um comportamento mais conservador em relação à proteção de um dado pessoal, sensível ou não. Portanto, entendo que devemos cuidar ou da **ocultação** ou da **anonimização** do nome e do CPF — a menos que haja um caso concreto sobre o qual seja aplicável base legal específica que autorize/determine a sua publicação.


> [LGPD](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm)

> _Art. 5º Para os fins desta Lei, considera-se:_

> _I - **dado pessoal:** informação relacionada a pessoa natural identificada ou identificável;_

> _II - **dado pessoal sensível:** dado pessoal sobre origem racial ou étnica, convicção religiosa, opinião política, filiação a sindicato ou a organização de caráter religioso, filosófico ou político, dado referente à saúde ou à vida sexual, dado genético ou biométrico, quando vinculado a uma pessoa natural;_

> _(...)_

> _XI - **anonimização:** utilização de meios técnicos razoáveis e disponíveis no momento do tratamento, por meio dos quais um dado perde a possibilidade de associação, direta ou indireta, a um indivíduo;_


## Dados disponibilizados na receita

São os seguintes dados disponibilizados da receita orçamentária pública:

  - **`Ano de Exercício`:** ano de exercício do orçamento fiscal.

  - **`Mês - Numérico`:** mês numérico do registro da respectiva receita.

  - **`Unidade Orçamentária - Código`:** código representativo da unidade orçamentária responsável pela identificação da receita arrecadada.

  - **`Fonte Recurso - Código`:** código da fonte de recurso origem da receita orçamentária.

  - **`Classificação Receita - Código`:** código  completo (13 dígitos) da classificação por natureza da receita (formato: xxxxxxxxxxxxx) correspondente a números de código decimal que integram a classificação da receita orçamentária.

  - **`Classificação Receita - Descrição`:** descrição da classificação completa da natureza da receita.

  - **`Classificação Receita - Formatado`:** código  completo (13 dígitos) da classificação por natureza da receita (formato: xxxx.x.xx.x.xx.xxx) correspondente a números de código decimal que integram a classificação da receita orçamentária.

  - **`Valor Previsto Inicial`:** valor, em reais, da previsão inicial da receita constante da Lei Orçamentária.

  - **`Valor Previsto Adicional`:** valor, em reais, da previsão adicional da receita.

  - **`Valor Previsto Atualizado`:** valor, em reais, da previsão atualizada da receita, resultante da expressão: Valor previsto inicial + Valor previsto adicional.

  - **`Valor Contabilizado`:** valor, em reais, da receita orçamentária contabilizada, aparecendo negativo quando houver cancelamento de receita.

  - **`Valor Efetivado Ajustado`:** valor, em reais, da receita orçamentária efetivada ajustada conforme mês de contabilização.

Em conclusão, a análise da base da receita pública orçamentária indica que não há dados, sensíveis ou não, que necessitem de proteção, ocultação ou anonimização. As informações contidas nessa base, como códigos de classificação da receita, valores previstos e contabilizados, e identificadores de unidades orçamentárias, são de natureza essencialmente técnica e institucional, não envolvendo dados pessoais ou sensíveis que possam comprometer a privacidade de indivíduos ou entidades. A publicização desses dados está alinhada com os princípios de transparência e acesso à informação, garantindo o controle social e a fiscalização dos recursos públicos sem infringir normas de proteção de dados. Portanto, a base da receita pode ser disponibilizada integralmente, assegurando o equilíbrio entre a transparência e a conformidade com a legislação vigente.
