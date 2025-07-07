---
title: Repositórios Públicos vs Privados
---

# Repositórios Públicos vs Privados 🔓🔒

## Decisão Estratégica

A escolha entre repositórios **públicos** ou **privados** é uma decisão estratégica que deve ser tomada considerando a natureza do projeto, os dados envolvidos e os objetivos da SPLOR. Esta decisão impacta diretamente a transparência, colaboração e segurança dos projetos.

## Repositórios Públicos 🌐

### Quando Usar

Repositórios públicos são ideais para:

- **Projetos de dados abertos** e transparência
- **Documentação pública** e manuais
- **Ferramentas e automações** que podem beneficiar a comunidade
- **Código não sensível** que pode ser reutilizado
- **Projetos educacionais** e de capacitação

### Benefícios

#### Transparência
- ✅ **Visibilidade total** para a sociedade
- ✅ **Demonstração** de boas práticas
- ✅ **Accountability** público
- ✅ **Confiança** na administração

#### Colaboração
- ✅ **Contribuições** da comunidade
- ✅ **Feedback** externo
- ✅ **Reutilização** de código
- ✅ **Networking** com outras organizações

#### Desenvolvimento
- ✅ **Revisão** de código pública
- ✅ **Documentação** acessível
- ✅ **Histórico** transparente
- ✅ **Padrões** abertos

### Exemplos de Repositórios Públicos

```
splor-mg-dados-abertos
splor-mg-docs-handbook
splor-mg-automacao-relatorios-publicos
splor-mg-templates-documentos
splor-mg-exemplos-codigo
```

## Repositórios Privados 🔒

### Quando Usar

Repositórios privados são necessários para:

- **Dados sensíveis** e confidenciais
- **Sistemas internos** da administração
- **Código proprietário** ou estratégico
- **Projetos em desenvolvimento** que não devem ser expostos
- **Informações pessoais** ou restritas

### Benefícios

#### Segurança
- ✅ **Controle de acesso** restrito
- ✅ **Proteção** de dados sensíveis
- ✅ **Compliance** com LGPD
- ✅ **Auditoria** de acesso

#### Desenvolvimento
- ✅ **Experimentação** sem exposição
- ✅ **Refinamento** antes da publicação
- ✅ **Testes** internos
- ✅ **Iteração** rápida

#### Estratégia
- ✅ **Proteção** de vantagens competitivas
- ✅ **Controle** de timing de lançamento
- ✅ **Gestão** de reputação
- ✅ **Compliance** regulatório

### Exemplos de Repositórios Privados

```
splor-mg-dados-sensiveis-orcamentarios
splor-mg-sistema-interno-gestao
splor-mg-automacao-dados-pessoais
splor-mg-projeto-em-desenvolvimento
splor-mg-documentos-internos
```

## Critérios de Decisão

### Matriz de Decisão

| Critério | Público | Privado |
|----------|---------|---------|
| **Dados Sensíveis** | ❌ | ✅ |
| **Código Estratégico** | ❌ | ✅ |
| **Transparência** | ✅ | ❌ |
| **Colaboração Externa** | ✅ | ❌ |
| **LGPD Compliance** | ⚠️ | ✅ |
| **Reutilização** | ✅ | ❌ |
| **Desenvolvimento Ativo** | ⚠️ | ✅ |

### Checklist de Avaliação

#### Para Repositórios Públicos

- ✅ [ ] Não contém dados pessoais
- ✅ [ ] Não expõe informações estratégicas
- ✅ [ ] Segue políticas de transparência
- ✅ [ ] Pode beneficiar a comunidade
- ✅ [ ] Documentação adequada
- ✅ [ ] Código de conduta definido

#### Para Repositórios Privados

- ✅ [ ] Contém dados sensíveis
- ✅ [ ] Requer controle de acesso
- ✅ [ ] Em desenvolvimento ativo
- ✅ [ ] Informações estratégicas
- ✅ [ ] Compliance regulatório
- ✅ [ ] Necessidade de auditoria

## Políticas da SPLOR

### Princípios Gerais

1. **Transparência por padrão**: Preferir repositórios públicos quando possível
2. **Segurança primeiro**: Proteger dados sensíveis e estratégicos
3. **Compliance obrigatório**: Seguir LGPD e outras regulamentações
4. **Documentação clara**: Explicar decisões de visibilidade

### Processo de Decisão

1. **Avaliar** o conteúdo do repositório
2. **Identificar** dados sensíveis ou estratégicos
3. **Consultar** políticas de transparência
4. **Decidir** baseado na matriz de critérios
5. **Documentar** a decisão e justificativa

## Migração entre Tipos

### Público → Privado

**Quando necessário:**
- Descoberta de dados sensíveis
- Mudança de estratégia
- Requisitos de compliance
- Proteção de informações

**Processo:**
1. **Avaliar** impacto da mudança
2. **Notificar** colaboradores
3. **Fazer backup** se necessário
4. **Alterar** configuração
5. **Documentar** mudança

### Privado → Público

**Quando apropriado:**
- Projeto maduro e estável
- Dados não sensíveis
- Benefício para comunidade
- Política de transparência

**Processo:**
1. **Revisar** todo o conteúdo
2. **Remover** dados sensíveis
3. **Atualizar** documentação
4. **Configurar** código de conduta
5. **Tornar** público

## Monitoramento e Auditoria

### Repositórios Públicos

- **Revisão periódica** do conteúdo
- **Monitoramento** de contribuições
- **Verificação** de compliance
- **Atualização** de documentação

### Repositórios Privados

- **Auditoria** de acesso
- **Revisão** de permissões
- **Monitoramento** de atividades
- **Backup** regular

## Ferramentas e Automação

### GitHub Actions

Podemos configurar ações para:
- **Detectar** dados sensíveis automaticamente
- **Alertar** sobre possíveis violações
- **Validar** configurações de segurança
- **Gerar** relatórios de compliance

### Scripts de Validação

Scripts podem verificar:
- **Presença** de dados sensíveis
- **Configurações** de segurança
- **Permissões** adequadas
- **Documentação** necessária

## Treinamento e Conscientização

### Para a Equipe

- **Orientação** sobre critérios de decisão
- **Treinamento** sobre LGPD
- **Conscientização** sobre segurança
- **Processos** claros de decisão

### Para Administradores

- **Políticas** de governança
- **Ferramentas** de monitoramento
- **Processos** de auditoria
- **Responsabilidades** claras

## Próximos Passos

1. **Revisar** repositórios existentes
2. **Classificar** por tipo apropriado
3. **Implementar** políticas de governança
4. **Configurar** ferramentas de monitoramento
5. **Treinar** equipe sobre critérios 