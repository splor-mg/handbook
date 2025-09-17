---
date: 2025-09-17
authors: [carloshob]
draft: false
comments: true
categories:
  - GitHub
  - Segurança
  - Tokens
  - Secrets
---

# 🔐 Autenticação, Autorização e Tokens JWT no GitHub

Esta postagem intui apresentar os conceitos fundamentais sobre tokens, explorando sua relação com autenticação e autorização, e documentar nossa experiência prática na gestão desses recursos. Abordaremos os diferentes tipos de tokens disponíveis no GitHub, como configurá-los adequadamente, e compartilharemos as práticas que adotamos para gerenciar `Organization Secrets`. 

Por fim, discutiremos os principais desafios enfrentados — incluindo limitações de rate limit (erro 429) — e apresentaremos as estratégias para modernizar nossa gestão de tokens.


<!-- more -->

---

!!! tldr "Contexto SPLOR"
    Dentro da organização [splor-mg](https://github.com/orgs/splor-mg/repositories) mantemos diversos repositórios/pastas — a maioria pública, porém alguns privados com informações sensíveis.

    Atualmente, para operar esse ecossistema e criar algumas rotinas de automação, usamos tokens em várias frentes: integrações externas (para buscar bases no gmail, por exemplo), scripts, pipelines do GitHub Actions, bots e automações internas. 

    Esse é o contexto no qual se insere a nossa gestão de chaves de acesso e tokens.


## 🧭 **Antes de tudo: Autenticação x Autorização**

- **Autenticação**: é o mecanismo de identificar quem você é.
>  - Exemplo: “Eu sou o App X instalado na nossa organização” ou “eu sou o usuário Y autenticado com este token”.

- **Autorização**: define o que você pode fazer depois de identificado ("quais papeis/escopos/permissões você tem?")
>  - Exemplo: “Este token pode ler repositórios privados, mas não pode deletá-los”.

Como os tokens entram nisso? O token é a “prova” apresentada em cada requisição para dizer quem está falando (**autenticação**); e, ao mesmo tempo, esse token também carrega limites de acesso (escopos/permissões) que determinam o que pode ser feito (**autorização**).

---

## 🔑 **Tokens: O que são e por que são importantes**

Os Tokens são utilizados, basicamente, para fazer uma **autenticação automática**, substituindo a etapa de autenticação convencional (login interativo), na qual digitamos manualmente `login` e `senha` do usuário.

Tokens, portanto, são credenciais de acesso usadas por sistemas (e pessoas, às vezes) para chamar a API do GitHub sem precisar de login interativo.

**Por que importam:**

  - Automatizam tarefas (CI/CD, bots, integrações);
  - Permitem controle fino de permissões (mínimo necessário);
  - Aumentam rastreabilidade (quem/qual sistema fez o quê e quando);
  - Facilitam rotação e revogação sem impactar contas de usuários.

**Tipos mais comuns no nosso contexto:**

- GITHUB_TOKEN (Actions): token efêmero gerado por execução do GitHub Actions, com permissões configuráveis por workflow.
- PAT (Personal Access Token): credencial pessoal; hoje existe o modelo Fine-grained (recomendado) com escopo mais restrito.


??? info "Como podemos gerar e encontrar tokens no GitHub"
    **1) GITHUB_TOKEN (gerado automaticamente no GitHub Actions)**

    - Onde aparece: disponível em cada execução de workflow como variável `GITHUB_TOKEN`.
    - Como habilitar/ajustar permissões: no arquivo do workflow (`.github/workflows/*.yml`), defina `permissions:` por job ou no topo do workflow.
    - Escopo e validade: é efêmero (só vale durante a execução). Ideal para operações dentro do próprio repositório, com princípio do menor privilégio.

    !!! hint "Exemplo mínimo no workflow:"
        ```yaml
        permissions:
          contents: write
          issues: read
        ```

    **2) PAT (Personal Access Token) — Fine-grained/classic**

    - Onde gerar, na sua conta pessoal do GitHub vá em `Settings` → `Developer settings` → `Personal access tokens` → `Fine-grained tokens/Tokens(classic)` → `Generate new token`.
    - Como configurar: escolha organização, repositórios e permissões específicas. Preferível o modelo fine-grained (mais restritivo e auditável).
    - Onde ver/gerenciar depois: na mesma tela de `Developer settings` (revogar, regenerar, ajustar escopos/expiração).
    - Uso típico: scripts locais, integrações pontuais que precisam agir “em nome” de um usuário com escopo limitado.

    Boas práticas rápidas:
    - Defina expiração curta e rotacione regularmente.
    - Conceda acesso apenas aos repositórios necessários.
    - Evite usar PAT pessoais em automações críticas de longo prazo


---


## **🔐 Organization secrets** _vs_ **tokens**

**O que são secrets**

Secrets são um **cofre onde armazenamos credenciais sensíveis**, como tokens (PAT, tokens de GitHub App), chaves de API e chaves privadas. São pares chave–valor criptografados mantidos pelo GitHub para uso em automações (principalmente GitHub Actions e Dependabot). 

Eles NÃO são um tipo de token.


**Como encontrar ou cadastrar um `secret`**

- **Organization Secrets**: dentro da organização do GitHub, vá em `Settings` → `Security` → `Secrets and variables` → `Actions` → `New organization secret`. Defina nome, valor e visibilidade (todos os repos ou um subconjunto).
- **Repository Secrets**: vá em `Repo Settings` → `Secrets and variables` → `Actions` → `New repository secret`.
- **Environment Secrets**: vá em `Repo Settings` → `Environments` → selecione o ambiente → `Add secret`.

??? info "Escopos disponíveis"
    - **Organization Secrets**: visíveis para vários repositórios da organização (conforme regras de visibilidade).
    - **Repository Secrets**: visíveis apenas dentro de um repositório específico.
    - **Environment Secrets**: visíveis para um ambiente de um repositório (ex.: `dev`, `stage`, `prod`) com proteções adicionais (aprovação, regras de branch).

??? info "Exemplo: quando cadastrar um secret"
    Cenário: um workflow precisa publicar um pacote em um registro externo (ou acessar uma API de terceiros como Gmail/Sheets/Databricks). Gere a credencial no provedor (ou um PAT fine‑grained/App token no GitHub) e armazene-a como secret.

    **Passos típicos:**

      - 1) Gere o token na origem (ex.: PAT fine‑grained com acesso somente leitura ao repositório `X`).
      - 2) Cadastre o token como `ORGANIZATION_SECRET_X` na organização (ou como secret do repositório/ambiente, se for um caso isolado).
      - 3) No workflow, consuma o secret via `secrets.ORGANIZATION_SECRET_X`.

??? info "Exemplo: uso no arquivo workflow YAML"
    Um workflow do GitHub Actions consome um secret para autenticar em um serviço externo e publicar um pacote:

    ```yaml
    jobs:
      publish:
        permissions:
          contents: read
        steps:
          - name: Login no provedor
            run: |
              tool login --token "${{ secrets.ORGANIZATION_SECRET_X }}"
          - name: Publicar pacote
            run: tool publish
    ```
    
??? warning "Atenção: limitações dos Organization Secrets"
    `Organization Secrets` **não são aplicáveis a repositórios privados**. Se você precisa inserir automações em repositórios privados que dependam de tokens de autenticação/autorização, você deverá salvar o token diretamente como `Repository secrets` dentro do repositório específico.


### **Qual a relação entre secrets e tokens**

- Tokens são as CREDENCIAIS (quem é você e o que pode fazer).
- Secrets são o MEIO SEGURO de armazenar e disponibilizar essas credenciais para automações.

??? hint "Dicas práticas:"
    - **Rotação**: quando você rotaciona um token, deve atualizar o secret correspondente. Prefira nomes estáveis de secret para não quebrar workflows.
    - **Isolamento**: evite usar o MESMO token em dezenas de repositórios via um único Organization Secret; isso concentra risco e consumo. Em casos amplos, prefira GitHub Apps com permissões por instalação.
    - **Princípio do menor privilégio**: crie tokens com escopo mínimo e armazene-os como secrets no menor escopo necessário (environment/repo antes de organization, quando fizer sentido).
    - **Observabilidade**: documente quais workflows usam cada secret para facilitar auditoria e resposta a incidentes.


---


## **🎯  Nossos atuais desafios com tokens e secrets**

Hoje utilizamos principalmente:

- **Organization Secrets** para centralizar credenciais usadas por múltiplos repositórios via Actions.
- **Tokens armazenados** em repositórios privados para integrações pontuais (scripts, jobs específicos).

Benefícios percebidos:

- Centralização facilita reuso e reduz duplicação de credenciais.
- Onboarding mais simples para pipelines padronizados.

**Lacunas e riscos do arranjo atual:**

- **Compartilhamento excessivo**: um mesmo token pode ser usado por vários fluxos diferentes, aumentando impacto em caso de vazamento ou expiração.
- **Escopos amplos demais**: permissões além do necessário elevam superfície de risco.
- **Observabilidade limitada**: difícil rastrear qual fluxo consumiu qual credencial (e em que volume).
- **Rotação irregular**: há tokens com prazos/lógicas de rotação distintos, o que dificulta governança.
- **Acoplamento a pessoas**: uso de PAT pessoais em automações cria dependência de contas individuais.
- **Tratamento de erro heterogêneo**: falhas de credencial (expirada/revogada) e de autorização (permissão insuficiente) se confundem com problemas de infraestrutura.
- **`429 Too Many Requests`**: quando vários fluxos concentram chamadas usando o mesmo token, a cota de uso daquele token se esgota e surgem falhas intermitentes em pipelines/integrações. O 429 é um sintoma de consolidação de tráfego e falta de isolamento entre credenciais, além de ausência de backoff adequado em alguns consumidores.
- **Dificuldade de auditoria**: sem padronização, fica mais difícil responder “quem executou esta ação?” e “por meio de qual credencial?”.
- **Rotação e validade**: tokens sem expiração ou com expiração mal gerida causam paradas silenciosas quando vencem.
- **Permissões desbalanceadas**: overpermission (excesso) ou underpermission (falta) geram erros “Forbidden” ou, pior, riscos desnecessários.


---

## **✅ Práticas modernas para gestão de tokens e automação**

**1. Evitar tokens pessoais (PATs) para automação**

- São difíceis de gerenciar (revogação, rotação, auditoria).
- Se o funcionário sair, o token pode ficar órfão.
- Melhor usar GitHub Apps ou OIDC (OpenID Connect) para obter credenciais temporárias.

**2. Usar GitHub Apps em vez de PATs**

- Um GitHub App instalado na organização/conta tem seu próprio rate limit separado.
- Garante auditoria e segurança, pois os tokens são rotacionados automaticamente e têm escopo reduzido.

**3. Usar provedores de nuvem (AWS, Azure ou GCP)**

Os principais provedores de nuvem oferecem serviços de computação, armazenamento e infraestrutura:

- **AWS (Amazon Web Services)**: plataforma de nuvem da Amazon, líder de mercado com serviços como EC2, S3, Lambda
- **Azure**: plataforma de nuvem da Microsoft, integrada ao ecossistema corporativo Windows/Office
- **GCP (Google Cloud Platform)**: plataforma de nuvem do Google, forte em machine learning e analytics

Todos esses provedores suportam autenticação via OIDC (OpenID Connect):

- O GitHub Actions pode gerar credenciais de nuvem temporárias via OIDC, sem precisar guardar secrets estáticos.
- Exemplo: um workflow obtém credenciais da AWS só durante a execução, eliminando risco de vazamento.

??? info "Evolução dos sistemas de autenticação do GitHub"
    **1ª Geração - Tokens clássicos (2013-2022)**
    
    - PATs com escopos amplos e fixos (ex.: `repo`, `admin:org`)
    - Problema: permissões excessivas, difícil auditoria, rotação manual
    
    **2ª Geração - OAuth Apps (2012-presente)**
    
    - Aplicações terceiras podem solicitar acesso limitado via OAuth
    - Problema: ainda dependente de tokens pessoais, escopo por aplicação
    
    **3ª Geração - Tokens Fine-grained (2022-presente)**
    
    - PATs com escopo granular por repositório específico
    - Melhoria: controle fino de permissões, mas ainda tokens pessoais
    
    **4ª Geração - GitHub Apps (2016-presente)**
    
    - Aplicações com identidade própria, tokens por instalação
    - Vantagem: isolamento total, rotação automática, auditoria nativa, rate limits separados
    
    **5ª Geração - OIDC + Cloud Providers (2021-presente)**
    
    - GitHub Actions gera credenciais temporárias via OpenID Connect
    - Vantagem: zero secrets estáticos, integração nativa com AWS/Azure/GCP


