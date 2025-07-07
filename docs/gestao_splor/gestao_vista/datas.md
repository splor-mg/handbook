---
title: Gestão de Datas
---

# Gestão de Datas 📅

## Data Início vs Data Fim

A gestão eficiente de **datas** é fundamental para o planejamento e acompanhamento de projetos na SPLOR. O sistema de datas permite controlar prazos, identificar atrasos e garantir que as entregas sejam realizadas no tempo adequado.

### Conceito de Datas

#### Data de Início
- **Momento** em que a atividade deve começar
- **Base** para cálculo de duração
- **Referência** para alocação de recursos
- **Ponto de partida** do planejamento

#### Data de Fim
- **Momento** em que a atividade deve ser concluída
- **Expectativa** de finalização
- **Prazo** para entrega
- **Objetivo** temporal a ser atingido

## Campo "Data Prevista" do Gestão à Vista

### Preenchimento Correto

O campo **"Data prevista"** do Gestão à Vista deve ser preenchido como **expectativa real de finalização** da Issue, não mais para marcar se a Issue era prevista ou não. Esta mudança traz maior precisão ao planejamento e acompanhamento.

#### Antes (Incorreto)
- **Data prevista**: Usado para marcar se Issue era planejada
- **Resultado**: Informação temporal imprecisa
- **Problema**: Dificuldade de acompanhar prazos reais

#### Agora (Correto)
- **Data prevista**: Expectativa real de finalização
- **Resultado**: Planejamento temporal preciso
- **Benefício**: Controle efetivo de prazos

### Como Preencher

#### Estimativa Realista
- **Baseada** na complexidade da atividade
- **Considerando** recursos disponíveis
- **Incluindo** tempo para testes e revisão
- **Adicionando** margem de segurança

#### Fatores a Considerar
- **Complexidade** técnica da atividade
- **Experiência** do desenvolvedor
- **Dependências** externas
- **Disponibilidade** de recursos
- **Qualidade** esperada

## Tipos de Datas

### Datas de Planejamento

#### Data de Início Planejada
- **Quando** a atividade deve começar
- **Baseada** na disponibilidade de recursos
- **Alinhada** com cronograma do projeto
- **Comunicada** à equipe

#### Data de Fim Planejada
- **Quando** a atividade deve terminar
- **Calculada** a partir da data de início
- **Considerando** duração estimada
- **Aprovada** pelo gestor

### Datas Reais

#### Data de Início Real
- **Quando** a atividade realmente começou
- **Registrada** no momento do início
- **Comparada** com data planejada
- **Analisada** para melhorias

#### Data de Fim Real
- **Quando** a atividade foi realmente concluída
- **Registrada** no momento da conclusão
- **Comparada** com data planejada
- **Usada** para métricas de performance

## Processo de Gestão de Datas

### Planejamento Inicial

#### 1. Estimativa de Duração
- **Análise** da complexidade da atividade
- **Comparação** com atividades similares
- **Consulta** à equipe técnica
- **Definição** de duração estimada

#### 2. Definição de Datas
- **Data de início**: Baseada na disponibilidade
- **Data de fim**: Data de início + duração estimada
- **Margem de segurança**: 10-20% adicional
- **Aprovação**: Pelo gestor do projeto

#### 3. Comunicação
- **Informar** equipe sobre datas
- **Documentar** no sistema
- **Comunicar** stakeholders
- **Atualizar** cronograma

### Acompanhamento Contínuo

#### 1. Monitoramento Diário
- **Verificar** progresso das atividades
- **Identificar** possíveis atrasos
- **Ajustar** datas se necessário
- **Comunicar** mudanças

#### 2. Revisão Semanal
- **Analisar** progresso do sprint
- **Identificar** atividades atrasadas
- **Ajustar** prioridades se necessário
- **Planejar** próximas atividades

#### 3. Ajustes Quando Necessário
- **Revisar** estimativas originais
- **Identificar** causas de atraso
- **Implementar** ações corretivas
- **Comunicar** mudanças

## Ferramentas de Gestão

### GitHub Issues

#### Campos de Data
- **Created**: Data de criação da issue
- **Updated**: Data da última atualização
- **Due date**: Data prevista de conclusão
- **Milestone**: Marco do projeto

#### Configuração
```yaml
# Exemplo de issue com datas
title: "Implementar novo relatório"
assignee: "@desenvolvedor"
due_date: "2024-02-15"
milestone: "Sprint 3"
labels: ["feature", "high-priority"]
```

### GitHub Projects

#### Colunas com Datas
- **Backlog**: Sem data específica
- **This Week**: Atividades da semana atual
- **Next Week**: Atividades da próxima semana
- **Overdue**: Atividades atrasadas

#### Automação
- **Mover** automaticamente baseado em datas
- **Alertar** sobre atividades atrasadas
- **Gerar** relatórios de progresso
- **Notificar** responsáveis

### Ferramentas Externas

#### Calendários
- **Google Calendar**: Integração com GitHub
- **Outlook**: Sincronização de datas
- **Calendário da equipe**: Visão compartilhada

#### Dashboards
- **Grafana**: Métricas de tempo
- **Power BI**: Análise de performance
- **Metabase**: Relatórios customizados

## Métricas de Tempo

### Indicadores de Performance

#### Aderência ao Prazo
- **Taxa** de atividades no prazo
- **Tempo médio** de atraso
- **Frequência** de atrasos
- **Impacto** de atrasos

#### Precisão das Estimativas
- **Diferença** entre estimado e real
- **Tendência** de subestimação
- **Melhoria** ao longo do tempo
- **Fatores** que afetam precisão

#### Velocidade da Equipe
- **Issues** concluídas por período
- **Tempo médio** por tipo de atividade
- **Eficiência** de desenvolvimento
- **Capacidade** da equipe

### Relatórios de Acompanhamento

#### Relatório Semanal
- **Atividades** concluídas no prazo
- **Atividades** atrasadas
- **Causas** de atrasos
- **Ações** corretivas

#### Relatório Mensal
- **Tendências** de performance
- **Melhorias** implementadas
- **Métricas** de qualidade
- **Planejamento** do próximo mês

## Boas Práticas

### Para Estimativas

#### Estimativa por Pontos
- **Story points**: Medida relativa de complexidade
- **Velocidade**: Pontos por sprint
- **Histórico**: Base para estimativas futuras
- **Refinamento**: Ajuste contínuo

#### Estimativa por Tempo
- **Horas**: Tempo estimado em horas
- **Dias**: Tempo estimado em dias
- **Semanas**: Para atividades complexas
- **Margem**: Buffer de segurança

### Para Acompanhamento

#### Atualizações Regulares
- **Diária**: Progresso das atividades
- **Semanal**: Revisão de prazos
- **Mensal**: Análise de tendências
- **Trimestral**: Planejamento estratégico

#### Comunicação Clara
- **Transparência**: Compartilhar status
- **Proatividade**: Alertar sobre riscos
- **Colaboração**: Buscar ajuda quando necessário
- **Documentação**: Registrar decisões

## Troubleshooting

### Problemas Comuns

#### Estimativas Inconsistentes
- **Causa**: Falta de padrão na estimativa
- **Solução**: Implementar processo padronizado
- **Prevenção**: Treinamento da equipe
- **Monitoramento**: Revisão regular

#### Atrasos Frequentes
- **Causa**: Estimativas muito otimistas
- **Solução**: Adicionar margem de segurança
- **Prevenção**: Análise de causas raiz
- **Monitoramento**: Métricas de performance

#### Falta de Visibilidade
- **Causa**: Datas não atualizadas
- **Solução**: Processo de atualização
- **Prevenção**: Automação de notificações
- **Monitoramento**: Compliance da equipe

## Processo de Melhoria

### Análise Retrospectiva

#### Coleta de Dados
- **Histórico** de estimativas vs real
- **Causas** de atrasos
- **Fatores** de sucesso
- **Lições** aprendidas

#### Análise de Tendências
- **Padrões** identificados
- **Melhorias** implementadas
- **Impacto** das mudanças
- **Próximos** passos

#### Implementação de Melhorias
- **Processos** atualizados
- **Ferramentas** implementadas
- **Treinamento** da equipe
- **Monitoramento** contínuo

## Próximos Passos

1. **Implementar** processo de estimativa
2. **Configurar** automação de datas
3. **Treinar** equipe sobre boas práticas
4. **Monitorar** métricas de performance
5. **Melhorar** continuamente o processo 