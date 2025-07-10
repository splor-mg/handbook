---
title: Papéis e Permissões
---

# Papéis e Permissões 🔐

## :material-shield-lock: Estratégia de Segurança

Com o objetivo de promover **um elevado nível de segurança para a [organização SPLOR](https://github.com/splor-mg)** no GitHub, foi pensada uma política clara de papéis e permissões visando garantir o controle adequado sobre os repositórios e recursos da organização. 

!!! warning "Atenção!"
    É oportuno e importante lembrar que, para além dos [**dados sensíveis**](https://splor-mg.github.io/handbook/blog/-publica%C3%A7%C3%A3o-das-bases-da-receita---an%C3%A1lise-sobre-prote%C3%A7%C3%A3o-de-dados/) dos próprios integrantes da equipe SPLOR, como CPF, e-mails pessoais etc., alguns dos conjuntos de dados geridos pela organização contém **informações sensíveis de terceiros, exigindo ainda mais cuidado e responsabilidade** no controle de acessos e permissões, especialmente com a **segurança da nossa própria senha**.  👉 Importante ver [duplo fator de autenticação (2FA)](duplo_fator_autenticacao.md)

## :material-account-tie: Papéis na Organização

### Owners (Proprietários)

**Apenas membros da Assessoria de Inteligência de Dados (AID) serão configurados como "owners"** da organização. Esta restrição é fundamental para:

- **Controle centralizado** das configurações da organização
- **Gestão de segurança** consistente
- **Prevenção de mudanças** não autorizadas
- **Auditoria** adequada das ações administrativas

As responsabilidades dos _owners_ são:

- Configurar políticas de segurança da organização
- Gerenciar times e permissões
- Configurar integrações e webhooks
- Aprovar mudanças críticas
- Gerenciar billing e recursos premium

### Members (Membros)

Todos os demais colaboradores da SPLOR serão configurados como **members** da organização, com permissões específicas baseadas em suas necessidades de trabalho.

!!! Tip "Papeis de quem cria um repositório"
    Quando uma pessoa criar um repositório ("nova pasta") dentro da organização SPLOR, ela será automaticamente considerada como **"owner"** daquele repositório específico. Isso significa que:
     
    - Ela terá controle total sobre o repositório criado
    - Poderá configurar colaboradores e permissões
    - Poderá deletar o repositório (se tiver permissão de admin)
    - Será responsável pela gestão do repositório

!!! Tip "Transferência de ownership (propriedade)"
    Para garantir a continuidade dos projetos e evitar perda de acesso, recomenda-se:
    
    1. **Transferir ownership** para um time da organização quando apropriado
    2. **Documentar** claramente quem é o responsável por cada repositório
    3. **Configurar** proteções de branch para repositórios críticos
    4. **Estabelecer** processos de backup e recuperação

## :material-key: Diferentes Níveis de Permissão

No GitHub, existem diferentes níveis de permissão e papéis que variam conforme o contexto em que você está atuando: no nível da **organização, do repositório ou do time** (equipe). Cada um desses níveis define o que cada pessoa pode visualizar, modificar ou administrar, garantindo segurança e flexibilidade na colaboração. Compreender essas diferenças é fundamental para manter o controle adequado dos acessos e das responsabilidades dentro dos projetos.

!!! tip "Níveis de permissão no GitHub"

    | Nível | Papel | Descrição |
    |-------|-------|-----------|
    | **Organizacional** | Owner | Apenas membros da AID |
    | | Member | Todos os colaboradores SPLOR |
    | **Repositório** | Admin | Controle total do repositório |
    | | Maintain | Pode gerenciar issues, pull requests e releases |
    | | Write | Pode fazer push de código e criar branches |
    | | Read | Pode visualizar e clonar o repositório |
    | **Time** | Member | Membro do time |
    | | Maintainer | Pode gerenciar membros do time |

## :material-security: Políticas de Segurança

### Proteção de Branches

- **main/master**: Sempre protegida
- Requer **pull request** para mudanças
- Requer **code review** de pelo menos um maintainer
- Requer **status checks** para passar

### Deleção de Repositórios

- **Apenas owners** podem deletar repositórios da organização
- Membros individuais podem deletar apenas repositórios que criaram
- Recomenda-se **confirmação adicional** para repositórios críticos

### Merge de Pull Requests

- **Apenas owners e maintainers** podem fazer merge
- Requer **aprovação** de pelo menos um reviewer
- **Status checks** devem passar antes do merge

## :material-table: Matriz de Responsabilidades

| Ação | Owner | Member | Repository Owner |
|------|-------|--------|------------------|
| Criar repositório | ✅ | ✅ | ✅ |
| Deletar repositório | ✅ | ❌ | ✅ (próprio) |
| Configurar proteções | ✅ | ❌ | ✅ |
| Gerenciar times | ✅ | ❌ | ❌ |
| Fazer merge em main | ✅ | ❌ | ✅ |
| Aprovar PRs | ✅ | ✅ (se maintainer) | ✅ |

## 🚀 Processo de Onboarding

### Para Novos Colaboradores

1. **Criar conta** no GitHub
2. **Solicitar acesso** à organização SPLOR
3. **Ser adicionado** ao time correspondente
4. **Receber treinamento** sobre políticas de segurança
5. **Configurar 2FA** (obrigatório)

### Para Novos Repositórios

1. **Criar repositório** com nome padronizado
2. **Configurar proteções** de branch
3. **Adicionar colaboradores** apropriados
4. **Configurar labels** e templates
5. **Documentar** no handbook

