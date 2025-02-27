---
date: 2025-02-27
authors: [gabrielbdornas]
draft: false
comments: true
categories:
  - O futuro já começou
---

# Organização do Trabalho da Equipe AID

Nosso trabalho é totalmente gerenciado no GitHub, garantindo transparência e rastreabilidade em nossas tarefas.
Todos os **Issues** abertos em nossos repositórios são automaticamente adicionados ao nosso [**Board Gestão à Vista do GitHub Projects**](https://github.com/orgs/splor-mg/projects/13/), onde passam por diferentes estágios até sua conclusão.

<!-- more -->

## Fluxo de Trabalho

### Gestão de Issues e Sprints

1. **Criação de Issues**
    - Toda ideia, questão ou erro deve ser registrada como um **Issue** em um de nossos [repositórios](https://github.com/orgs/splor-mg/repositories).
    - Se a tarefa não for incluída na sprint atual, o Issue deve ser criado com o status **Backlog**.

1. **Planejamento Mensal**
    - No início de cada mês, realizamos uma reunião de planejamento para revisar os **Issues não finalizados** e decidir as prioridades do período.
    - Os Issues selecionados para a sprint do mês terão seu status alterado de **Backlog** para **Todo**.
    - O campo **Data Prevista** deve ser preenchido com o último dia do mês para os Issues planejados.

1. **Execução da Sprint**
    - Durante o mês, novos Issues podem surgir por motivos urgentes (como erros ou falhas inesperadas).
    - Esses Issues entrarão no status **Todo**, mas **não terão o campo Data Prevista preenchido**, indicando que não foram planejados antecipadamente.

1. **Finalização**
    - Os Issues classificados com **Todo** passam pelos estágios **In Progress**, **Review** e **Done** conforme avançam no desenvolvimento.

    !!! Note
        No futuro, planejamos implementar uma métrica de desempenho para medir a produtividade da equipe com base no número de Issues (planejados ou não) finalizados.

## Organização da View Individual

Cada integrante da equipe tem uma **view personalizada**, em formato de tabela, no GitHub Projects.
Atualmente, estas views contem os seguintes campos:

- **Status** (Backlog, Todo, In Progress, Review, Done).
- **Projeto**.
- **Título do Issue**.
- **Data Prevista**.
- **Sprint** (mensal).
- **Repositório**.
- **Linked Pull Requests**.

## Reuniões Semanais

### Reunião Gerencial
- Participação de toda a equipe.
- Cada integrante apresenta sua **view** e relata as ações realizadas, bem como dificuldades encontradas.

### Reunião Individual
- Encontro entre gestor e colaborador.
- Baseada na **view individual**, serve para fornecer e receber feedback sobre o trabalho realizado.

Essa estrutura nos permite acompanhar o andamento das atividades, identificar gargalos e garantir um fluxo de trabalho eficiente.
Como dito, a inteção é criar, no futuro, métricas de desempenho (quantitativo e qualitativo) para aprimorar ainda mais a gestão do time.
