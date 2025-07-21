---
title: Instalação e Configuração
---

# Instalação e Configuração

Vamos instalar o Git no seu computador!
O processo é simples e rápido.
Escolha o seu sistema operacional abaixo:

## :material-microsoft-windows: Windows

### Opção 1: Git for Windows (Recomendado)
1. Acesse [git-scm.com](https://git-scm.com/download/win).
2. Baixe o instalador (será detectado automaticamente).
3. Execute o arquivo `.exe` baixado.
4. **Importante**: Durante a instalação, mantenha as opções padrão.
5. Clique em "Next" até finalizar.

### Opção 2: Via Chocolatey (para desenvolvedores)
```bash
choco install git
```

### Opção 3: Via Winget
```bash
winget install --id Git.Git -e --source winget
```

## :simple-macos: macOS

### Opção 1: Via Homebrew (Recomendado)
```bash
brew install git
```

### Opção 2: Via Xcode Command Line Tools
```bash
xcode-select --install
```

### Opção 3: Download direto
1. Acesse [git-scm.com](https://git-scm.com/download/mac)
2. Baixe e instale o pacote

## :simple-linux: Linux

### Ubuntu/Debian
```bash
sudo apt update
sudo apt install git
```

### Fedora
```bash
sudo dnf install git
```

### CentOS/RHEL
```bash
sudo yum install git
```

### Arch Linux
```bash
sudo pacman -S git
```

## ✅ Verificando a Instalação

Após instalar, abra o terminal (ou Prompt de Comando no Windows) e digite:

```bash
git --version
```

Você deve ver algo como: `git version 2.39.0`

## ⚙️ Configuração Inicial

Agora vamos configurar suas credenciais:

```bash
git config --global user.name <Seu Nome Completo>
git config --global user.email <seu_email_github@email.com>
```

### Configurações Recomendadas para SPLOR

```bash
# Editor padrão (escolha um que você conheça)
git config --global core.editor "code --wait"  # VS Code
# ou
git config --global core.editor "notepad"      # Bloco de Notas (Windows)

# Configurar branch padrão
git config --global init.defaultBranch main

# Configurar autenticação HTTPS
git config --global credential.helper store
```

## 🔐 Configurando Autenticação

### Para GitHub (Recomendado)
1. Acesse [github.com](https://github.com)
2. Faça login na sua conta
3. Vá em Settings > Developer settings > Personal access tokens
4. Gere um novo token com permissões de `repo`
5. Use esse token como senha quando solicitado

### Alternativa: SSH Keys
```bash
# Gerar chave SSH
ssh-keygen -t ed25519 -C "seu_email_github@email.com"

# Adicionar à conta GitHub
# Copie o conteúdo de ~/.ssh/id_ed25519.pub
# Cole em GitHub > Settings > SSH and GPG keys
```

## 🎯 Próximos Passos

Agora que o Git está instalado e configurado, você pode:

1. **Criar seu primeiro repositório**: `git init`
2. **Clonar um repositório existente**: `git clone <endereço_ssh>`
3. **Adicionar suas alterações**:`git add .`
4. **Fazer seu primeiro commit**: `git commit -m "Primeiro commit"`

## 🆘 Precisa de Ajuda?

- **Documentação oficial**: [git-scm.com/doc](https://git-scm.com/doc)
- **GitHub Guides**: [guides.github.com](https://guides.github.com)
- **Colegas da SPLOR**: Não hesite em pedir ajuda!

---

**Dica**: Se você nunca usou linha de comando, não se preocupe!
O Git também funciona com interfaces gráficas como GitHub Desktop, GitKraken ou integração com editores como VS Code.
