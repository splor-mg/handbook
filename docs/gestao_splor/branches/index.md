---
title: Branches (Galhos)
---

# Branches (Galhos) 🌿

## O que é um Branch?

Um **branch** é como uma linha paralela de trabalho dentro do projeto. Ele permite que você desenvolva novas funcionalidades, faça correções ou testes sem afetar o código principal (main).

## Boas Práticas para Branches

- **Crie um branch sempre que for trabalhar em algo novo** (funcionalidade, correção, ajuste).
- **Não use acentos, espaços ou letras maiúsculas** no nome do branch. Use apenas letras minúsculas, números e hífens (-) para separar palavras. Exemplo: `feature-nova-tela`.
- **Mantenha o branch atualizado**: Se o desenvolvimento for demorado, traga as atualizações do main para o seu branch com frequência (`git merge main`). Isso evita conflitos na hora de juntar o código.
- **Quando terminar o trabalho, abra um Pull Request** para que outra pessoa possa revisar antes de juntar ao main.
- **Cada branch deve ter um objetivo claro**: evite misturar várias tarefas diferentes no mesmo branch.

## Fluxo Básico

1. **Crie um branch novo**:
   ```bash
   git checkout main
   git pull origin main
   git checkout -b nome-do-branch
   ```
2. **Faça suas alterações e commits**.
3. **Mantenha o branch atualizado**:
   ```bash
   git merge main
   ```
4. **Abra um Pull Request** assim que possível, mesmo que o trabalho ainda não esteja finalizado. Isso permite acompanhamento e feedback.
5. **Quando aprovado, faça o merge usando "squash and merge"** para manter o histórico do main limpo.

## Dicas para Iniciantes

- Não se preocupe em errar: branches servem justamente para testar ideias sem medo.
- Sempre peça revisão de alguém antes de juntar seu branch ao main.
- Se tiver dúvidas sobre nomes ou processos, pergunte para alguém mais experiente do time.

## Resumo Visual

```
main (tronco principal)
│
├── branch-novo-relatorio
│     └── (desenvolvimento)
│
├── branch-corrigir-bug
│     └── (desenvolvimento)
```

Quando o trabalho em um branch termina e é revisado, ele é "mesclado" (merge) de volta ao main.

---

Essas práticas ajudam a manter o projeto organizado, facilitam a colaboração e evitam problemas na hora de juntar o trabalho de todos.

---

> Para saber mais sobre branches e pull requests na prática, consulte o material complementar da trilha dev:
> [🎥 Vídeo 15 – Branch e Pull Request](https://splor-mg.github.io/trilha-dev/aulas/dia_05/dia_05/) 