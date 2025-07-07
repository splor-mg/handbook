---
title: Git
---

# Git — O superpoder da colaboração

Quando uma equipe está trabalhando conjuntamente na elaboração de um documento, um dos maiores desafios é coordenar a contribuição de todos e, talvez o maior deles, como, por raios, **nomear e saber qual, de fato, é a versão final desse arquivo**.

![Charge Final](../../assets/gestao-splor/charge-doc-final.gif)


Agora imagina só esse desafio se, ao invés de uma equipe, o **mundo todo** estivesse contribuindo para a elaboração desse documento?!

O Git nasceu justamente desse contexto. Em 2005, o desenvolvimento do kernel Linux, um dos **maiores projetos de código aberto do mundo**, estava enfrentando desafios com seu sistema de controle de versão — imagina, as contribuições do mundo todo eram geridas e processadas individualmente **por email!!**. Foi então que Linus Torvalds, o criador do Linux, se viu instigado a desenvolver uma **ferramenta para coordenar a colaboração e, com isso, o versionamento dos documentos produzidos coletivamente.** Ele precisava de algo que fosse rápido, facilmente distribuído e que permitisse a colaboração de milhares de desenvolvedores de forma simultânea e eficiente. **Eis que surgiu o Git!** e, desde sua criação, ele vem revolucionando a forma como equipes trabalham conjuntamente.

🔍 Dá só uma olhada nesse [TEDx de Clay Shirky](https://www.youtube.com/watch?v=CEN4XNth61o&t) sobre como o Git está contribuindo para **materializar o tão sonhado projeto de Governo Aberto**:

![type:video](https://www.youtube.com/embed/YSUJFYS3chs)

---

## Como o Git funciona?

Apesar de poder parecer complexo à primeira vista, as **operações básicas do Git são surpreendentemente simples**. Quando várias pessoas estão trabalhando juntas em um mesmo documento, normalmente enfrentamos pelo menos 4 grandes desafios (cada um deles, simplesmente **um potencial — e literal — pesadelo** sem uma ferramenta de colaboração):

1. **Qual é a versão mais recente do arquivo?** Ou: como recuperar uma **versão específica** do arquivo e retomar o trabalho a partir dela?
2. **Como documentar as alterações** de forma a informar às(aos) demais colaborador(as)es o que foi feito? Ou como perceber exatamente **o que mudou de uma versão para outra**?
3. Finalizadas as contribuições, como **notificar e enviar a todos a versão final do arquivo?** Por email? Por whatsapp? Pelo "drive"? Com qual nome???
4. **Por último, mas não menos importante, como juntar todas as contribuições feitas?**

O **Git resolve tudo** isso de forma automática e elegante com **4 operações básicas**:

1. **`git pull`** — Com esse comando, você **baixa as alterações mais recentes** feitas por outras pessoas;
2. Depois de fazer suas contribuições, você avisa ao Git que **terminou as alterações** (**`git add`**) e deixa uma **mensagem explicando** a mudança em seu contexto (**`git commit`**);
3. Você então pode **compartilhar suas contribuições** — sem precisar anexar a algum email, ou enviar por whatsapp, ou copiar para uma pasta de rede — tornando-as **imediatamente disponíveis para tod(as)os** com o simples comando: **`git push`**;
4. Por fim, a pessoa mantenedora responsável pelo documento, caso decida **aceitar as contribuições feitas**, basta dar um comando **`git merge`**.

Com esses comandos, o Git garante que: 

  - todos trabalhem sempre na versão mais atual; 
  - que nenhuma alteração se perca por descuido;
  - que a colaboração seja fluida, fácil de ser compartilhada e documentada, sem aquela bagunça de envio de arquivo por email, ou whatsapp, teams, drive...
  - qualquer versão do arquivo que já foi produzida é facilmente recuperável
  
Na SPLOR, o Git vem se tornando a base para nossa cultura de colaboração, transparência e inovação contínua. Se você está começando, não hesite em explorar [tutoriais](https://splor-mg.github.io/trilha-dev/), [pedir ajuda](https://github.com/splor-mg/atividades/issues), propor a [discussão de um novo tema](https://github.com/orgs/splor-mg/discussions/new/choose) ou [contribuir](https://github.com/orgs/splor-mg/discussions) para alguma discussão já existente.

---

## Como o versionamento opera sua mágica?

O modelo mental próprio do universo da gestão documental pode ser interpretada da seguinte forma: 

!!! info "Como o Git muda o jogo"
    <div style="display: flex; gap: 2em; flex-wrap: wrap; align-items: flex-start;">

    <div style="flex:1; min-width:220px; background:#f8f9fa; border-radius:8px; padding:1em; box-shadow:0 2px 8px #0001;">
      <h4 style="margin-top:0;"><br> 📁 Modelo tradicional: bidimensional<br></h4>
      <ul style="margin:0.5em 0 0 1.2em;">
        <li>Pastas</li>
        <li>Arquivos</li>
      </ul>
    </div>

    <div style="flex:1; min-width:220px; background:#e3f2fd; border-radius:8px; padding:1em; box-shadow:0 2px 8px #0001;">
      <h4 style="margin-top:0;"><br> 🚀 Modelo colaborativo: tridimensional<br></h4>
      <ul style="margin:0.5em 0 0 1.2em;">
        <li>Pastas</li>
        <li>Arquivos</li>
        <li><b>Tempo</b> <span style="font-size:1.2em;">⏰</span></li>
      </ul>
    </div>
    </div>

Isto é, uma vez introduzia a **dimensão tempo** como sendo intrínsica à gestão documental - marcado pelos "commits" (**`git commit`** visto acima) - torna-se trivial recuperar a exata **versão de um arquivo em um determinado momento no tempo**. Com isso, fica ainda mais claro o conceito de **versionamento** e sua gigantesca relevância no contexto organizacional: 

!!! Tip "Versionamento"
    **Versionamento** é registro da evolução de um arquivo/documento ao longo do tempo, permitindo rastreabilidade (quem fez?) e reprodutibilidade (o quê foi feito?) de um documento a qualquer momento.

---

## E aí, como usar o Git?

Você sabia que você **não precisa nem mesmo instalar um programa no computador** para começar a usar o Git??! Para compreender como isso funciona, o primeiro é saber a diferença entre Git e GitHub de forma bem simples:

*Você vai usar os dois juntos: Git para registrar, GitHub para compartilhar.*

!!! Tip "Git vs GitHub"
    🎥 **Para entender melhor essa diferença, não deixe de assistir ao [Vídeo 2 - Git e GitHub: qual a diferença?](https://splor-mg.github.io/trilha-dev/aulas/dia_01/dia_01/) da nossa [trilha-dev](https://splor-mg.github.io/trilha-dev/)!**

A plataforma do GitHub oferece uma ferramenta incrível chamada **GitHub Codespaces**, que é como ter um **computador virtual** rodando diretamente no seu navegador, com tudo que você precisa para programar já instalado e configurado. É como se você tivesse um "estúdio de desenvolvimento" completo, mas sem precisar instalar nada no seu computador!

!!! Tip "GitHub Codespace"
    🎥 **Quer saber como usar? Assista ao [Vídeo 5 - Usando o Codespace](https://splor-mg.github.io/trilha-dev/aulas/dia_02/dia_02/) da nossa trilha!**

### Para quem quer instalar no computador

Se você se sentir confortável com a instalação e quiser ter o Git rodando diretamente no seu computador, as orientações são simples e estão bem detalhadas no arquivo [Instalação e Configuração do Git](instalacao.md).

**Dica**: Comece com o Codespaces para experimentar, e depois, se quiser, instale o Git no seu computador. O importante é começar!