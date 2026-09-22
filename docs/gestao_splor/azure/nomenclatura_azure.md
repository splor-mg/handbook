---
title: Nomenclatura Azure
tags:
  - azure
  - infraestrutura
---

# Nomenclatura de Recursos Azure ☁️

## Contexto

A AID (Assessoria de Inteligência de Dados) provisiona a infraestrutura da SPLOR na Azure (subscription `SEPLAGMG-SPLOR`): servidores, backup e modelos/agentes no Azure AI Foundry.

Esta página documenta a convenção de nomenclatura efetivamente implementada, baseada no [Cloud Adoption Framework (CAF)](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming) da Microsoft, adaptada ao nosso contexto. Toda a infraestrutura é declarada como código (Bicep + Deployment Stacks) no repositório [`splor-mg/azure-migration`](https://github.com/splor-mg/azure-migration), que é a fonte de verdade — esta página é um resumo para consulta rápida.

!!! warning "Por que definir antes de criar?"

    Resource groups **não podem ser renomeados** depois de criados - a única alternativa é recriar e migrar os recursos. O custo de errar a nomenclatura no início é alto.

!!! note "Recursos movidos mantêm nome legado"

    Recursos que vieram da subscription antiga via `az resource move` mantêm o nome com que nasceram lá (ex.: o Public IP `aid-ip`), em vez de serem renomeados para o padrão CAF. Só recursos criados do zero na SPLOR seguem a convenção abaixo à risca.

## Convenção Geral

```
{abreviacao-tipo}-aid-{workload-ou-papel}-{ambiente}[-{regiao}][-{nn}]
```

| Componente | Descrição | Exemplos |
|---|---|---|
| `abreviacao-tipo` | Prefixo abreviado do tipo de recurso, conforme as [abreviações do CAF](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations) | `rg`, `vm`, `vnet`, `nsg` |
| `aid` | Identificador da área (Assessoria de Inteligência de Dados) | `aid` |
| `workload-ou-papel` | A carga de trabalho (RG, app) ou o papel arquitetural (VM, NIC) | `runtime`, `llm`, `network`, `shared`, `backup` |
| `ambiente` | Ambiente de execução | `prd`, `dev`, `lab` |
| `regiao` | Só onde aplicável (VNet, Cognitive Services) | `brs`, `eus2`, `swc` |
| `nn` | Só quando há múltiplas instâncias do mesmo papel | `01`, `02` |

## Critério de Separação dos Resource Groups

Recursos que compartilham **ciclo de vida** ficam no mesmo resource group. O RG é a unidade de:

1. **Deleção em massa** - se faz sentido apagar tudo junto, fica junto
2. **RBAC (role-based access control)** - Permissões atribuídas no escopo do RG, não recurso a recurso
3. **Custo** - cada RG vira um filtro pronto no Cost Management

Aqui a separação é por **camada arquitetural** (rede, identidade/segredos, modelos LLM, runtime de cada ambiente, backup), não por caso de uso — um caso de uso específico (ex.: análise de pleitos) não ganha RG próprio, só um deployment de modelo ou uma tag `projeto`.

## Resource Groups

| Resource group | Conteúdo |
|---|---|
| `rg-aid-network-prd` / `rg-aid-network-nonprd` | VNets, subnets, NSGs |
| `rg-aid-shared-prd` | Key Vault, Log Analytics Workspace, identidades gerenciadas |
| `rg-aid-llm-prd` | Contas AI Foundry (Cognitive Services) e deployments de modelo |
| `rg-aid-runtime-prd` | VM de produção (host de containers Easypanel) |
| `rg-aid-runtime-dev` | VM de bancada de testes manual (não é espelho de prd — ver nota abaixo) |
| `rg-aid-runtime-lab` | VMs de laboratório/experimentação, compartilhadas entre equipes |
| `rg-aid-backup-prd` | Recovery Services Vault e políticas de backup |

## Nomenclatura por Recurso

| Tipo de recurso | Padrão | Exemplo |
|---|---|---|
| Resource Group | `rg-aid-{workload}-{amb}` | `rg-aid-runtime-prd`, `rg-aid-llm-prd` |
| Virtual Machine | `vm-aid-{papel}-{amb}[-{nn}]` | `vm-aid-runtime-prd`, `vm-aid-runtime-dev` |
| Virtual Network | `vnet-aid-{amb}-{regiao}` | `vnet-aid-prd-brs`, `vnet-aid-nonprd-brs` |
| Subnet | `snet-aid-{finalidade}[-{amb}]` | `snet-aid-runtime`, `snet-aid-runtime-dev` |
| Network Security Group | `nsg-aid-{papel}-{amb}` | `nsg-aid-runtime-prd` |
| Public IP | `pip-aid-{papel}-{amb}` | `pip-aid-runtime-prd` |
| Network Interface | `nic-aid-{papel}-{amb}-{nn}` | `nic-aid-runtime-prd-01` |
| Managed Disk (OS) | `disk-aid-{papel}-{amb}-os` | `disk-aid-runtime-prd-os` |
| SSH Public Key | `sshkey-aid-{papel}-{amb}` | `sshkey-aid-runtime-prd` |
| Recovery Services Vault | `rsv-aid-{amb}` | `rsv-aid-prd` |
| Key Vault | `kv-aid-{amb}` | `kv-aid-prd` |
| Log Analytics Workspace | `log-aid-{amb}` | `log-aid-prd` |
| User Assigned Identity | `id-aid-{workload}-{amb}` | `id-aid-runtime-prd`, `id-aid-llm-prd` |
| Cognitive Services (AI Foundry) | `cog-aid-{finalidade}-{amb}-{regiao}` | `cog-aid-foundry-prd-eus2` |
| Storage Account | `staid{workload}{amb}{regiao}` | `staidlogsprdbrs` (ver [regra de storage](#regra-especial-storage-accounts)) |

### AI Foundry — modelo de contas por região, não Hub/Project

Diferente de um modelo baseado em Hub/Project do Foundry, aqui a arquitetura é **contas Cognitive Services por região**, com deployments de modelo diretamente na conta:

| Conta | Região | Papel |
|---|---|---|
| `cog-aid-foundry-prd-eus2` | eastus2 | Primária — todo tráfego roteia pra cá por padrão |
| `cog-aid-foundry-prd-swc` | swedencentral | Secundária (HA) — deployments idênticos, ativa em incidente da primária |

Deployments seguem `{modelo}-{purpose}` (ex.: `gpt-5-default`, `gpt-5.5-analise-pleitos`). `default` é o purpose do deployment de uso geral; um purpose novo só se justifica por um caso de uso real, nunca "criar por criar".

### Papéis válidos de VM (campo `{papel}`)

VMs nomeadas pelo **papel arquitetural**, não pelo conteúdo. O conteúdo muda; o papel não.

| Papel | Significado |
|---|---|
| `runtime` | Host de containers multi-serviço (Docker / Easypanel hospedando vários apps) |
| `app` | VM dedicada a uma aplicação única |
| `worker` | Processamento batch / jobs assíncronos |
| `db` | Servidor de banco de dados standalone |
| `gpu` | Carga de ML/LLM com GPU |
| `bastion` | Jump host para acesso administrativo |

!!! note "`vm-aid-runtime-dev` não é ambiente de desenvolvimento no sentido comum"

    Apesar do sufixo `dev`, essa VM não sincroniza automaticamente com a `prd`. É uma bancada de testes manual: quem for usar instala e configura item por item, sem nunca importar o banco de dados da prd em massa (evita reativar automações reais de produção por engano). Detalhes na [ADR-024 do repositório de migração](https://github.com/splor-mg/azure-migration/blob/main/docs/05-decisoes-tomadas.md).

## Sufixos de ambiente

| Sufixo | Uso |
|---|---|
| `prd` | Produção — recursos com SLA, dados reais, integrações com sistemas em produção |
| `dev` | Bancada de testes — validação manual antes de promover para prd |
| `lab` | Laboratório, treinamento, experimentação |

## Regra Especial: Storage Accounts

Storage account tem restrição própria: **3 a 24 caracteres, apenas letras minúsculas e números, sem hífen, nome único globalmente**.

Padrão: `st` + `aid` + workload + ambiente + região, tudo colado:

```
staidlogsprdbrs
```

Se o nome já estiver tomado globalmente, acrescentar diferenciador da organização.

## Tags Obrigatórias

Aplicadas no nível de Resource Group (via Bicep). Um recurso individual pode sobrescrever `diretoria`/`projeto` quando ele serve um caso de uso específico diferente do padrão do RG (ex.: um deployment de modelo que atende uma diretoria só).

| Tag | Valores | Notas |
|---|---|---|
| `area` | `AID` | Fixo |
| `superintendencia` | `SPLOR`, `SCPTS`, `Gabinete` | `Gabinete` quando o recurso serve a AID/Gabinete diretamente — a AID é assessoria ligada ao Gabinete, não subordinada a uma superintendência |
| `diretoria` | `DCPPN`, `DCAF`, `DCMEFO`, `DCTP`, `DCCG` | Vazio quando `superintendencia=Gabinete` |
| `ambiente` | `prd` / `dev` / `lab` | |
| `projeto` | Caso de uso (ex.: `analise-pleitos`, `compartilhado`) | `compartilhado` para infra que serve múltiplos casos de uso |
| `responsavel` | E-mail do dono técnico | |

!!! tip "Herança de tags"

    Tags do RG são herdadas automaticamente pelos recursos via Azure Policy built-in *Inherit a tag from the resource group if missing* (6 atribuições, uma por tag, com identidade `SystemAssigned` própria cada — não sobrescreve tag já definida manualmente no recurso). `diretoria` não existe em nenhum RG hoje — infra compartilhada, sem diretoria única dona; só aparece em recursos individuais tagueados na mão.

## Pontos de Atenção

- **Nomes legados**: recursos movidos entre subscriptions via `az resource move` mantêm o nome de origem (ver nota no topo). Nunca renomear um recurso movido pra "consertar" a nomenclatura.
- **Deployments Cognitive Services**: sub-recurso de `Microsoft.CognitiveServices/accounts` — não aparecem em `az resource list`, mas suportam tag própria via `az resource show --ids .../deployments/{nome}`.
