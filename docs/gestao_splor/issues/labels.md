---
title: Labels de Issues
---

# Labels de Issues 🏷️

## Relação com Semantic Versioning

As **labels** de issues na SPLOR estão diretamente relacionadas ao **Semantic Versioning** (SemVer), um padrão de versionamento que facilita a comunicação sobre mudanças e impactos das atualizações. Esta relação garante consistência entre o que é discutido nas issues e o que é implementado no código.

### Conceito do Semantic Versioning

O Semantic Versioning usa o formato `MAJOR.MINOR.PATCH` onde:

- **MAJOR**: Mudanças incompatíveis com versões anteriores
- **MINOR**: Novas funcionalidades compatíveis
- **PATCH**: Correções de bugs compatíveis

## Labels Propostas para SPLOR

### Labels Baseadas no SemVer

#### `fix` 🔧
- **Corresponde a**: PATCH version
- **Uso**: Correções de bugs e problemas
- **Exemplo**: "Corrigir erro na validação de dados"
- **Impacto**: Baixo, não quebra funcionalidades existentes

#### `feat` ✨
- **Corresponde a**: MINOR version
- **Uso**: Novas funcionalidades
- **Exemplo**: "Adicionar novo relatório de indicadores"
- **Impacto**: Médio, adiciona funcionalidades sem quebrar existentes

#### `docs` 📚
- **Corresponde a**: PATCH version
- **Uso**: Melhorias na documentação
- **Exemplo**: "Atualizar README com novas instruções"
- **Impacto**: Baixo, apenas documentação

#### `build` 🔨
- **Corresponde a**: PATCH version
- **Uso**: Mudanças no sistema de build
- **Exemplo**: "Atualizar dependências do projeto"
- **Impacto**: Baixo, infraestrutura

#### `test` 🧪
- **Corresponde a**: PATCH version
- **Uso**: Adição ou correção de testes
- **Exemplo**: "Adicionar testes para nova funcionalidade"
- **Impacto**: Baixo, qualidade

#### `chore` 🛠️
- **Corresponde a**: PATCH version
- **Uso**: Tarefas de manutenção
- **Exemplo**: "Limpar código não utilizado"
- **Impacto**: Baixo, manutenção

### Labels de Planejamento

#### `planejado` 📋
- **Uso**: Issues que fazem parte do planejamento
- **Exemplo**: Funcionalidades planejadas para o próximo sprint
- **Benefício**: Facilita o acompanhamento do planejamento

#### `nao_planejado` ⚡
- **Uso**: Issues que surgiram durante o desenvolvimento
- **Exemplo**: Bugs descobertos durante testes
- **Benefício**: Identifica trabalho não previsto

### Labels de Comunicação

#### `question` ❓
- **Uso**: Dúvidas rápidas e pontuais
- **Exemplo**: "Como configurar o ambiente de desenvolvimento?"
- **Benefício**: Facilita identificação de dúvidas

#### `wontfix` 🚫
- **Uso**: Problemas identificados mas sem solução viável
- **Exemplo**: "Limitação técnica conhecida"
- **Benefício**: Evita retrabalho em problemas sem solução

## Reflexão: Redundância de Trabalho?

### Análise Crítica

A utilização de labels pode parecer uma **redundância de trabalho** em alguns casos, mas oferece benefícios significativos:

#### Vantagens das Labels

- **Categorização automática** de issues
- **Filtros eficientes** para visualização
- **Relatórios automáticos** de progresso
- **Comunicação clara** sobre tipos de mudança
- **Integração** com ferramentas de CI/CD

#### Possíveis Redundâncias

- **Duplicação** com títulos descritivos
- **Esforço extra** para classificação
- **Inconsistência** na aplicação
- **Complexidade** para novos membros

### Estratégia de Otimização

#### Automação
- **Templates** de issues com labels pré-definidas
- **GitHub Actions** para aplicar labels automaticamente
- **Integração** com ferramentas de análise de código

#### Simplificação
- **Redução** do número de labels
- **Foco** nas mais utilizadas
- **Documentação** clara de uso

## Implementação na SPLOR

### Configuração Inicial

1. **Criar** labels na organização
2. **Configurar** cores e descrições
3. **Documentar** critérios de uso
4. **Treinar** equipe sobre aplicação

### Templates de Issues

#### Bug Report
```yaml
labels: ["fix", "nao_planejado"]
assignees: []
title: "[BUG] Descrição do problema"
body: |
  ## Descrição
  [Descreva o problema]

  ## Comportamento Esperado
  [O que deveria acontecer]

  ## Comportamento Atual
  [O que está acontecendo]
```

#### Feature Request
```yaml
labels: ["feat", "planejado"]
assignees: []
title: "[FEAT] Nova funcionalidade"
body: |
  ## Descrição
  [Descreva a funcionalidade]

  ## Justificativa
  [Por que é necessária]

  ## Critérios de Aceitação
  - [ ] Critério 1
  - [ ] Critério 2
```

#### Documentation
```yaml
labels: ["docs"]
assignees: []
title: "[DOCS] Melhoria na documentação"
body: |
  ## Área
  [Qual área da documentação]

  ## Melhoria Proposta
  [O que deve ser melhorado]
```

### Workflow de Aplicação

1. **Criar issue** com template apropriado
2. **Labels são aplicadas** automaticamente
3. **Revisar** e ajustar se necessário
4. **Desenvolver** seguindo o tipo da issue
5. **Commit** usando conventional commits

## Integração com Conventional Commits

### Mapeamento Direto

| Label | Commit Type | Version Impact |
|-------|-------------|----------------|
| `fix` | `fix:` | PATCH |
| `feat` | `feat:` | MINOR |
| `docs` | `docs:` | PATCH |
| `build` | `build:` | PATCH |
| `test` | `test:` | PATCH |
| `chore` | `chore:` | PATCH |

### Benefícios da Integração

- **Consistência** entre issues e commits
- **Automação** de changelog
- **Versionamento** automático
- **Rastreabilidade** completa

## Monitoramento e Métricas

### KPIs Sugeridos

- **Distribuição** de tipos de issues
- **Tempo médio** de resolução por tipo
- **Taxa de issues planejadas vs não planejadas**
- **Qualidade** da aplicação de labels

### Relatórios Automáticos

- **Sprint retrospectives** baseadas em labels
- **Análise** de tendências de desenvolvimento
- **Identificação** de áreas problemáticas
- **Planejamento** baseado em dados

## Próximos Passos

1. **Implementar** labels na organização
2. **Criar** templates de issues
3. **Configurar** automação
4. **Treinar** equipe
5. **Monitorar** e ajustar 