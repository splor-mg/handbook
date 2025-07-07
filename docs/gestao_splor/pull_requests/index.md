---
title: Pull Requests
---

# Pull Requests 🔄

## Revisão e Aprovação de Mudanças

Os **Pull Requests (PRs)** são o mecanismo central de colaboração e controle de qualidade no GitHub. Na SPLOR, utilizamos PRs para garantir que todas as mudanças sejam revisadas, testadas e aprovadas antes de serem integradas ao código principal.

## Conceito de Pull Requests

### O que são Pull Requests?

Um **Pull Request** é uma solicitação para integrar mudanças de uma branch para outra. É o momento onde o código é revisado, discutido e aprovado antes de ser mesclado. É como "pedir permissão" para integrar suas mudanças.

### Benefícios dos PRs

#### Controle de Qualidade
- ✅ **Revisão de código** por pares
- ✅ **Detecção de bugs** antes da integração
- ✅ **Validação** de testes automatizados
- ✅ **Verificação** de padrões de código

#### Colaboração
- ✅ **Discussão** sobre implementação
- ✅ **Compartilhamento** de conhecimento
- ✅ **Mentoria** para desenvolvedores júnior
- ✅ **Documentação** de decisões técnicas

#### Segurança
- ✅ **Proteção** contra mudanças não autorizadas
- ✅ **Auditoria** de todas as mudanças
- ✅ **Reversão** fácil se necessário
- ✅ **Histórico** completo de decisões

## Processo de Pull Request na SPLOR

### 1. Criação do PR

#### Antes de Criar
- ✅ **Branch atualizada** com a base
- ✅ **Commits organizados** e com mensagens claras
- ✅ **Testes passando** localmente
- ✅ **Documentação** atualizada se necessário

#### Template de PR
```markdown
## Descrição
[Descreva as mudanças realizadas]

## Tipo de Mudança
- [ ] Bug fix
- [ ] Nova funcionalidade
- [ ] Melhoria
- [ ] Documentação
- [ ] Refatoração

## Impacto
- **Usuários afetados**: [Descrição]
- **Sistemas afetados**: [Lista]
- **Breaking changes**: [Sim/Não]

## Testes
- [ ] Testes unitários passando
- [ ] Testes de integração passando
- [ ] Testes manuais realizados
- [ ] Performance testado

## Checklist
- [ ] Código segue padrões estabelecidos
- [ ] Documentação atualizada
- [ ] Commits com mensagens claras
- [ ] Não há conflitos de merge
- [ ] Labels aplicadas corretamente

## Screenshots (se aplicável)
[Adicionar screenshots das mudanças visuais]

## Informações Adicionais
[Qualquer informação relevante]
```

### 2. Revisão de Código

#### Responsabilidades do Autor
- **Responder** a todos os comentários
- **Fazer** mudanças solicitadas
- **Explicar** decisões técnicas
- **Manter** o PR atualizado

#### Responsabilidades do Reviewer
- **Revisar** código com atenção
- **Testar** funcionalidades
- **Verificar** documentação
- **Fornecer** feedback construtivo

#### Critérios de Aprovação
- ✅ **Código funcional** e sem bugs
- ✅ **Padrões** de código seguidos
- ✅ **Testes** adequados
- ✅ **Documentação** atualizada
- ✅ **Performance** aceitável

### 3. Processo de Aprovação

#### Política de Aprovação
- **Mínimo 1 aprovação** para PRs pequenos
- **Mínimo 2 aprovações** para PRs complexos
- **Aprovação obrigatória** de tech lead para mudanças críticas
- **Aprovação de stakeholders** para mudanças de negócio

#### Estados do PR
- **Draft**: Em desenvolvimento
- **Ready for review**: Pronto para revisão
- **Changes requested**: Mudanças solicitadas
- **Approved**: Aprovado
- **Merged**: Mesclado

## Templates de Pull Request

### Template para Features
```yaml
name: Feature Request
title: "[FEAT] Descrição da funcionalidade"
labels: ["feat", "planejado"]
assignees: []
body: |
  ## Descrição
  [Descreva a nova funcionalidade]

  ## Justificativa
  [Por que esta funcionalidade é necessária]

  ## Implementação
  [Como foi implementada]

  ## Testes
  - [ ] Testes unitários
  - [ ] Testes de integração
  - [ ] Testes manuais

  ## Documentação
  - [ ] README atualizado
  - [ ] API docs atualizados
  - [ ] Changelog atualizado

  ## Screenshots
  [Se aplicável]
```

### Template para Bug Fixes
```yaml
name: Bug Fix
title: "[FIX] Descrição do bug"
labels: ["fix", "nao_planejado"]
assignees: []
body: |
  ## Problema
  [Descreva o bug encontrado]

  ## Causa
  [O que causou o problema]

  ## Solução
  [Como foi corrigido]

  ## Testes
  - [ ] Bug reproduzido
  - [ ] Correção testada
  - [ ] Regressão testada

  ## Impacto
  [Quem é afetado pela correção]
```

### Template para Documentação
```yaml
name: Documentation
title: "[DOCS] Melhoria na documentação"
labels: ["docs"]
assignees: []
body: |
  ## Área
  [Qual área da documentação]

  ## Mudanças
  [O que foi alterado/adicionado]

  ## Justificativa
  [Por que as mudanças são necessárias]

  ## Revisão
  - [ ] Conteúdo técnico correto
  - [ ] Linguagem clara
  - [ ] Exemplos adequados
```

## Configurações de Proteção

### Branch Protection Rules

#### Para `main`
```yaml
Require pull request reviews before merging: true
Required approving reviews: 2
Dismiss stale pull request approvals when new commits are pushed: true
Require status checks to pass before merging: true
Require branches to be up to date before merging: true
Restrict pushes that create files: true
Require linear history: true
```

#### Para `develop`
```yaml
Require pull request reviews before merging: true
Required approving reviews: 1
Dismiss stale pull request approvals when new commits are pushed: true
Require status checks to pass before merging: true
Require branches to be up to date before merging: true
```

### Status Checks

#### Testes Automatizados
- **Unit Tests**: Todos os testes unitários devem passar
- **Integration Tests**: Testes de integração devem passar
- **Linting**: Código deve seguir padrões de estilo
- **Security Scan**: Verificação de vulnerabilidades

#### Validações
- **Code Coverage**: Cobertura mínima de 80%
- **Documentation**: Documentação deve estar atualizada
- **Dependencies**: Dependências devem estar atualizadas

## Workflow de Revisão

### Processo Detalhado

#### 1. Criação
1. **Desenvolver** na feature branch
2. **Fazer commits** frequentes e organizados
3. **Testar** localmente
4. **Criar PR** com template adequado

#### 2. Revisão Inicial
1. **Self-review**: Autor revisa seu próprio código
2. **Atualizar** branch se necessário
3. **Solicitar** revisão de colegas
4. **Responder** a comentários iniciais

#### 3. Iteração
1. **Fazer** mudanças solicitadas
2. **Adicionar** commits ou fazer amend
3. **Atualizar** PR com novas mudanças
4. **Responder** a novos comentários

#### 4. Aprovação
1. **Receber** aprovações necessárias
2. **Verificar** que todos os checks passam
3. **Resolver** conflitos se houver
4. **Fazer merge** quando aprovado

### Boas Práticas de Revisão

#### Para Reviewers
- ✅ **Revisar** código, não pessoas
- ✅ **Ser específico** nos comentários
- ✅ **Sugerir** melhorias construtivas
- ✅ **Testar** funcionalidades quando possível
- ✅ **Aprovar** apenas quando satisfeito

#### Para Autores
- ✅ **Manter** PRs pequenos e focados
- ✅ **Responder** a todos os comentários
- ✅ **Fazer** mudanças solicitadas
- ✅ **Explicar** decisões técnicas
- ✅ **Manter** PR atualizado

## Automação e Integração

### GitHub Actions

#### Workflow de CI/CD
```yaml
name: Pull Request Checks
on: [pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run tests
        run: npm test
      - name: Run linting
        run: npm run lint
      - name: Check coverage
        run: npm run coverage
```

#### Automação de Labels
```yaml
name: Auto-label PRs
on: [pull_request]
jobs:
  auto-label:
    runs-on: ubuntu-latest
    steps:
      - name: Auto-label based on title
        uses: actions/github-script@v6
        with:
          script: |
            const title = context.payload.pull_request.title;
            if (title.includes('[FEAT]')) {
              github.rest.issues.addLabels({
                issue_number: context.issue.number,
                owner: context.repo.owner,
                repo: context.repo.repo,
                labels: ['feat']
              });
            }
```

### Integração com Ferramentas

#### Code Quality
- **SonarQube**: Análise de qualidade de código
- **CodeClimate**: Métricas de complexidade
- **ESLint**: Linting de JavaScript/TypeScript
- **Prettier**: Formatação de código

#### Security
- **Snyk**: Verificação de vulnerabilidades
- **Dependabot**: Atualizações de dependências
- **CodeQL**: Análise de segurança

## Métricas e Monitoramento

### KPIs de Pull Requests

- **Tempo médio** de revisão
- **Tempo médio** de merge
- **Taxa de aprovação** na primeira revisão
- **Número de comentários** por PR
- **Tamanho médio** dos PRs

### Relatórios

- **Sprint retrospectives** baseadas em PRs
- **Análise** de tendências de qualidade
- **Identificação** de gargalos no processo
- **Métricas** de produtividade da equipe

## Troubleshooting

### Problemas Comuns

#### Conflitos de Merge
```bash
# Resolver conflitos
git checkout feature/minha-feature
git fetch origin
git rebase origin/main
# Resolver conflitos manualmente
git add .
git rebase --continue
git push --force-with-lease
```

#### PR Stuck
- **Verificar** se todos os checks passam
- **Solicitar** revisão de colegas
- **Atualizar** branch com a base
- **Contactar** tech lead se necessário

#### Reviews Demoradas
- **Ping** reviewers após 24h
- **Solicitar** revisão de outros colegas
- **Documentar** urgência se necessário
- **Escalar** para tech lead se crítico

## Próximos Passos

1. **Configurar** templates de PR
2. **Implementar** automação de labels
3. **Configurar** proteções de branch
4. **Treinar** equipe sobre processo
5. **Monitorar** métricas e ajustar 