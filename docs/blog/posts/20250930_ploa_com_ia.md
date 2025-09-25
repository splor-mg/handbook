---
date: 2025-09-30
authors: [carloshob]
draft: false
comments: true
categories:
  - LOA
  - Docker
  - IA no Orçamento
---

# Utilizando a Inteligência Artificial integrada para auxiliar na elaboração dos volumes da LOA

## **Contexto e Desafios**

A geração dos volumes da LOA depende de um ecossistema complexo de ferramentas, pacotes internos e estruturas de teste, cujas versões e dependências evoluem continuamente, gerando potenciais conflitos e quebras de compatibilidade.

**Principais desafios:**
- **Dependências transitivas**: mudanças em pacotes base afetam toda a cadeia
- **Versionamento heterogêneo**: diferentes ferramentas com ciclos de release distintos
- **Ambiente de desenvolvimento**: inconsistências entre máquinas de desenvolvimento
- **Reprodutibilidade**: garantir resultados idênticos em diferentes ambientes

## **Solução Implementada: Containerização**

Para contornar essa complexidade, a SPLOR implementou uma estratégia de **containerização** usando Docker:

- **Imagens Docker**: capturam o estado exato do ambiente de execução
- **Versionamento de ambiente**: cada imagem contém versões específicas de todas as dependências
- **Reprodutibilidade garantida**: mesmo ambiente em qualquer máquina


**Componentes:**
- **`volumes-docker`**: repositório responsável por construir e manter as imagens Docker
- **Docker Hub**: registro público onde as imagens são publicadas e versionadas
- **`volumes-loa`**: repositório que consome as imagens para gerar os volumes

??? info "Docker Hub - Registro de Imagens"
    O [Docker Hub](https://hub.docker.com/) é o maior registro público de imagens Docker, funcionando como um "repositório de repositórios" para containers. É onde publicamos nossas imagens para consumo pelos repositórios de produção.



## **🔍 Validação do Ambiente para Início da PLOA**

### **Objetivo da Validação**

Antes de iniciar os protocolos de elaboração da PLOA, é essencial validar que o ambiente de execução está funcionando corretamente. Esta validação garante que:

- ✅ A imagem Docker está sendo publicada corretamente
- ✅ O repositório `volumes-loa` consegue gerar volumes idênticos aos da versão anterior
- ✅ Todas as dependências estão funcionando como esperado

### **Estratégias de Validação**

Existem pelo menos três abordagens para reconstruir e validar a geração dos volumes da LOA do ano anterior:

#### **1. 🟢 Validação Simples (Recomendada para início)**

**Configuração:**
- **Imagem Docker**: mesma do ano anterior
- **Pacotes internos**: mesmas versões do ano anterior 
- **Bases de dados**: bases versionadas após última LOA (versão corrente, sem rodar `dpm install`)

**Critério de aprovação:**
- Conseguir gerar todos os volumes da LOA
- Os volumes gerados na pasta `pdf/` devem ser **iguais** aos versionados no término da elaboração do projeto de lei orçamentária
- Validação via `git status` - nenhuma mudança detectada

**Vantagens:**
- ✅ Validação rápida e direta
- ✅ Garante reprodutibilidade completa
- ✅ Ideal para verificação inicial

#### **2. 🟡 Validação Avançada**

**Configuração:**
- **Imagem Docker**: mesma do ano anterior
- **Pacotes internos**: mesmas versões dos anos anteriores
- **Bases de dados**: bases já versionadas após última LOA (versão corrente, sem rodar `dpm install`)

**Critério de aprovação:**
- Conseguir gerar todos os volumes da LOA
- Os volumes devem passar no teste `make check`
- Validação via golden tests construídos no repositório `volumes-loa`

**Vantagens:**
- ✅ Testes automatizados mais robustos
- ✅ Permite detecção de problemas sutis, validação de
- ✅ Validação de lógica de negócio


#### **3. 🔵 Teste Exploratório (investigação de compatibilidade)**

**Configuração:**
- **Imagem Docker**: gerar nova imagem docker, com versões mais recentes das ferramentas
- **Pacotes internos**: versões mais recentes, ou aquela fixada para o projeto de lei orçamentária em curso
- **Bases de dados**: base de dados do ano anterior mediande 

**Uso:**
- Investigação de problemas de compatibilidade
- Teste de novas versões de dependências
- Desenvolvimento de soluções para issues específicos

