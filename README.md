# Assessoria de Dados

 Esse repositório é o ponto central para centralização e coleta das informações necessárias para a gestão da Assessoria de Dados/SPLOR.



---
## Git - Boas Práticas

 Relação de boas práticas para utilização da ferramenta Git na Assessoria.

 ### Branch

  > - vide item 'novo branch' no tópico 'Pull Request (PR)';

  > - *critério para criação*: 
        >> 1) *revisão* - é necessário que ao menos uma pessoa reveja o código, idealmente diferente daquela que participou da elaboração das alterações em questão - no caso de realizadas por mais de uma pessoa conjuntamente/de forma síncrona;
        >> 2) *status* - esteja pronto para rodar no main/em produção.

  > - *nomenclatura*
   >> - i. não utilizar *acentuação* no nome do branch, nem *letas maiúsculas*;
   >> - ii. caso seja interessante **separar o nome** do branch em mais de uma palavra, utilize "-";

  > - *git merge main* - nos casos dos branches com duração de desenvolvimento e aplicação maiores, fazer merge do main para o branch com recorrência, de forma a evitar eventual quebra no que está sendo desenvolvido no branch;


 ### Clone - clonar

  > - *dependências* - após clonar a primeira vez, instalar dependências: `Rscript -e renv::install()`, ou `install.packages("renv")`;


 ### Comentários

  > - *edição* - apesar de ser possível editar um comentário em um issue, mesmo o issue tendo sido criado por outra pessoa, sugere-se que a edição seja previamente pautada em uma 'reunião gerencial';

 
 ### Commits
  > - *estruturação* - idealmente, separar alterações de *lógica* das alterações de *texto*. Isso tem o objetivo de facilitar a compreensão a respeito do que foi alterado, assim como para desfazer eventual equívoco.


 ### Issue

  > - *escopo* - diz respeito mais sobre a definição sobre "o quê" precisa ser feito; o "como" é algo mais próprio para o PR;

  > - *descrição* - diz "o porquê" das alterações

 
 ### Pull Request (PR)

  > - *novo branch* - quando se criar um novo 'branch' e houver as primeiras alterações, já criar o 'PR' para que a chefia possa ser notificada e acompanhar a evolução do projeto/repositório;

  > - *iniciar* o comentário associado ao 'PR' com "Closes #<número-do-issue-a-que-se-refere>";

  > - quando **criar** o 'PR', atribui-lo a si mesmo;

  > - quando **concluídas** as alterações no 'PR', atribuir um revisor;

  > - *merge* - quando for fazer o "merge", optar pelo **squash and merge**. Essa orientação tem o objetivo de não poluir o 'branch main' com todos os commits feitos ao longo do 'PR';

  > - lugar apropriado para discussão a respeito de "como" solucionar alguma demanda/desenvolvimento (issue);

  > - em regra, espera-se que um 'pull request' esteja relacionado a apenas um 'issue'; no entanto, é possível que, por falta de precisão/desconhecimento na criação de um 'issue', um PR resolva mais de um 'issue';


---
## Reuniões - Gerenciais e Status

 São duas as reuniões ordinárias na AID, uma 'gerencial', de equipe, e uma de 'status', com a(o) Subsecretária(o).

 > - **gravações** - as reuniões **gerenciais** são, em regra, gravadas e publicadas no canal da [AID no YouTube](https://studio.youtube.com/channel/), formato "unlisted" e, em seguida, seu link indicado/postado no respectivo issue da reunião;

 > - **pautas/atas** - o que for entendido como relevante e passível de registro em ata deverá ser feito pelo próprio membro da equipe;

 > - **ciente** - dar um "ciente" (joinha como comentário, não como react) no issue da reunião após finalizadas a reunião e respectivos registros;



---
## RH - Ponto Digital

 ### Contatos
  > - scpmso@planejamento.mg.gov.br : para questões envolvendo perícia médica;


---