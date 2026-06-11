---
title: Nomenclatura Azure
tags:
  - azure
  - infraestrutura
---

# Nomenclatura de Recursos Azure ☁️

## Contexto

A AID (Assessoria de Inteligência de Dados) provisiona a infraestrutura da SPLOR na Azure (subscription `SEPLAGMG-SPLOR`): servidores, backup, Synapse e modelos/agentes no Azure AI Foundry.

Esta página documenta a convenção de nomenclatura adotada, baseada no [Cloud Adoption Framework (CAF)](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming) da Microsoft, adaptada ao nosso contexto.

!!! warning "Por que definir antes de criar?"

    Resource groups **não podem ser renomeados** depois de criados - a única alternativa é recriar e migrar os recursos. O custo de errar a nomenclatura no início é alto.

## Convenção Geral

```
[tipo]-aid-[workload]-[ambiente]
```

| Componente | Descrição | Exemplos |
|---|---|---|
| `tipo` | Prefixo abreviado do tipo de recurso, conforme as [abreviações do CAF](https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations) | `rg`, `vnet`, `vm`, `kv` |
| `aid` | Identificador da área (Assessoria de Inteligência de Dados) | `aid` |
| `workload` | A carga de trabalho | `ai`, `data`, `infra`, `backup` |
| `ambiente` | Ambiente de execução | `prd`, `dev` |

## Critério de Separação dos Resource Groups

Recursos que compartilham **ciclo de vida** ficam no mesmo resource group. O RG é a unidade de:

1. **Deleção em massa** - se faz sentido apagar tudo junto, fica junto
2. **RBAC (role-based access control)** - Permissões atribuídas no escopo do RG, não recurso a recurso (ex.: equipe de dados tem `Contributor` no RG de dados, sem acesso aos agentes)
3. **Custo** - cada RG vira um filtro pronto no Cost Management (custo dos modelos vs. Synapse vs. VMs)

## Resource Groups

| Resource group | Conteúdo |
|---|---|
| `rg-aid-ai-prd` | AI Foundry Hub, projects, deployments de modelos, AI Search |
| `rg-aid-data-prd` | Synapse, Data Lake, storage de dados |
| `rg-aid-infra-prd` | VMs, VNet, NSGs, IPs |
| `rg-aid-backup-prd` | Recovery Services Vault, políticas de backup |
| `rg-aid-ai-dev` | Ambiente de desenvolvimento (espelha `prd` com sufixo `dev`) |

## Nomenclatura por Recurso

### `rg-aid-ai-prd` - IA / Foundry

| Recurso | Nome | Observação |
|---|---|---|
| AI Foundry Hub | `hub-aid-prd` | 1 hub para a AID inteira |
| AI Foundry Project | `proj-[caso-de-uso]` | 1 project por caso de uso (ex.: `proj-agente-teams`, `proj-rag-orcamento`) |
| Azure OpenAI / AI Services | `aoai-aid-prd` | Nome globalmente único; em caso de colisão usar `aoai-aid-splor-prd` |
| AI Search | `srch-aid-prd` | Globalmente único, só minúsculas e hífens |
| Storage do hub | `staidaiprd` | Ver [regra de storage](#regra-especial-storage-accounts) |
| Key Vault | `kv-aid-ai-prd` | Máx. 24 caracteres, globalmente único |
| Container Registry | `craidaiprd` | Sem hífens, alfanumérico |

!!! note "Separação por caso de uso"

    A separação por caso de uso acontece no nível de **project** do Foundry, não em RGs diferentes. Todo o Foundry mora em um único RG, com deployments de modelo no hub compartilhados pelos projects.

### `rg-aid-data-prd` - Dados / Synapse

| Recurso | Nome | Observação |
|---|---|---|
| Synapse Workspace | `synw-aid-prd` | Globalmente único |
| Data Lake (ADLS Gen2) | `dlsaidprd` | Regra de storage |
| Storage geral | `staiddataprd` | Regra de storage |
| SQL Pool dedicado | `sqlpool-aid-prd` | Dentro do workspace |
| Spark Pool | `sparkaid` | Máx. 15 caracteres, sem hífen |

### `rg-aid-infra-prd` - Servidores e Rede

| Recurso | Nome | Observação |
|---|---|---|
| VNet | `vnet-aid-prd` | |
| Subnet | `snet-aid-[finalidade]-prd` | Uma por finalidade (ex.: `snet-aid-app-prd`) |
| NSG | `nsg-aid-[finalidade]-prd` | Espelha a subnet |
| VM | `vm-aid-[função]-prd-NN` | Ex.: `vm-aid-n8n-prd-01`; Windows limita o nome do SO a 15 caracteres |
| Disco | `disk-[nome-da-vm]-os` | |
| IP público | `pip-[nome-da-vm]` | |
| NIC | `nic-[nome-da-vm]` | |

### `rg-aid-backup-prd` - Backup

| Recurso | Nome | Observação |
|---|---|---|
| Recovery Services Vault | `rsv-aid-prd` | |
| Política de backup | `bkpol-[alvo]-[frequência]` | Ex.: `bkpol-vm-diario`, `bkpol-vm-semanal` |

### `rg-aid-ai-dev` - Desenvolvimento

Espelha a estrutura de produção trocando o sufixo: `hub-aid-dev`, `synw-aid-dev`, `staidaidev`. Permite comparar custos dev vs. prd com um único filtro.

## Regra Especial: Storage Accounts

Storage account tem restrição própria: **3 a 24 caracteres, apenas letras minúsculas e números, sem hífen, nome único globalmente**.

Padrão: `st` + área + workload + ambiente, tudo colado:

```
staidaiprd
```

Se o nome já estiver tomado globalmente, acrescentar diferenciador da organização: `staidsplorprd` ou `stcamgaidprd`.

## Tags Obrigatórias

Aplicar em todos os recursos, a partir do RG:

| Tag | Valores |
|---|---|
| `area` | `AID` |
| `subsecretaria` | `SPLOR` |
| `ambiente` | `prd` / `dev` |
| `projeto` | `agente-teams`, `rag-orcamento`, `compartilhado` |
| `responsavel` | E-mail do dono técnico |

!!! tip "Herança de tags"

    Tags do RG **não são herdadas** automaticamente pelos recursos. Utilizamos a Azure Policy built-in *Inherit a tag from the resource group* atribuída na subscription para forçar a herança.

## Pontos de Atenção

- **Região**: modelos/Foundry em `eastus2` (melhor disponibilidade de modelos). Para dados do Synapse, avaliar `brazilsouth` caso haja requisito LGPD de residência de dados.
- **Move de recursos**: mover recursos entre RGs é possível, mas Foundry hub/projects têm restrições - criar já no RG correto.
