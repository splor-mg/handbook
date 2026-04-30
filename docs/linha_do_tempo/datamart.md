# Datamart

> **AID-SPLOR/SEPLAG**

---

<div class="project-status-card" markdown>

**Status:** `Em execução`

</div>

!!! abstract "Descrição"

    O projeto Datamart da SPLOR tem como objetivo organizar e unificar os dados orçamentários que hoje estão dispersos em diversos repositórios, cada um com seu próprio processo de extração e sem integração entre si.

    A área já possui uma base sólida: os repositórios dados-* realizam extração e armazenamento de dados seguindo o padrão datapackage. O problema é que cada um faz isso à sua maneira, o que gera dificuldade de manutenção, retrabalho e perda de conhecimento quando há mudança de equipe.

    O projeto resolve isso entregando um processo único, padronizado e documentado, com um banco de dados central que consolida todo o histórico orçamentário desde 2002. Sobre essa base, será disponibilizada uma ferramenta de consulta self-service para que as áreas acessem os dados de forma direta, confiável e sem depender de intermediários técnicos.

??? tip "Objetivos"

    - Unificação do processo de ETL em uma mesma base de código em Python.
    - Aprimoramento dos metadados atuais.
    - Manter todo o processo de transformação dentro do processo unificado de ETL e não em ferramentas de BI.
    - Inclusão de todos os dados extraídos em um banco de dados unificado.
    - Unificação de dados históricos para todo período existente (2002 em diante).
    - Disponibilização de ferramenta self-service BI que poderá ser utilizada como fonte de consulta dos dados unificados.
    - Documentar todo o processo, facilitando a transmissão do conhecimento para novos integrantes da equipe.

!!! info "Linha do Tempo — Datamart"

    ```mermaid
    timeline
        title Linha do Tempo — Datamart
        Fevereiro 2026 : Ferramenta de extração criada e publicada
                   : Coleta automatizada de dados por e-mail e sistemas de informação disponibilizada
        Março 2026 : Ferramenta aprimorada e validada
                   : Ajustes de estabilidade - Novos recursos de configuração e testes em ambientes
        Abril 2026 : Início do banco de dados - Em andamento
                   : Coletas sendo executadas automaticamente - Em andamento
                   : Construção da estrutura do banco de dados - Em andamento
        Próximos Passos : Migração das fontes de dados
                   : Bases de dados integradas ao novo padrão de coleta e armazenamento
                   : Banco de dados central estruturado
                   : Qualidade e validação dos dados
    ```

??? info "Projeto no Github — Gestão à Vista"

    Acesse o painel do projeto no GitHub:

    [ Acessar Painel ](https://github.com/orgs/splor-mg/projects/13/views/28){ .md-button }

??? success "Ganhos Esperados"

    - Repositório (este) de datapackages unificados (metadados).
    - Ferramenta CLI unificando todo o processo de ETL.
    - Metadados de todos os datapackages revisados e melhorados (principalmente descrições e constraints).
    - Repositórios anuais (histórico) de todos os datapackages (dados e metadados), que servirão, entre outras coisas, como backup de dados.
    - Banco de dados SQL alimentado com todos os dados extraídos (e rotina de alimentação diária funcionando).
    - Configuração de ferramenta self-service BI Metabase.
    - Documentação completa de todos os repositórios e processos criados.

??? quote "Observações"

    As informações apresentadas refletem o estado atual do projeto e serão atualizadas conforme o avanço das atividades.

