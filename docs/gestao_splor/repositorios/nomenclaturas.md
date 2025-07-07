---
title: Nomenclaturas
---

# Nomenclaturas 📁

## O que é um Repositório?

Um **repositório** (ou "repo") é o local onde armazenamos e gerenciamos o código fonte, documentação e outros arquivos relacionados a um projeto. É como uma "pasta" digital que contém todo o histórico de mudanças e permite que múltiplas pessoas trabalhem colaborativamente.

### Conceitos Básicos

- **Cada pasta representa um projeto** específico
- **Contém todo o histórico** de mudanças (commits)
- **Permite colaboração** entre múltiplos desenvolvedores
- **Mantém controle de versão** do código
- **Facilita o backup** e recuperação de dados

### Para Aprender Mais

Recomendamos fortemente consultar a **trilha dev** da SPLOR, especialmente a aula que explica detalhadamente o que são repositórios e como funcionam. Esta aula fornece uma base sólida para entender os conceitos fundamentais do Git e GitHub.

## Padrões de Nomenclatura

### Estrutura Geral

```
[organizacao]-[tipo]-[nome-projeto]
```

### Exemplos de Nomenclatura

#### Repositórios de Dados
- `splor-mg-dados-volumes-loa`
- `splor-mg-dados-orcamentarios`
- `splor-mg-dados-abertos`

#### Repositórios de Documentação
- `splor-mg-docs-handbook`
- `splor-mg-docs-politicas`
- `splor-mg-docs-procedimentos`

#### Repositórios de Sistemas
- `splor-mg-sistema-gestao-orcamentaria`
- `splor-mg-sistema-dados-abertos`
- `splor-mg-sistema-relatorios`

#### Repositórios de Automações
- `splor-mg-automacao-etl-dados`
- `splor-mg-automacao-relatorios`
- `splor-mg-automacao-dashboard`

## Regras de Nomenclatura

### 1. Prefixo da Organização
- **Sempre** começar com `splor-mg-`
- Identifica claramente que pertence à SPLOR
- Facilita a busca e organização

### 2. Tipo de Conteúdo
- **dados**: Para repositórios de dados e datasets
- **docs**: Para documentação e manuais
- **sistema**: Para aplicações e sistemas
- **automacao**: Para scripts e automações
- **api**: Para APIs e serviços
- **web**: Para aplicações web

### 3. Nome do Projeto
- **kebab-case**: palavras separadas por hífen
- **descritivo**: deve indicar claramente o propósito
- **conciso**: evitar nomes muito longos
- **sem acentos**: usar apenas caracteres ASCII

### 4. Sufixos Opcionais
- **-api**: para APIs específicas
- **-web**: para interfaces web
- **-mobile**: para aplicações mobile
- **-backend**: para backends específicos
- **-frontend**: para frontends específicos

## Exemplos por Categoria

### Dados e Analytics
```
splor-mg-dados-volumes-loa
splor-mg-dados-orcamentarios
splor-mg-dados-abertos
splor-mg-dados-indicadores
splor-mg-dados-metabase
```

### Documentação
```
splor-mg-docs-handbook
splor-mg-docs-politicas
splor-mg-docs-procedimentos
splor-mg-docs-treinamentos
splor-mg-docs-arquitetura
```

### Sistemas e Aplicações
```
splor-mg-sistema-gestao-orcamentaria
splor-mg-sistema-dados-abertos
splor-mg-sistema-relatorios
splor-mg-sistema-dashboard
splor-mg-sistema-api
```

### Automações e Scripts
```
splor-mg-automacao-etl-dados
splor-mg-automacao-relatorios
splor-mg-automacao-backup
splor-mg-automacao-deploy
splor-mg-automacao-monitoramento
```

## Validação de Nomes

### Checklist para Novos Repositórios

- ✅ [ ] Começa com `splor-mg-`
- ✅ [ ] Usa kebab-case (hífens)
- ✅ [ ] É descritivo e claro
- ✅ [ ] Não tem acentos ou caracteres especiais
- ✅ [ ] Não é muito longo (máximo 50 caracteres)
- ✅ [ ] Segue o padrão de tipo de conteúdo
- ✅ [ ] É único na organização

### Exemplos de Nomes Incorretos

```
❌ splor-mg/volumes_loa (usando underscore)
❌ splor-mg/VolumesLOA (camelCase)
❌ splor-mg/volumes-loa (sem prefixo)
❌ splor-mg-dados-volumes-lei-orcamentaria-anual (muito longo)
❌ splor-mg-dados-volumes-loa-2024 (com ano específico)
```

## Migração de Repositórios Existentes

### Processo de Renomeação

1. **Identificar** repositórios que não seguem o padrão
2. **Propor** novo nome seguindo as regras
3. **Renomear** o repositório no GitHub
4. **Atualizar** links e referências
5. **Notificar** a equipe sobre a mudança

### Repositórios Prioritários

- Repositórios com nomes confusos
- Repositórios sem prefixo da organização
- Repositórios com nomenclatura inconsistente

## Ferramentas de Validação

### GitHub Actions

Podemos configurar uma GitHub Action para validar automaticamente se novos repositórios seguem o padrão de nomenclatura.

### Scripts de Validação

Scripts podem ser criados para:
- Verificar se o nome segue o padrão
- Sugerir nomes alternativos
- Gerar relatórios de conformidade

## Documentação e Treinamento

### Para Novos Membros

- **Orientação** sobre padrões de nomenclatura
- **Exemplos** práticos de uso
- **Validação** antes da criação

### Para Administradores

- **Checklist** de validação
- **Processo** de renomeação
- **Ferramentas** de automação

## Próximos Passos

1. **Revisar** repositórios existentes
2. **Identificar** inconsistências
3. **Criar** plano de migração
4. **Implementar** validação automática
5. **Treinar** equipe sobre padrões 