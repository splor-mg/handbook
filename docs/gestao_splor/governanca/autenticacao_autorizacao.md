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

# 🔐 GitHub APP - Autenticação, Autorização e Tokens JWT

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

## 🔑 **Tokens**

O que são e por que são importantes?

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


## **🔐 Secrets** _vs_ **tokens**

**O que são os organization secrets**

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


## **🎯  Desafios**

Desde o início da criação da organização `splor-mg` no GitHub utilizamos principalmente:

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

## **✅ Práticas modernas**

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


---


## 🚀 Implementando GitHub App


Agora que entendemos os conceitos e desafios, vamos implementar uma solução moderna usando **GitHub Apps**. Esta abordagem resolve os principais problemas identificados: isolamento de credenciais, rotação automática, auditoria nativa e rate limits separados.

**Por que GitHub App?**

- **Identidade própria**: o App tem sua própria identidade, independente de usuários
- **Rate limits separados**: cada App tem sua própria cota de API, evitando conflitos
- **Rotação automática**: tokens são gerados sob demanda e expiram automaticamente
- **Auditoria nativa**: todas as ações são rastreadas como "GitHub App X"
- **Permissões granulares**: controle fino sobre o que o App pode fazer

---

**Passo a passo: Criando um GitHub App**

**1. Criar o GitHub App na organização**

1. **Acesse as configurações da organização**:
   - Vá para `https://github.com/orgs/SUA_ORGANIZACAO/settings`
   - Clique em **Developer settings** → **GitHub Apps**

2. **Criar novo App**:
   - Clique em **New GitHub App**
   - Preencha os campos obrigatórios:
     - **GitHub App name**: `meu-app-autenticacao` (nome único)
     - **Homepage URL**: URL do seu repositório ou documentação
     - **Webhook**: Deixe desabilitado para começar
     - **Description**: "App para autenticação e automação"

3. **Configurar permissões**:
   ```
   Repository permissions:
   - Contents: Read (para ler arquivos)
   - Issues: Write (para gerenciar issues)
   - Metadata: Read (informações básicas)
   - Pull requests: Read (se necessário)
   
   Organization permissions:
   - Members: Read (se precisar listar membros)
   ```

4. **Configurar eventos** (opcional):
   - Marque apenas os eventos que seu App realmente precisa
   - Exemplo: `Issues`, `Repository` se for monitorar mudanças

5. **Salvar e instalar**:
   - Clique em **Create GitHub App**
   - Na página do App, clique em **Install App**
   - Selecione a organização e configure as permissões

**2. Obter as credenciais necessárias**

Após criar o App, você precisará de três informações:

1. **App ID** (ID numérico):
   - Na página do App → **General**
   - Copie o **App ID** (exemplo: `123456`)

2. **Installation ID** (ID da instalação):
   - Na página do App → **Install App** → **Installations**
   - Clique na instalação da sua organização
   - O ID aparece na URL: `.../installations/789012`

3. **Private Key** (chave privada):
   - Na página do App → **General** → **Private keys**
   - Clique em **Generate a private key**
   - **IMPORTANTE**: Baixe o arquivo `.pem` imediatamente
   - Esta chave só é mostrada uma vez!

??? warning "⚠️ Segurança da chave privada"
    A chave privada é **extremamente sensível**. Trate-a como uma senha mestra:
    - Nunca commite no Git
    - Armazene em secrets do GitHub
    - Use apenas em ambientes seguros
    - Rotacione periodicamente

---

**Implementação: Script de Autenticação**

Agora vamos implementar o código que usa essas credenciais para obter tokens temporários. Vamos analisar um exemplo prático baseado no script `github_app_auth.py`:

**Estrutura básica do script**

```python
#!/usr/bin/env python3
"""
Helper para autenticação via GitHub App.
Gera JWT assinado com a chave privada do App e troca por um
installation access token, que é o token usado nas chamadas à API.
"""

import base64
import json
import os
import time
from pathlib import Path
import jwt  # PyJWT
import requests

GITHUB_API_URL = "https://api.github.com"
```

**1. Lendo a chave privada**

```python
def _read_private_key_from_env_or_path() -> str:
    """
    Lê a chave privada do GitHub App.
    Prioridade:
      1. GITHUB_APP_PRIVATE_KEY (conteúdo PEM bruto ou base64)
      2. GITHUB_APP_PRIVATE_KEY_PATH (caminho para arquivo .pem)
    """
    # Tentar ler da variável de ambiente primeiro
    key_inline = os.getenv("GITHUB_APP_PRIVATE_KEY")
    if key_inline:
        # Permitir que venha em base64 (útil para secrets)
        stripped = key_inline.strip()
        if "BEGIN" in stripped:
            return stripped  # Já está em formato PEM
        try:
            return base64.b64decode(stripped).decode("utf-8")
        except Exception:
            return stripped  # Usar como está
    
    # Fallback: ler de arquivo
    key_path = os.getenv("GITHUB_APP_PRIVATE_KEY_PATH")
    if not key_path:
        raise RuntimeError("Missing GITHUB_APP_PRIVATE_KEY or GITHUB_APP_PRIVATE_KEY_PATH")
    
    path = Path(key_path).expanduser()
    if not path.exists():
        raise RuntimeError(f"Private key file not found: {path}")
    
    return path.read_text(encoding="utf-8")
```

??? info "💡 Por que duas formas de ler a chave?"
    - **Variável de ambiente**: ideal para GitHub Actions (secrets)
    - **Arquivo**: útil para desenvolvimento local
    - **Base64**: permite armazenar a chave em secrets do GitHub sem quebras de linha

**2. Criando o JWT (JSON Web Token)**

```python
def _create_app_jwt(app_id: str, private_key_pem: str) -> str:
    """
    Cria um JWT RS256 com expiração curta (60s) para o GitHub App.
    """
    now = int(time.time())
    payload = {
        "iat": now - 5,  # pequena folga de clock skew
        "exp": now + 55,  # expira em 55 segundos
        "iss": app_id,    # ID do App (issuer)
    }
    
    # Assinar com a chave privada usando algoritmo RS256
    token = jwt.encode(payload, private_key_pem, algorithm="RS256")
    return token
```

??? info "🔍 Entendendo o JWT"
    O JWT é como um "bilhete de identidade" temporário que prova que você é o GitHub App:
    - **iat** (issued at): quando foi criado
    - **exp** (expires): quando expira (curto, por segurança)
    - **iss** (issuer): quem emitiu (ID do seu App)
    - **Assinatura**: prova que foi criado com sua chave privada

**3. Trocando JWT por token de instalação**

```python
def _create_installation_token(app_jwt: str, installation_id: str) -> str:
    """
    Troca o JWT do App por um installation access token.
    """
    url = f"{GITHUB_API_URL}/app/installations/{installation_id}/access_tokens"
    headers = {
        "Authorization": f"Bearer {app_jwt}",
        "Accept": "application/vnd.github+json",
    }
    
    resp = requests.post(url, headers=headers)
    if resp.status_code not in (200, 201):
        raise RuntimeError(
            f"Failed to create installation token ({resp.status_code}): {resp.text}"
        )
    
    data = resp.json()
    return data["token"]  # Este é o token que usaremos nas chamadas da API
```

**4. Função principal (orquestrando tudo)**

```python
def get_github_app_installation_token() -> str:
    """
    Obtém um installation token usando variáveis de ambiente:
      - GITHUB_APP_ID
      - GITHUB_APP_INSTALLATION_ID  
      - GITHUB_APP_PRIVATE_KEY ou GITHUB_APP_PRIVATE_KEY_PATH
    """
    # 1. Ler credenciais das variáveis de ambiente
    app_id = os.getenv("GITHUB_APP_ID")
    installation_id = os.getenv("GITHUB_APP_INSTALLATION_ID")
    
    if not app_id or not installation_id:
        raise RuntimeError("Missing GITHUB_APP_ID or GITHUB_APP_INSTALLATION_ID")
    
    # 2. Ler a chave privada
    private_key_pem = _read_private_key_from_env_or_path()
    
    # 3. Criar JWT com a chave privada
    app_jwt = _create_app_jwt(app_id, private_key_pem)
    
    # 4. Trocar JWT por token de instalação
    return _create_installation_token(app_jwt, installation_id)
```

---

**⚙️ Configuração do ambiente**

**Para desenvolvimento local**

Crie um arquivo `.env` na raiz do seu projeto:

```bash
# GitHub App credentials
GITHUB_APP_ID=123456
GITHUB_APP_INSTALLATION_ID=789012
GITHUB_APP_PRIVATE_KEY_PATH=/caminho/para/sua/chave.pem
```

**Para GitHub Actions**

Configure os secrets no repositório:

1. **Repository Secrets**:
   - `GH_APP_ID`
   - `GH_APP_INSTALLATION_ID`  
   - `GH_APP_PRIVATE_KEY`: conteúdo da chave privada (formato PEM)

2. **No workflow**:
```yaml
- name: Generate GitHub App token
  id: app-token
  uses: actions/create-github-app-token@v2
  with:
    app-id: ${{ secrets.GH_APP_ID }}
    private-key: ${{ secrets.GH_APP_PRIVATE_KEY }}
    owner: ${{ github.repository_owner }}

- name: Use the token
  run: |
    # Seu script aqui
  env:
    GITHUB_TOKEN: ${{ steps.app-token.outputs.token }}
```

---

**🚀 Exemplo prático: Usando o token**

```python
import requests
from github_app_auth import get_github_app_installation_token

def list_repositories():
    """Lista repositórios da organização usando GitHub App"""
    
    # Obter token via GitHub App
    token = get_github_app_installation_token()
    
    # Usar o token nas chamadas da API
    headers = {
        'Authorization': f'token {token}',
        'Accept': 'application/vnd.github.v3+json'
    }
    
    # Exemplo: listar repositórios
    response = requests.get(
        'https://api.github.com/orgs/sua-organizacao/repos',
        headers=headers
    )
    
    if response.status_code == 200:
        repos = response.json()
        print(f"Encontrados {len(repos)} repositórios")
        return repos
    else:
        print(f"Erro: {response.status_code} - {response.text}")
        return []

# Usar a função
repos = list_repositories()
```

---

**✅ Vantagens desta abordagem**

1. **Segurança**: tokens temporários, chave privada nunca exposta
2. **Isolamento**: rate limits separados, sem conflitos
3. **Auditoria**: todas as ações são rastreadas como "GitHub App X"
4. **Flexibilidade**: permissões configuráveis por instalação
5. **Manutenção**: rotação automática, sem intervenção manual


---

**🏢 Desafio organizacional: Coordenação da migração**

Em uma organização com múltiplos setores, o maior desafio não é técnico, mas **coordenativo**. Cada unidade pode vir a desenvolver suas próprias automações usando tokens (PATs, GITHUB_TOKEN) ao longo do tempo, criando um cenário fragmentado e difícil de gerenciar.

**O desafio real**

- **Inventário completo**: identificar todos os repositórios que utilizam tokens
- **Mapeamento de dependências**: entender quais workflows dependem de cada token
- **Coordenação entre setores**: alinhar diferentes equipes para uma migração coordenada
- **Planejamento de impacto**: minimizar interrupções durante a transição
- **Capacitação**: treinar equipes nos novos procedimentos

**Estratégia de migração organizacional**

1. **Auditoria completa**: varrer todos os repositórios passados que utilizam tokens
2. **Priorização por criticidade**: começar pelos processos mais importantes
3. **Comunicação centralizada**: manter todas as unidades informadas sobre o progresso
4. **Suporte técnico**: oferecer assistência durante a migração
5. **Monitoramento contínuo**: acompanhar a adoção e identificar resistências

---

**🔍 Reflexão: Protocolo de monitoramento**

Uma questão fundamental surge: **será necessário criar protocolos organizacionais para verificar se PATs (Personal Access Tokens) estão sendo utilizados?**

Para organizações de médio a grande porte, uma leitura inicial da documentação sobre o tema indica que **sim, é recomendável** estabelecer protocolos de monitoramento. Isso garante:

- **Controle centralizado** sobre credenciais
- **Segurança aprimorada** com rotação automática
- **Visibilidade** sobre uso de recursos
- **Padronização** de práticas de automação

A migração para GitHub Apps não é apenas uma modernização técnica, mas uma **evolução na governança de segurança** que beneficia toda a organização.