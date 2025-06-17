---
date: 2025-06-17
authors: [gabrielbdornas]
draft: false
comments: true
categories:
  - Banco de Dados
---

# Banco de Dados e Diagrama Entidade Relacionamento: Um Guia Prático

Você já se perguntou como os dados são organizados em um banco de dados?
Como as informações se conectam entre si?
O Diagrama Entidade Relacionamento (DER) é a ferramenta que nos ajuda a responder essas perguntas.
Neste guia, vamos explorar os conceitos fundamentais do DER e como ele nos ajuda a estruturar nossos dados de forma clara e eficiente.

<!-- more -->

Um Diagrama Entidade Relacionamento, ou DER, é uma representação visual de como os dados estão organizados em um banco de dados.
Neste contexto, é importante entender que:

- **Entidade** é sinônimo de **tabela** no banco de dados.
- Cada entidade possui **atributos** (ou colunas) que descrevem suas características.
- Os **registros** são as linhas de dados que preenchem estas tabelas.
- Os **relacionamentos** mostram como os registros de uma tabela se conectam com os registros de outra tabela.

Por exemplo, em um sistema de biblioteca:
- A entidade "Livro" (tabela) tem atributos como título, autor, ISBN.
- A entidade "Autor" (tabela) tem atributos como nome e CPF.
- Os registros são os cadastros dos livros e autores específicos.
- O relacionamento mostra como cada livro está associado a seu(s) autore(s).

Se você entendeu bem, já sacou que o DER nos ajuda a visualizar esta estrutura de um banco, mostrando as tabelas, suas colunas e como elas se conectam através dos relacionamentos.

## Por que usar um DER?

- **Organização**: Ajuda a estruturar as informações de forma clara e organizada.
- **Comunicação**: Facilita a comunicação entre desenvolvedores e usuários.
- **Prevenção de erros**: Permite identificar problemas antes de criar o banco de dados.
- **Documentação**: Serve como documentação do sistema ou do próprio banco de dados.

## Os Três Tipos de Relacionamentos

Melhorar aqui a explicação do que são as relações.
Falar que a relação é a representação de uma regra de negócio, não sendo, portanto uma verdade absoluta entre negócios diversos.

### 1. Relacionamento Um para Um (1:1)

O relacionamento um para um (1:1) ocorre quando cada registro de uma entidade se relaciona com exatamente um registro de outra entidade, e vice-versa.

Por exemplo, quando dizemos que um funcionário tem um único cargo atual[^1], podemos estabelecer que:

- Cada funcionário só pode ter um cargo atual por vez.
- Cada cargo só pode ser ocupado por um funcionário por vez.
- Esta relação é bidirecional e exclusiva, ou seja, a unicidade é garantida tanto do lado do funcionário quanto do lado do cargo.

[^1]: É sempre importante ressaltar que os relacionamentos representam uma regra de negócio específica, que podem variar dependendo de situação.


**Exemplo na prática:**

??? "Um funcionário por cargo"

    Um funcionário só pode ter um cargo atual, e um cargo só pode ser ocupado por um funcionário por vez.


    === "DER"

        ```mermaid
        erDiagram
            FUNCIONARIO {
                int id
                string nome_pessoa
            }
            CARGO {
                int id
                string nome_cargo
                int funcionario_id
            }
            FUNCIONARIO ||--|| CARGO : "ocupa"
        ```

    === "Tabelas"

        | id | nome_pessoa |
        |----|-------------|
        | 1  | João Silva  |
        | 2  | Maria Santos|
        | 3  | Pedro Costa |
        | 4  | Maria José  |
        | 5  | João Paulo  |

        | id | nome_cargo | funcionario_id |
        |----|------------|----------------|
        | 1  | Analista   | 1              |
        | 2  | Gerente    | 2              |
        | 3  | Coordenador| 3              |

    === "Resultado da Consulta"

        | id_cargo | nome_cargo | id_funcionario | nome_pessoa |
        |----------|------------|----------------|-------------|
        | 1        | Analista   | 1              | João Silva  |
        | 2        | Gerente    | 2              | Maria Santos|
        | 3        | Coordenador| 3              | Pedro Costa |

        ??? "Consulta SQL que une as tabelas"

            ```sql
            SELECT
                c.id as id_cargo,
                c.nome_cargo,
                f.id as id_funcionario,
                f.nome_pessoa
            FROM cargo c
            INNER JOIN funcionario f
            ON f.id = c.funcionario_id
            ORDER BY c.id;
            ```

Outro exemplo poderia ser o casamento monogâmico.
Como sabemos, em um casamento monogâmico, uma pessoa só pode ser casada com uma outra pessoa.

**Exemplo na prática:**

??? "Casamento monogâmico"

    Uma pessoa só pode ser casada com uma outra pessoa, e vice-versa.


    === "DER"

        ```mermaid
        erDiagram
            PESSOA {
                int id
                string cpf
                string nome
                int conjuge_id
            }
            PESSOA ||--|| PESSOA : "id = conjuge_id"
        ```

    === "Tabela"

        | id | cpf        | nome          | conjuge_id |
        |----|------------|---------------|------------|
        | 1  | 12345678900| João Silva    | 2         |
        | 2  | 98765432100| Maria Santos  | 1         |
        | 3  | 11122233344| Pedro Costa   | 4         |
        | 4  | 55566677788| Ana Oliveira  | 3         |

    === "Resultado da Consulta"

        | id_pessoa | cpf_pessoa | nome_pessoa | id_conjuge | cpf_conjuge | nome_conjuge |
        |-----------|------------|-------------|------------|-------------|--------------|
        | 1         | 12345678900| João Silva  | 2          | 98765432100 | Maria Santos |
        | 3         | 11122233344| Pedro Costa | 4          | 55566677788 | Ana Oliveira |

        ??? "Consulta SQL que une as tabelas"

            ```sql
            SELECT
                p1.id as id_pessoa,
                p1.cpf as cpf_pessoa,
                p1.nome as nome_pessoa,
                p2.id as id_conjuge,
                p2.cpf as cpf_conjuge,
                p2.nome as nome_conjuge
            FROM pessoa p1
            INNER JOIN pessoa p2
            ON p1.conjuge_id = p2.id
            ORDER BY p1.id;
            ```

            > 💡 **Nota**: A consulta proposta retorna apenas 2 linhas (ao invés de 4) porque cada casal aparece uma única vez, com uma pessoa na posição "pessoa" e a outra na posição "cônjuge".
            Isso evita duplicação de informações, já que o relacionamento é bidirecional.

### 2. Relacionamento Um para Muitos (1:N)

O relacionamento um para N (1:N) ocorre quando um registro de uma entidade se relaciona com um ou vários registros de outra entidade.

Por exemplo, é como uma mãe e seus filhos: uma mãe pode ter vários filhos, mas cada filho tem apenas uma mãe biológica.

**Exemplo na prática:**

??? "Mãe e filho biológico"

    Uma mãe biológica pode ter vários filhos, mas cada filho tem apenas uma mãe biológica.


    === "DER"

        ```mermaid
        erDiagram
            MAE {
                int id
                string nome
                string cpf
            }
            FILHO {
                int id
                string nome
                string cpf
                int mae_id
            }
            MAE ||--o{ FILHO : "id = mae_id"
        ```

    === "Tabelas"

        | id | nome          | cpf        |
        |----|---------------|------------|
        | 1  | Maria Santos  | 12345678900|
        | 2  | Ana Oliveira  | 98765432100|
        | 3  | Carla Silva   | 11122233344|

        | id | nome          | cpf        | mae_id |
        |----|---------------|------------|---------|
        | 1  | João Silva    | 55566677788| 1      |
        | 2  | Pedro Santos  | 99988877766| 1      |
        | 3  | Lucas Oliveira| 44433322211| 2      |
        | 4  | Sofia Silva   | 77788899900| 3      |

    === "Resultado da Consulta"

        | id_mae | nome_mae    | id_filho | nome_filho   |
        |--------|-------------|----------|--------------|
        | 1      | Maria Santos| 1        | João Silva   |
        | 1      | Maria Santos| 2        | Pedro Santos |
        | 2      | Ana Oliveira| 3        | Lucas Oliveira|
        | 3      | Carla Silva | 4        | Sofia Silva  |

        ??? "Consulta SQL que une as tabelas"

            ```sql
            SELECT
                m.id as id_mae,
                m.nome as nome_mae,
                f.id as id_filho,
                f.nome as nome_filho
            FROM mae m
            INNER JOIN filho f
            ON m.id = f.mae_id
            ORDER BY m.id, f.id;
            ```


Outros exemplos de relação um para muitos (1:N) podem ser:

- Uma editora pode publicar vários livros.
- Um departamento pode ter vários funcionários.
- Uma categoria pode ter vários produtos.

!!! note "**Hora de praticar!**"

    :man_raising_hand: Agora que você já viu exemplos práticos de relacionamentos 1:1 e 1:N, que tal criar seus próprios? Tente:

    1. Desenhar o DER.
    2. Criar as tabelas com alguns registros de exemplo.
    3. Escrever a consulta SQL que une as tabelas (Avançado!!).

    :bulb: **Dica**: Use a ferramenta [Mermaid.js](https://mermaid.js.org/syntax/entityRelationshipDiagram.html) :mermaid: para desenhar seu DER.
    Ela é gratuita e funciona direto no Markdown!

    Compartilhe seu resultado na sessão de comentários abaixo e vamos aprender juntos! :rocket:

### 3. Relacionamento Muitos para Muitos (N:M)

O relacionamento muitos para muitos (N:M) ocorre quando registros de uma entidade podem se relacionar com vários registros de outra entidade, e vice-versa.
Este tipo de relacionamento é mais complexo e geralmente requer uma tabela intermediária (tabela de junção) para ser implementado no banco de dados.

Por exemplo, quando falamos de alunos e disciplinas:

- Um aluno pode se matricular em várias disciplinas.
- Uma disciplina pode ter vários alunos matriculados.
- Precisamos de uma tabela intermediária (matrícula) para registrar estas relações.

**Exemplo na prática:**

??? "Alunos e Disciplinas"

    Um aluno pode se matricular em várias disciplinas, e uma disciplina pode ter vários alunos matriculados.


    === "DER"

        ```mermaid
        erDiagram
            ALUNO {
                int id
                string nome
                string matricula
            }
            DISCIPLINA {
                int id
                string nome
                string codigo
            }
            MATRICULA {
                int id
                int aluno_id
                int disciplina_id
                date data_matricula
            }
            ALUNO ||--o{ MATRICULA : "id = aluno_id"
            DISCIPLINA ||--o{ MATRICULA : "id = disciplina_id"
        ```

    === "Tabelas"

        | id | nome          | matricula |
        |----|---------------|-----------|
        | 1  | João Silva    | 2023001   |
        | 2  | Maria Santos  | 2023002   |
        | 3  | Pedro Costa   | 2023003   |

        | id | nome          | codigo |
        |----|---------------|---------|
        | 1  | Matemática    | MAT001  |
        | 2  | Português     | PORT001 |
        | 3  | História      | HIST001 |

        | id | aluno_id | disciplina_id | data_matricula |
        |----|----------|---------------|----------------|
        | 1  | 1        | 1             | 2023-02-01     |
        | 2  | 1        | 2             | 2023-02-01     |
        | 3  | 2        | 1             | 2023-02-01     |
        | 4  | 2        | 3             | 2023-02-01     |
        | 5  | 3        | 2             | 2023-02-01     |
        | 6  | 3        | 3             | 2023-02-01     |

    === "Resultado da Consulta"

        | id_aluno | nome_aluno | id_disciplina | nome_disciplina |
        |----------|------------|---------------|-----------------|
        | 1        | João Silva | 1             | Matemática      |
        | 1        | João Silva | 2             | Português       |
        | 2        | Maria Santos| 1            | Matemática      |
        | 2        | Maria Santos| 3            | História        |
        | 3        | Pedro Costa| 2             | Português       |
        | 3        | Pedro Costa| 3             | História        |

        ??? "Consulta SQL que une as tabelas"

            ```sql
            SELECT
                a.id as id_aluno,
                a.nome as nome_aluno,
                d.id as id_disciplina,
                d.nome as nome_disciplina
            FROM aluno a
            INNER JOIN matricula m ON m.aluno_id = a.id
            INNER JOIN disciplina d ON d.id = m.disciplina_id
            ORDER BY a.id, d.id;
            ```

            > 💡 **Nota**: Observe como a tabela MATRICULA serve como intermediária, permitindo que um aluno se relacione com várias disciplinas e vice-versa. Este é um padrão comum em relacionamentos N:M.

!!! note "**Hora de praticar!**"

    :man_raising_hand: Consegue pensar em outros exemplos muitos para muitos (N:M)?
    Claro que consegue.
    Além de pensar,tente também:

    1. Desenhar o DER.
    2. Criar as tabelas com alguns registros de exemplo.
    3. Escrever a consulta SQL que une as tabelas (Avançado!!).

    :bulb: **Dica**: Use a ferramenta [Mermaid.js](https://mermaid.js.org/syntax/entityRelationshipDiagram.html) :mermaid: para desenhar seu DER.
    Ela é gratuita e funciona direto no Markdown!

    Compartilhe seu resultado na sessão de comentários abaixo e vamos aprender juntos! :rocket:

    ??? note "Sistema de Biblioteca"

        Agora que você já sabe tudo sobre o DER, e já praticou todos os tipos de relacionamento, porque não criar seu primeiro banco de dados?
        Como sugestão, pense no banco para uma biblioteca: :book:

        - As **entidades** podem ser: Funcionários, Setores, Livros, Autores, Leitores, Empréstimos
        - Os **relacionamentos** podem ser:
            - Um setor pode ter um funcionário responsável.
            - Um funcionário pode ter uma chefia imediata.
            - Um livro pode ser guardado em apenas um setor.
            - Um livro pode ter vários autores.
            - Um leitor pode pegar vários livros emprestados.
            - Um livro pode ser emprestado várias vezes.

        Se você conseguir desenhar este DER pode ter certeza que vai conseguir criar qualquer um.

## Dicas finais para criação de um bom DER

1. **Comece simples**: Identifique as entidades principais primeiro.
2. **Use nomes claros**: Escolha nomes que façam sentido para todos.
3. **Pense nas relações**: Como as entidades se conectam?
4. **Valide com usuários**: Certifique-se que o diagrama faz sentido para quem vai usar, ou se ela realmente representa a regra de negócio a ser atendida.

## Conclusão

O Diagrama Entidade Relacionamento é uma ferramenta poderosa para planejar e entender a estrutura de um banco de dados.
Ao dominar os tipos de relacionamentos você estará preparado para criar estruturas de dados eficientes e bem organizadas.

Lembre-se: um bom DER é aquele que qualquer pessoa consegue entender, mesmo que não seja especialista em banco de dados.
Por isso, use exemplos do dia a dia e mantenha a simplicidade!
