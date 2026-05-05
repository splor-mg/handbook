# Volumes LOA

> **AID-SPLOR/SEPLAG**

---

<div class="project-status-card" markdown>

**Status:** `Concluído`

</div>

!!! abstract "Descrição"

    O Projeto Volumes LOA tem como foco principal a modernização, automação e estabilização do processo de geração dos documentos da Lei Orçamentária Anual. O trabalho centraliza-se na criação de um fluxo de trabalho (pipeline) robusto que permita a geração confiável desses volumes, eliminando processos manuais, resolvendo conflitos de dependência de software e garantindo a segurança no tratamento de dados sensíveis. Além da dimensão técnica, o projeto promove uma cultura de compartilhamento de conhecimento e documentação contínua dentro da equipe.

??? tip "Objetivos"

    - Produção Automatizada da LOA, implementando fluxos de CI/CD (GitHub Actions) que garantam a elaboração dos volumes da LOA de forma contínua, previsível e ágil, reduzindo a necessidade de intervenções manuais na geração dos documentos orçamentários.

    - Segurança da Infraestrutura, assegurando o tratamento sigiloso de credenciais sensíveis durante o processo de build das imagens Docker, eliminando a exposição de dados de acesso ao Bitbucket e garantindo um ambiente de desenvolvimento e produção seguro.

    - Eliminar conflitos de dependência e falhas de build através da fixação rigorosa de versões e da padronização do ambiente, assegurando consistência total entre as execuções locais e no servidor.

    - Promover a longevidade do projeto por meio da refatoração contínua de scripts, manutenção de documentação técnica acessível e disseminação de conhecimento, facilitando a autonomia da equipe e o onboarding de novos colaboradores.

!!! info "Linha do Tempo — Volumes LOA"

    ```mermaid
    timeline
        title Linha do Tempo — Volumes LOA
        Setembro 2025 : Geração e testes da LOA 2026
                   : Gestão de pendências
        Outubro 2025 : Inclusão de base de dados.
        Janeiro 2026 : Verificação de bases pós-emendas
        Fevereiro 2026 : Geração de volumes pós-emendas
        Março 2026 : Fechamento da LOA 2026
        Próximos Passos : Refatoração de scripts
                   : Automação via Taskipy
                   : Configuração do Dockerhub
    ```

??? info "Projeto no Github — Gestão à Vista"

    Acesse o painel do projeto no GitHub:

    [ Acessar Painel ](https://github.com/orgs/splor-mg/projects/13/views/15?sliceBy%5Bvalue%5D=Volumes+LOA){ .md-button }

??? success "Ganhos Esperados"

    -  Redução significativa do tempo necessário para gerar os volumes da LOA, permitindo que a equipe foque em análises em vez de correção de erros de infraestrutura.

    - Eliminação da fragilidade de hardcoding de credenciais, protegendo os sistemas e repositórios contra acessos não autorizados.

    - Garantia de que, ao rodar o processo em qualquer ambiente (local ou nuvem), o resultado seja exatamente o mesmo, evitando os "conflitos de dependência" que paralisam o desenvolvimento.

    - Com a documentação centralizada e a cultura de live coding, a equipe se torna menos dependente de indivíduos específicos, tornando o conhecimento um ativo coletivo da organização.

    - Redução da "dívida técnica", resultando em menos tempo gasto consertando o próprio ambiente e mais tempo gerando valor para a LOA.

??? quote "Observações"

    As informações apresentadas refletem o estado atual do projeto e serão atualizadas conforme o avanço das atividades.

