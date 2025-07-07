---
title: Tipos de Issues
---

# Tipos de Issues 📋

## Análise de Impacto e Importância

O sistema de **tipos de issues** na SPLOR é baseado na análise de **impacto** e **importância** de cada atividade. Esta classificação permite priorizar adequadamente o trabalho e alocar recursos de forma eficiente.

### Critérios de Classificação

#### Impacto
- **Alto**: Afeta múltiplos usuários ou sistemas críticos
- **Médio**: Afeta alguns usuários ou funcionalidades importantes
- **Baixo**: Afeta poucos usuários ou funcionalidades secundárias

#### Importância
- **Alta**: Crítica para o funcionamento ou objetivos estratégicos
- **Média**: Importante para melhorias ou funcionalidades
- **Baixa**: Desejável mas não essencial

## Níveis de Priorização

### Nível 1 - Alta Prioridade 🔴

#### Características
- **Impacto**: Alto
- **Importância**: Alta
- **Urgência**: Imediata
- **Recursos**: Máxima atenção

#### Exemplos
- **Bugs críticos** que impedem o funcionamento
- **Vulnerabilidades de segurança** identificadas
- **Problemas de compliance** regulatório
- **Falhas em sistemas de produção**
- **Dados corrompidos** ou perdidos

#### Processo de Tratamento
1. **Identificação imediata** e notificação
2. **Alocação de recursos** prioritários
3. **Desenvolvimento** em paralelo se necessário
4. **Testes rigorosos** antes do deploy
5. **Comunicação** clara sobre resolução

### Nível 2 - Média Prioridade 🟡

#### Características
- **Impacto**: Médio
- **Importância**: Média
- **Urgência**: Planejada
- **Recursos**: Atenção normal

#### Exemplos
- **Novas funcionalidades** planejadas
- **Melhorias** em sistemas existentes
- **Otimizações** de performance
- **Atualizações** de documentação
- **Refatoração** de código

#### Processo de Tratamento
1. **Planejamento** no próximo sprint
2. **Estimativa** de tempo e recursos
3. **Desenvolvimento** seguindo cronograma
4. **Testes** padrão
5. **Deploy** em release planejado

### Nível 3 - Baixa Prioridade 🟢

#### Características
- **Impacto**: Baixo
- **Importância**: Baixa
- **Urgência**: Baixa
- **Recursos**: Quando disponível

#### Exemplos
- **Melhorias cosméticas** na interface
- **Documentação adicional** opcional
- **Otimizações menores** de código
- **Funcionalidades** "nice to have"
- **Limpeza** de código não crítico

#### Processo de Tratamento
1. **Backlog** para quando houver tempo
2. **Desenvolvimento** em paralelo com outras tarefas
3. **Testes** básicos
4. **Deploy** em releases menores

## Matriz de Decisão

### Critérios de Classificação

| Critério | Nível 1 | Nível 2 | Nível 3 |
|----------|---------|---------|---------|
| **Usuários Afetados** | >50% | 10-50% | <10% |
| **Tempo de Resolução** | <24h | 1-7 dias | >7 dias |
| **Recursos Necessários** | Múltiplos | 1-2 pessoas | 1 pessoa |
| **Risco de Negócio** | Alto | Médio | Baixo |
| **Dependências** | Múltiplas | Algumas | Poucas |

### Exemplos Práticos

#### Nível 1 - Sistema de Dados Abertos
```
Issue: "Sistema de dados abertos fora do ar"
Impacto: Todos os usuários externos não conseguem acessar dados
Importância: Crítica para transparência governamental
Classificação: Nível 1 - Alta Prioridade
```

#### Nível 2 - Novo Relatório
```
Issue: "Adicionar relatório de indicadores orçamentários"
Impacto: Analistas internos terão nova ferramenta
Importância: Melhora a capacidade de análise
Classificação: Nível 2 - Média Prioridade
```

#### Nível 3 - Melhoria de Interface
```
Issue: "Melhorar cores do dashboard"
Impacto: Apenas aspecto visual
Importância: Melhora experiência do usuário
Classificação: Nível 3 - Baixa Prioridade
```

## Workflow de Classificação

### Processo de Avaliação

1. **Criação** da issue com descrição detalhada
2. **Análise inicial** de impacto e importância
3. **Classificação** em nível apropriado
4. **Revisão** por gestor ou tech lead
5. **Ajuste** se necessário
6. **Aprovação** final

### Responsabilidades

#### Criador da Issue
- **Descrever** claramente o problema/necessidade
- **Identificar** usuários afetados
- **Estimar** impacto inicial
- **Sugerir** nível de prioridade

#### Gestor/Tech Lead
- **Revisar** classificação proposta
- **Ajustar** baseado em contexto organizacional
- **Validar** recursos necessários
- **Aprovar** classificação final

#### Equipe de Desenvolvimento
- **Questionar** classificação se necessário
- **Propor** ajustes baseados em complexidade técnica
- **Estimar** tempo de desenvolvimento
- **Identificar** dependências

## Templates por Nível

### Template Nível 1 - Alta Prioridade
```markdown
## Descrição
[Descreva o problema crítico]

## Impacto
- Usuários afetados: [Número/Percentual]
- Sistemas afetados: [Lista]
- Tempo de indisponibilidade: [Estimativa]

## Urgência
- Prazo máximo: [Data/Hora]
- Consequências se não resolvido: [Descrição]

## Recursos Necessários
- Pessoas: [Lista]
- Tempo estimado: [Horas/Dias]
- Dependências: [Lista]

## Critérios de Aceitação
- [ ] Sistema funcionando
- [ ] Testes realizados
- [ ] Documentação atualizada
```

### Template Nível 2 - Média Prioridade
```markdown
## Descrição
[Descreva a funcionalidade/melhoria]

## Justificativa
- Benefícios: [Lista]
- Usuários beneficiados: [Descrição]
- Alinhamento estratégico: [Como se alinha]

## Recursos
- Pessoas: [Lista]
- Tempo estimado: [Horas/Dias]
- Dependências: [Lista]

## Critérios de Aceitação
- [ ] Funcionalidade implementada
- [ ] Testes realizados
- [ ] Documentação atualizada
- [ ] Treinamento realizado (se necessário)
```

### Template Nível 3 - Baixa Prioridade
```markdown
## Descrição
[Descreva a melhoria desejada]

## Benefícios
- Melhoria: [Descrição]
- Usuários: [Quem se beneficia]

## Recursos
- Pessoas: [Lista]
- Tempo estimado: [Horas/Dias]

## Critérios de Aceitação
- [ ] Melhoria implementada
- [ ] Testes básicos realizados
```

## Monitoramento e Ajustes

### Métricas de Acompanhamento

- **Tempo médio** de resolução por nível
- **Taxa de reclassificação** de issues
- **Satisfação** da equipe com classificação
- **Aderência** aos prazos estabelecidos

### Processo de Revisão

- **Revisão semanal** de issues em cada nível
- **Ajuste** de classificação se necessário
- **Feedback** da equipe sobre critérios
- **Melhoria** contínua do processo

## Integração com Ferramentas

### GitHub Labels
- `priority-1`: Alta prioridade
- `priority-2`: Média prioridade
- `priority-3`: Baixa prioridade

### GitHub Projects
- **Colunas** por nível de prioridade
- **Automação** baseada em labels
- **Relatórios** de progresso

### Ferramentas de Gestão
- **Integração** com Jira, Trello, etc.
- **Sincronização** de prioridades
- **Relatórios** unificados

## Próximos Passos

1. **Implementar** sistema de classificação
2. **Criar** templates por nível
3. **Treinar** equipe sobre critérios
4. **Configurar** automação
5. **Monitorar** e ajustar processo 