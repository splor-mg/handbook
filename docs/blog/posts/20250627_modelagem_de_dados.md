---
date: 2025-06-27
authors: [carloshob]
draft: false
comments: true
categories:
  - Bancos de Dados
  - Modelagem de Dados
---

# Fundamentos para Modelagem de Dados

Na empreitada de modernizar a gestão dos bancos de dados do Estado, encontramos na modelagem de dados um dos conhecimentos fundamentais indispensáveis. Nesta postagem, compartilho alguns dos conhecimentos adquiridos durante o curso [Mastering Data Modeling Fundamentals](https://www.udemy.com/course/mastering-data-modeling-fundamentals/?couponCode=LOCLZDOFFPBRCTRL), ministrado por Alan R. Simon, professor da Arizona State University e uma autoridade respeitada em modelagem de dados, data warehousing e arquitetura de sistemas de informação. 


<!-- more -->

## Por que modelar?

A modelagem de dados trata de uma representação daquilo que os dados realmente são no mundo real e nos fornece informações sobre as diversas características e regras que se aplicam aos dados.

Como modelo, ela nos auxilia na abstração das especificidades da implementação de um banco de dados e, com isso, permite o foco em aspectos conceituais dos dados.

A modelagem trabalha essencialmente com dados tabulares, ou seja, aqueles estruturados em linhas e colunas, onde uma linha (ou registro) representa uma observação ou entidade (sujeito de dados), e uma coluna (ou campo/atributo) representa uma variável ou característica dessa observação. Apesar de se parecer com uma planilha, guarda mais semântica de transação do que uma planilha.

???+ info "Quando surgiu a modelagem?"
    A modelagem de dados como disciplina formal foi inaugurada pelo artigo seminal de Peter Chen, "[The Entity-Relationship Model: Toward a Unified View of Data](https://dl.acm.org/doi/10.1145/320434.320440)", publicado em 1976 na ACM Transactions on Database Systems. Este trabalho estabeleceu os fundamentos conceituais que ainda hoje orientam a prática da modelagem de dados.

???+ info "O que a modelagem de dados faz?"
    A modelagem de dados tem quatro funções principais:

    **1. Identificar os principais sujeitos de dados**
    Também chamados entidades, objetos, classes ou tabelas - são os "nouns" do sistema de dados.

    **2. Identificar os atributos**
    As características ou propriedades de cada sujeito de dados.

    **3. Identificar as relações entre os sujeitos**
    Como os registros de uma tabela se conectam com os registros de outra tabela.

    **4. Identificar as regras de negócio**
    As regras específicas que se aplicam aos dados e suas relações.

???+ info "Como fazer modelagem de dados?"
    O processo de modelagem segue quatro etapas fundamentais:

    **1. Entender os dados**
    Compreender os principais assuntos e conceitos do domínio.

    **2. Estabelecer as regras de negócio**
    Definir como as regras de negócio serão replicadas no banco de dados.

    **3. Estabelecer os relacionamentos**
    Mapear como os diferentes sujeitos de dados se conectam.

    **4. Resolver inconsistências**
    Identificar e corrigir problemas, preenchendo lacunas no modelo.

## Entidades

Uma entidade representa um **objeto do mundo real** que existe independentemente e sobre o qual queremos armazenar informações. Em termos práticos, uma entidade se torna uma **tabela de banco de dados** quando implementada.

**Exemplos de entidades no orçamento:**
- Unidades Orçamentárias
- Fontes de Recurso
- Elementos de despesa
- Função
- Unidade de Programação de Gasto

As entidades representam **áreas temáticas importantes** do domínio e podem ser entendidas como "nouns" do sistema - coisas sobre as quais queremos manter dados.

???+ note "Entidades fortes vs entidades fracas"
    As entidades podem ser classificadas em dois tipos principais baseados em sua **independência** e **capacidade de identificação**:

    === "Entidades Fortes"

        - **Existem independentemente** de outras entidades
        - **Podem ser identificadas unicamente** por seus próprios atributos
        - **Não dependem** de nenhuma outra entidade para existir
        - **Sempre possuem uma chave primária própria**

        **Exemplos:**

        - **CLIENTE** (identificado por CPF ou ID)
        - **PRODUTO** (identificado por código ou SKU)
        - **DEPARTAMENTO** (identificado por código ou nome)

    === "Entidades Fracas"

        - **Dependem de outras entidades** para existir
        - **Não podem ser identificadas unicamente** apenas por seus próprios atributos
        - **Precisam de uma entidade forte** para ter significado
        - **Sua chave primária inclui a chave da entidade forte**

        **Tipos de dependência:**

        - **Dependência de identificação**: A entidade fraca não pode ser identificada sem a entidade forte
        - **Dependência de existência**: A entidade fraca não pode existir sem a entidade forte

        **Exemplos:**

        - **DEPENDENTE** (depende de FUNCIONARIO)
        - **ITEM_PEDIDO** (depende de PEDIDO)
        - **NOTA** (depende de ALUNO e DISCIPLINA)

    === "DER"
        ```mermaid
        erDiagram
            FUNCIONARIO ||--o{ DEPENDENTE : "possui"
            PEDIDO ||--o{ ITEM_PEDIDO : "contém"
            ALUNO ||--o{ NOTA : "recebe"
            DISCIPLINA ||--o{ NOTA : "avalia"
        ```

    **Nota:** As entidades fracas são representadas com bordas duplas em diagramas ER para indicar sua dependência.

## Atributos

Um atributo representa uma **característica ou propriedade** de uma entidade. Em termos práticos, quando convertemos um modelo de dados em banco de dados, um atributo se torna uma **coluna** (ou campo) de uma tabela.

**Exemplos:**

- **CLIENTE**: nome, CPF, data_nascimento, email, telefone
- **PRODUTO**: código, nome, preço, categoria, estoque
- **FUNCIONARIO**: matricula, nome, salario, data_admissao

### **Tipos de Atributos**

Os atributos podem ser **simples** ou  **multivalorados**.

- **Simples**: Contêm apenas um valor (ex: uma pessoa normalmente tem somente um nome, somente uma idade, somente um CPF)
- **Multivalorados**: Podem conter múltiplos valores (ex: uma pessoa pode ter um ou mais emails, telefones, endereços)


### **Determinação de Atributos**

Normalmente, os atributos são definidos **após** as entidades serem identificadas. No entanto, houve um período em que a abordagem `bottom-up` ("de baixo para cima") era popular - primeiro identificavam-se todos os atributos possíveis e, em seguida, agrupavam-se quais pertenciam a cada entidade.


### **Regras e Descrições**

Os atributos podem ter **descrições e regras** que definem:

- **Tipo de dados** (ex: VARCHAR, INTEGER, DATE)
- **Valores possíveis** (ex: "ativo", "inativo", "suspenso")
- **Restrições** (ex: idade entre 0 e 150)
- **Obrigatoriedade** (se pode ou não ser nulo)

???+ note "Tipos de Dados"
    Os tipos de dados definem **como os valores são armazenados e processados** no banco de dados. Cada tipo tem características específicas que determinam o formato, tamanho e operações permitidas. A escolha correta do tipo de dados afeta a performance, armazenamento e integridade dos dados.

    ???+ info "Tipos numéricos"
        - **INTEGER/INT**: Números inteiros (ex: 1, -5, 1000)
        - **DECIMAL/NUMERIC**: Números com casas decimais (ex: 10.50, 3.14159)
        - **FLOAT/REAL**: Números de ponto flutuante para cálculos científicos
        - **BIGINT**: Números inteiros muito grandes


    ???+ info "Tipos de texto"
        - **VARCHAR(n)**: Texto de tamanho variável até n caracteres
        - **CHAR(n)**: Texto de tamanho fixo com n caracteres
        - **TEXT**: Texto de tamanho ilimitado
        - **LONGTEXT**: Texto muito longo

    ???+ info "Tipos de data e hora"
        - **DATE**: Data (ex: 2024-01-15)
        - **TIME**: Hora (ex: 14:30:25)
        - **DATETIME**: Data e hora combinadas
        - **TIMESTAMP**: Marca temporal automática

    ???+ info "Tipos booleanos"
        - **BOOLEAN/BOOL**: Valores verdadeiro/falso (TRUE/FALSE, 1/0)

    ???+ info "Tipos binários"
        - **BLOB**: Dados binários (imagens, documentos)
        - **BINARY**: Dados binários de tamanho fixo

???+ note "Valores Possíveis"
    Os valores possíveis definem **quais valores são aceitos** por um atributo, garantindo que apenas dados válidos sejam inseridos no banco de dados. Outro benefício da definição prévia dos valores possíveis é permitir uma validação automática acerca da consistência de dados e prevenção de erros.

    ???+ info "Amplitude de valores"
        - **Faixas numéricas**: idade >= 0 AND idade <= 150
        - **Intervalos de datas**: data_nascimento >= '1900-01-01' AND data_nascimento <= CURRENT_DATE
        - **Limites de texto**: LENGTH(nome) >= 2 AND LENGTH(nome) <= 100

    ???+ info "Listas de valores"
        - **Enumerados**: status IN ('ativo', 'inativo', 'suspenso')
        - **Códigos**: tipo_pessoa IN ('F', 'J') (Física, Jurídica)
        - **Categorias**: categoria IN ('eletrônicos', 'vestuário', 'alimentos')

    ???+ info "Padrões (tegex)"
        - **CPF**: Formato XXX.XXX.XXX-XX
        - **Email**: Deve conter @ e domínio válido
        - **Telefone**: Formato (XX) XXXXX-XXXX

    ???+ info "Valores especiais"
        - **NULL**: Valor nulo (ausência de valor)
        - **DEFAULT**: Valor padrão quando não especificado
        - **AUTO_INCREMENT**: Valor automático incremental


???+ note "Restrições de Atributos"
    As restrições são **regras que definem limitações e condições** que devem ser respeitadas pelos dados. Elas ajudam a garantir a **integridade e consistência** dos dados no modelo. São fundamentais para manter a **qualidade dos dados** e devem ser identificadas durante a modelagem conceitual, mesmo que sua implementação ocorra apenas no modelo físico.

    ???+ info "1. Restrições de tipo"
        Definem o tipo de dados que um atributo pode armazenar.
        
        **Exemplos**: VARCHAR(50), INTEGER, DATE, DECIMAL(10,2)
        
        **Objetivo**: Garantir que os dados sejam do formato correto

    ???+ info "2. Restrições de domínio"
        Definem os valores válidos que um atributo pode assumir.
        
        **Amplitude dos dados**: idade > 0 e idade < 150
        
        **Lista de valores**: status IN ('ativo', 'inativo', 'suspenso')
        
        **Objetivo**: Validar que os valores estão dentro do esperado

    ???+ info "3. Restrições de chave"
        Identificam atributos que devem ser únicos para cada registro.
        
        **Chave Primária**: Identifica unicamente cada registro
        
        **Chave Única**: Garante que não há duplicatas
        
        **Objetivo**: Manter a unicidade dos dados

    ???+ info "4. Restrições de integridade referencial"
        Garantem que relacionamentos entre entidades sejam válidos.
        
        **Chave Estrangeira**: Referencia uma chave primária em outra tabela
        
        **Objetivo**: Manter a consistência entre tabelas relacionadas

    ???+ info "5. Restrições de negócio"
        Regras específicas do domínio que os dados devem seguir.
        
        **Exemplo**: "Um funcionário não pode ter salário negativo"
        
        **Objetivo**: Implementar lógica de negócio nos dados

???+ note "Obrigatoriedade"
    A obrigatoriedade define se um atributo **deve ou não ter um valor**, controlando a completude dos dados no banco de dados. Afeta a integridade dos dados, bem como a experiência do usuário.

    ???+ info "NOT NULL (obrigatório)"
        - **Definição**: O atributo **deve** ter um valor
        - **Comportamento**: Não aceita valores nulos
        - **Exemplos**: CPF, nome, data_nascimento
        - **Uso**: Para informações essenciais que sempre devem estar presentes

    ???+ info "NULL (opcional)"
        - **Definição**: O atributo **pode** não ter um valor
        - **Comportamento**: Aceita valores nulos
        - **Exemplos**: telefone_secundario, observacoes, foto_perfil
        - **Uso**: Para informações complementares que podem estar ausentes

    ???+ info "DEFAULT (valor padrão)"
        - **Definição**: Valor automaticamente atribuído quando não especificado
        - **Exemplos**: 
            - data_cadastro DEFAULT CURRENT_TIMESTAMP
            - status DEFAULT 'ativo'
            - quantidade DEFAULT 1
        - **Uso**: Para valores comuns que não precisam ser sempre informados

    **Considerações Importantes:**

    - **Chaves primárias**: Sempre NOT NULL
    - **Chaves estrangeiras**: Podem ser NULL (dependendo da regra de negócio)
    - **Campos de auditoria**: Geralmente NOT NULL como DEFAULT
    - **Campos opcionais**: Devem ser NULL para permitir ausência


## Relacionamentos entre entidades

Os relacionamentos representam as conexões ou associações lógicas entre diferentes entidades em um modelo de dados, descrevendo como elas interagem ou se relacionam entre si. Na notação clássica ER (Entity-Relationship), os relacionamentos são representados graficamente por um diamante (♢) conectando as entidades envolvidas, enquanto na notação "Crow's Foot" (Pé de Galinha) são representados simplesmente por linhas conectando as entidades, com símbolos especiais nas extremidades para indicar a cardinalidade do relacionamento.

🚌 Os relacionamentos basicamente auxiliam na navegação, como uma espécie de estrada que lhe permite trafegar por todo conjunto de dados 

???+ info "Regras de negócio vs banco de dados"
    É a partir das regras de negócio é que podemos derivar as seguintes características do **relacionamento** entre as entidades: 

    - **Cardinalidade**
    - **Obrigatoriedade**
    - **Valores possíveis/restrições**

### **Cardinalidade**

A cardinalidade define quantas instâncias de uma entidade podem se relacionar com quantas instâncias de outra entidade em um relacionamento. É uma propriedade fundamental que determina a "força" ou "intensidade" do relacionamento entre duas entidades.

A cardinalidade é determinada pelas regras de negócio e deve ser cuidadosamente analisada durante a modelagem conceitual, pois influencia diretamente a estrutura do banco de dados final.

???+ info "Tipos e notação de cardinalidade"
    - **1:1 (Um para Um)**: Uma instância da entidade A se relaciona com exatamente uma instância da entidade B
    - **1:N (Um para Muitos)**: Uma instância da entidade A se relaciona com múltiplas instâncias da entidade B
    - **N:1 (Muitos para Um)**: Múltiplas instâncias da entidade A se relacionam com uma instância da entidade B
    - **N:M (Muitos para Muitos)**: Múltiplas instâncias da entidade A se relacionam com múltiplas instâncias da entidade B

    **Notação de Cardinalidade**:

    - **Notação Clássica ER**: Usa símbolos específicos nas extremidades das linhas de relacionamento
    - **Notação Crow`s Foot**: Utiliza "pés de galinha" (três linhas) para indicar "muitos" e linhas simples para "um"

    === "Notação Clássica ER (Entity-Relationship)"
        A notação clássica ER utiliza símbolos específicos nas extremidades das linhas de relacionamento para indicar a cardinalidade. Esta notação foi desenvolvida por Peter Chen e é amplamente utilizada em modelagem conceitual.

        **Símbolos utilizados:**

        - `|` (linha vertical) = exatamente um (1)
        - `O` (círculo) = zero ou um (0..1)
        - `||` (duas linhas verticais) = zero ou muitos (0..*)
        - `|` (linha vertical com barra) = um ou muitos (1..*)

        **Exemplo prático - Sistema Acadêmico:**

        ```mermaid
        erDiagram
            DEPARTAMENTO ||--o{ PROFESSOR : "pertence a"
            PROFESSOR ||--o{ AULA : "ministra"
            AULA ||--o{ ALUNO : "matriculado em"
            DEPARTAMENTO ||--o{ AULA : "oferece"
            AULA ||--|| SALA : "ocorre em"
        ```

        **Explicação dos relacionamentos:**

        - **DEPARTAMENTO ||--o{ PROFESSOR**: Um departamento pode ter zero ou muitos professores, e um professor pertence a exatamente um departamento
        - **PROFESSOR ||--o{ AULA**: Um professor pode ministrar zero ou muitas aulas, e uma aula é ministrada por exatamente um professor
        - **AULA ||--o{ ALUNO**: Uma aula pode ter zero ou muitos alunos matriculados, e um aluno pode estar matriculado em zero ou muitas aulas
        - **DEPARTAMENTO ||--o{ AULA**: Um departamento pode oferecer zero ou muitas aulas, e uma aula é oferecida por exatamente um departamento
        - **AULA ||--|| SALA**: Uma aula ocorre em exatamente uma sala, e uma sala pode ser usada para exatamente uma aula por vez

    === "Notação Crow's Foot (Pé de Galinha)"
        A notação Crow's Foot (pé de galinha) é uma representação mais visual e intuitiva que utiliza "pés de galinha" (três linhas divergentes ⋔) para indicar "muitos" e linhas simples para "um". Esta notação é muito popular em ferramentas de modelagem como ERwin, PowerDesigner e MySQL Workbench, mas sofre variações a depender da ferramenta utilizada.

        **Símbolos utilizados:**

        - `|` (linha simples) = exatamente um (1)
        - `O` (círculo) = zero ou um (0..1)
        - `|||` (três linhas) = zero ou muitos (0..*)

        **Representação visual real do Crow's Foot:**

        ```
        CLIENTE ||────0< PEDIDO
        (um)             (zero ou muitos)
        (1,1)            (0,M)
        
        PEDIDO ||────0< ITEM_PEDIDO
        (um)            (zero ou muitos)
        (1,1)           (0,M)
        
        PRODUTO ||────0< ITEM_PEDIDO
        (um)             (zero ou muitos)
        (1,1)            (0,M)
        
        CLIENTE ||────1M ENDERECO
        (um)             (zero ou muitos)
        (1,1)            (1,M)
        
        PEDIDO ||────|| CARRINHO
        (um)            (um)
        (1,1)           (1,1)
        ```

        **Exemplo prático - Sistema de E-commerce:**

        ```mermaid
        erDiagram
            CLIENTE ||--o{ PEDIDO : "faz"
            PEDIDO ||--|| CARRINHO : "contém"
            PEDIDO ||--o{ ITEM_PEDIDO : "inclui"
            PRODUTO ||--o{ ITEM_PEDIDO : "vendido em"
            CATEGORIA ||--o{ PRODUTO : "classifica"
            CLIENTE ||--o{ ENDERECO : "possui"
        ```

        **Explicação dos relacionamentos:**
        - **CLIENTE ||--o{ PEDIDO**: Um cliente pode fazer zero ou muitos pedidos, e um pedido pertence a exatamente um cliente
        - **PEDIDO ||--|| CARRINHO**: Um pedido contém exatamente um carrinho, e um carrinho pertence a exatamente um pedido
        - **PEDIDO ||--o{ ITEM_PEDIDO**: Um pedido pode incluir um ou muitos itens, e um item de pedido pertence a exatamente um pedido
        - **PRODUTO ||--o{ ITEM_PEDIDO**: Um produto pode ser vendido em zero ou muitos itens de pedido, e um item de pedido refere-se a exatamente um produto
        - **CATEGORIA ||--o{ PRODUTO**: Uma categoria pode classificar zero ou muitos produtos, e um produto pertence a exatamente uma categoria
        - **CLIENTE ||--o{ ENDERECO**: Um cliente pode possuir zero ou muitos endereços, e um endereço pertence a exatamente um cliente

        **Nota:** O diagrama Mermaid acima usa a notação textual equivalente, mas em ferramentas como ERwin, PowerDesigner ou MySQL Workbench, você veria visualmente os "pés de galinha" (três linhas divergentes) nas extremidades dos relacionamentos.

    === "Comparação entre as Notações"
        | Cardinalidade | Notação Clássica ER | Notação Crow's Foot | Descrição |
        |---------------|---------------------|-------------------|-----------|
        | 1:1 | `||--||` | `||--||` | Um para um |
        | 1:N | `||--o{` | `||--o{` | Um para muitos |
        | N:1 | `}o--||` | `}o--||` | Muitos para um |
        | M:N | `}o--o{` | `}o--o{` | Muitos para muitos |
        | 0..1:1 | `O|--||` | `O|--||` | Zero ou um para um |
        | 1:0..1 | `||--O|` | `||--O|` | Um para zero ou um |

        **Vantagens de cada notação:**

        **Notação Clássica ER:**

        - Mais formal e acadêmica
        - Símbolos precisos e padronizados
        - Ideal para documentação técnica detalhada

        **Notação Crow's Foot:**

        - Mais intuitiva e visual
        - Amplamente suportada por ferramentas
        - Facilita a comunicação com stakeholders não técnicos




### **Direção**

Cuida da nomeação (bidirecional ou unidirecional) de como ocorre a interação entre os diferentes objetos de dados existentes. Por exemplo, entre a entidade "professor" e a entidade "aula" podemos nomear pelo menos 1 relação que ocorre em duas direções (bidirecional): enquanto um professor oferta uma aula (direção "professor-aula"), uma aula é ofertada por um professor (direção "aula-professor").

**Exemplo prático - Relacionamento bidirecional:**
- **Professor** → **Aula**: "oferece"
- **Aula** → **Professor**: "é oferecida por"

???+ info "⚠️ Atenção!"
    - Os nomes de um relacionamento **não precisam ser exclusivos** a nível conceitual
    - Recomenda-se usar nomes que representem a **relação bidirecional** entre duas entidades
    - É possível haver **múltiplos relacionamentos** entre as mesmas entidades
    - A direção ajuda na **navegação** e **compreensão** do modelo de dados


### **Hierarquia**

Trata da organização dos elementos de dados em **níveis de autoridade, dependência ou generalidade**, permitindo representar estruturas de **parentesco** ou de **especialização** entre entidades.

No contexto da modelagem de dados, a hierarquia pode indicar:

- **Subordinação**: uma entidade pode ser subordinada a outra (por exemplo, uma *Aula* está subordinada a um *Departamento Acadêmico*);
- **Composição**: uma entidade pode ser **parte de** uma entidade maior (por exemplo, um *Departamento Acadêmico* é composto por *Instrutores*);
- **Especialização/Generalização**: uma entidade pode ser uma especialização de outra (por exemplo, *Pessoa* pode ser generalização de *Aluno* e *Instrutor*).

A hierarquia influencia:

- **A integridade referencial**, pois uma entidade hierarquicamente inferior geralmente depende da existência da superior;
- **A propagação de atributos ou restrições** (ex.: herança em modelos mais avançados como os objetos-relacionais);
- **A forma de navegação ou junção entre tabelas** em consultas SQL, especialmente em joins que seguem a lógica hierárquica dos dados.

???+ info "⚠️ Atenção!"
    - Hierarquia não implica necessariamente direção de relacionamento, mas pode coexistir com ela;
    - É comum representar hierarquia visualmente com árvores ou estruturas de **camadas**;
    - Em bancos relacionais, hierarquias muitas vezes se expressam por **chaves estrangeiras** apontando para entidades superiores ou pela presença de **campos identificadores** hierárquicos (ex.: códigos estruturados)

### **Relacionamentos Ternários**

Um relacionamento ternário envolve **três entidades simultaneamente**, onde a relação entre duas entidades depende da terceira.

???+ info "O que é um relacionamento ternário?"
    **Definição**: Relacionamento que só faz sentido quando consideramos as três entidades juntas.

    **Exemplo prático**: 
    - **PROFESSOR** ensina **AULA** em **SALA**
    - A pergunta "Qual professor ensina qual aula?" não é suficiente
    - Precisamos saber **também** "em qual sala" para ter a informação completa

    ```mermaid
    erDiagram
        PROFESSOR ||--o{ AULA_PROFESSOR_SALA : "ministra em"
        SALA ||--o{ AULA_PROFESSOR_SALA : "local de"
        AULA ||--o{ AULA_PROFESSOR_SALA : "ocorre com"
    ```

???+ info "Outros exemplos"
    **Sistema de Vendas**: VENDEDOR vende PRODUTO para CLIENTE
    
    **Sistema de Projetos**: FUNCIONARIO trabalha em PROJETO como FUNCAO
    
    **Sistema de Seguros**: SEGURADO possui APOLICE com COBERTURA

???+ info "Implementação"
    **Como implementar**: Através de uma **tabela de relacionamento** que contém:
    - Chaves estrangeiras para as três entidades
    - Atributos específicos do relacionamento (se houver)
    - Chave primária composta

    **Quando usar**:
    - Quando a relação entre duas entidades **depende** de uma terceira
    - Quando há **atributos específicos** do relacionamento
    - Quando a **regra de negócio** exige as três entidades


## Ambientes para Modelagem de Dados

A modelagem de dados pode ocorrer em diferentes tipos de ambientes, dentre os quais se destacam os ambientes **analítico e transacional**. Os sistemas transacionais (ou operacionais) são a espinha dorsal das operações diárias das organizações, responsáveis por processar transações em tempo real – como vendas, cadastros ou movimentações financeiras. Já os sistemas analíticos têm como propósito transformar esses dados operacionais em insights estratégicos. Normalmente, os dados são extraídos dos sistemas transacionais e enviados para um ambiente analítico – como data marts ou data warehouses –, onde são modelados, integrados e otimizados para análises complexas. Esses ambientes utilizam estruturas dimensionalizadas (como esquemas em estrela ou floco de neve) e técnicas como OLAP, permitindo à SPLOR realizar desde análises históricas até projeções orçamentárias com agilidade e profundidade, sem impactar o desempenho dos sistemas operacionais.

???+ info "Data Warehouse (DW), Data Mart e Data Lake"
    - **Data Warehouse (DW)**: repositório centralizado de dados **estruturados**, otimizado para análise e relatórios, com esquema rigidamente construído (schema-on-write). Ex.: DW de um varejista com vendas, estoques e dados de clientes. Pode ser entendido como uma "fonte da verdade" para análises estruturadas;

    - **Data Mart**: é um subconjunto de um DW, focado em uma **análise específica**/ em atender as necessidades analíticas de um setor. Ex.: Data Mart dos dados das vendas de um varejista. Pode ser entendido como uma  "loja de departamento" para necessidades específicas;

    - **Data Lake**: armazena dados brutos, **estruturados, semiestruturados e não estruturados**. A diferença básica entre um dado estruturado e um não-estruturado é que aqueles contam com um formato fixo, padronizado como tabelas com linhas e colunas, enquanto estes não seguem nenum modelo organizacinal para mapeamento dos dados, tais como vídeos, um pdf com parecer jurídico, um e-mail, etc.


???+ info "📊 Metodologias de Modelagem de Dados"
    | Aspecto                           | Transacional                                                   | Analítico (DW)                                                                     |
    | --------------------------------- | -------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
    | **Nível conceitual**              | Espelha o mundo real                                           | Dimensional                                                                        |
    | **Nível lógico (relacional)**     | Regras de normalização de dados com desnormalização deliberada | Tabelas de fatos e dimensões conforme melhores práticas                            |
    | **Nível lógico (não relacional)** | NoSQL, construções OODBMS, etc.                                | Cubos, bancos de dados colunares, etc.                                             |
    | **Nível físico**                  | Blocos/trilhas, distribuição MPP, etc.                         | Blocos/trilhas, distribuição MPP, buckets da AWS, HDFS NameNodes e DataNodes, etc. |
    | --------------------------------- | -------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
    | **Objetivo principal**            | Suporte a operações do dia a dia                               | Apoio à análise e tomada de decisão                                                |
    | **Modelo conceitual**             | Baseado no mundo real (entidades e relacionamentos)            | Modelo dimensional (fatos e dimensões)                                             |
    | **Normalização**                  | Normalizada (com possível desnormalização pontual)             | Desnormalizada para performance de leitura                                         |
    | **Estrutura relacional**          | Muitas tabelas com relacionamentos complexos                   | Tabelas de fatos e dimensões com chaves simples                                    |
    | **Performance**                   | Otimizada para escrita e transações rápidas                    | Otimizada para leitura e consultas complexas                                       |
    | **Atualizações**                  | Frequentes e em tempo real                                     | Atualizações periódicas (batch ou streaming controlado)                            |
    | **Tipo de dados**                 | Dados operacionais e atuais                                    | Dados históricos e agregados                                                       |
    | **Tecnologias comuns**            | RDBMS (MySQL, PostgreSQL, Oracle), NoSQL, OODBMS               | OLAP, bancos colunares, Hadoop, Redshift, BigQuery, etc.                           |
    | **Esquema típico**                | **Modelo Entidade-Relacionamento** (ER)                        | **Esquema Estrela** ou **Floco de Neve**                                           |
    | **Exemplo de uso**                | Sistema bancário, ERP, e-commerce                              | BI, dashboards, relatórios gerenciais, análise preditiva                           |


## Normalização de Banco de Dados Relacional

A normalização de banco de dados é um processo de organização de dados em tabelas para reduzir redundância e dependências, previnir anomalias, garantir a integridade referencial, melhorando a coesão e eficiência do banco de dados. São 3 as principais formas de normalização, sendo que cada uma delas têm consigo regras às quais o banco de dados deve obedecer. **É importante destacar que a normalização é aplicada principalmente em sistemas transacionais (operacionais), enquanto sistemas analíticos (como Data Warehouses) frequentemente utilizam desnormalização intencional para otimizar consultas complexas e melhorar a performance de leitura.**


### **🧱 1ª Forma Normal (1NF)** 
- cada linha deve ser única (chave primária)
- cada coluna/grupo deve ser atômico (não pode se repetir ou se dividir)

**Exemplo de violação:**

```
| ID | Nome | Telefones                  |
|----|------|---------------------------|
| 1  | João | (11)9999-9999, (11)8888-8888 |
```

problema: `Telefones` é uma coluna composta, pois pode ter mais de um telefone para o mesmo cliente.

**Exemplo de correção:**

```
| ID | Nome  | ID_TELEFONE |
|----|-------|-------------|
| 1  | João  | 1           |

| ID | ID_CLIENTE | Telefone      |
|----|------------|--------------|
| 1  | 1          | (11)9999-9999|
| 2  | 1          | (11)8888-8888|
```

Normalmente, as violações de 1NF são corrigidas através da criação de uma tabela para os atributos multivalorados.


### **🧱 2ª Forma Normal (2NF)**
- deve estar na 1NF
- todas as colunas não-chave devem depender da chave primária inteira ("no partial key dependencies")

**Exemplo de violação:**

```
| ID_Pedido | ID_Produto | Nome_Produto | Quantidade | Preco_Unitario |
|-----------|------------|--------------|------------|----------------|
| 1         | 101        | Notebook     | 2          | 1500.00        |
| 1         | 102        | Mouse        | 1          | 50.00          |
```

problema: `Nome_Produto` depende apenas de `ID_Produto`, mas não de `ID_Pedido` (chave primária)

**Exemplo de correção:**

```
| ID_Pedido | ID_Produto | Quantidade | Preco_Unitario |
|-----------|------------|------------|----------------|
| 1         | 101        | 2          | 1500.00        |
| 1         | 102        | 1          | 50.00          |

| ID_Produto | Nome_Produto |
|------------|--------------|
| 101        | Notebook     |
| 102        | Mouse        |
```

Normalmente, as violações de 2NF são corrigidas através do **reposicionamento do atributo não-chave em na tabela-entidade própria**, normalmente já existente. Caso não exista, deve-se criar uma nova tabela para o atributo não-chave.
    

### **🧱 3ª Forma Normal (3NF)**
- deve estar na 2NF
- não deve haver dependências transitivas entre os atributos
_obs: a dependência transitiva ocorre quando um atributo depende de outro atributo que depende de uma chave primária (A -> B -> C, onde A é a chave primária e C é a dependência transitiva, então A -> C é uma dependência transitiva)_

**Exemplo de violação:**

```
| ID | Nome | ID_Departamento | Nome_Departamento | Cidade_Departamento |
|----|------|-----------------|-------------------|--------------------|
| 1  | Ana  | 10              | TI                | São Paulo          |
| 2  | Bob  | 10              | TI                | São Paulo          |
```

problema: `Cidade_Departamento` depende de `Nome_Departamento`, mas não de `ID_Departamento`

**Exemplo de correção:**

```
| ID | Nome | ID_Departamento |
|----|------|-----------------|
| 1  | Ana  | 10              |
| 2  | Bob  | 10              |

| ID_Departamento | Nome_Departamento | Cidade_Departamento |
|-----------------|-------------------|--------------------|
| 10              | TI                | São Paulo          |
```

**Sob o ponto de vista conceitual, não há problema em haver violação das regras de normalização**, devendo esses problemas serem tratados sob o ponto de vista lógico.
  
