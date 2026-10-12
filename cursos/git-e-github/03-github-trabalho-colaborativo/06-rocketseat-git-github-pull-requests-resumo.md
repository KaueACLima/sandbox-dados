# 📌 Pull Requests (PR)

### 1. Conceito Central
O **Pull Request (PR)** é o mecanismo do GitHub para solicitar, revisar e aprovar mudanças de código antes que elas entrem na branch principal de um repositório — seja ele público (de outra pessoa) ou privado (do qual você faz parte). A analogia central da aula: é como pedir revisão de um texto antes dele ser publicado em um jornal, ou como controlar quem pode editar um documento compartilhado que, se ficasse totalmente aberto, qualquer pessoa poderia alterar livremente.

Na prática, em vez de alterar a `main` diretamente (branch que o cliente final usa), você trabalha em uma branch isolada (ex: `feature/login`), abre um PR dessa branch para a `main`, alguém revisa e aprova, e só então ocorre o **merge**. O PR tem interface e funcionalidade muito semelhantes às issues (descrição em Markdown, labels, assignees, milestones), mas serve a um propósito diferente: issue é tarefa/problema, PR é entrega de código para revisão.

### 2. Pontos-chave e Sintaxe
- **Por que existe o PR:** em repositórios públicos, você não consegue alterar o código diretamente se ele não é seu — o PR é a forma de solicitar essa mudança. Em repositórios privados dos quais você faz parte, o PR serve para garantir revisão antes do código entrar na branch principal.
- Cada PR carrega **registro de mudanças, commits e texto explicativo**, assim como as issues.
- Fluxo típico: criar uma branch → fazer commits nela → dar `git push` (criando a origin da branch, se ainda não existir) → abrir o PR dessa branch para a branch base (geralmente `main`) → revisores aprovam → ocorre o **merge**.
- Na tela de criação do PR, o GitHub mostra se as branches **"are able to merge"** automaticamente ou se vão gerar conflito.
- Campos configuráveis ao abrir um PR (muito parecidos com os de issue):
  - **Reviewers**: pessoas (ou IA, como o GitHub Copilot) responsáveis por revisar e aprovar.
  - **Assignees**: responsáveis pela entrega do código do PR.
  - **Labels**: categorização (ex: `documentation`).
  - **Projects**: vincula o PR a um quadro de gestão de tarefas (GitHub Projects).
  - **Milestone**: vincula o PR a uma meta do projeto.
  - **Linkar issues**: um PR pode ser vinculado a uma ou mais issues, de forma que, ao ser concluído (merge), a issue vinculada é fechada automaticamente — issue e PR funcionam em conjunto, não isoladamente.
- A numeração de PRs no GitHub **continua a sequência das issues** (não começa do zero) — ambos compartilham a mesma contagem por proximidade de função.
- **Tipos de merge disponíveis ao finalizar um PR:**
  - **Create a merge commit** (padrão/recomendado): cria um commit específico que sinaliza que ocorreu o merge.
  - **Squash and merge**: adiciona as mudanças na branch base sem um commit de merge visível — não recomendado, pois esconde o histórico de que houve um merge.
  - **Rebase and merge**: aplica o conceito de rebase (já visto em aulas anteriores) para integrar as mudanças.
- Depois do merge, a branch da feature **continua existindo no origin** (pode ser apagada manualmente), mas **não é removida da máquina local**.
- Após o merge feito pela interface do GitHub, é necessário dar `git pull` na máquina local (estando na branch `main`) para baixar o commit de merge que já está no remoto — senão um `git push` posterior gera conflito, pois a `main` remota está à frente da local.
- **Branch Protection Rules** (Settings → Branches): regras que reforçam comportamentos de segurança em branches sensíveis como a `main`. Destaques trazidos na aula:
  - **Require a pull request before merging**: bloqueia push direto na branch protegida — toda mudança tem que vir via PR.
  - **Exigir número mínimo de aprovações** antes do merge (ex: 1 aprovação).
  - **A aprovação precisa vir de alguém diferente de quem fez o push** (não é possível auto-aprovar o próprio PR).
  - Também é possível exigir aprovação do **code owner**, de **times específicos**, e exigir que o PR seja reaprovado sempre que novos commits forem enviados após uma aprovação anterior.
- 💡 **Dica:** a combinação de "exigir PR antes de merge" + "exigir aprovação de outra pessoa" é o que garante, na prática, que nenhum código entre na `main` sem revisão humana — mesmo que o autor tenha permissão de escrita no repositório.

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[Branch de feature (ex: feature/login)] -> commits feitos localmente
   -> git push (cria origin da branch, se necessário)
   -> Abrir Pull Request (branch feature -> branch main)
        -> GitHub verifica: able to merge automaticamente?
             SIM -> segue para revisão
             NÃO -> sinaliza conflito a ser resolvido antes
        -> Passa por Branch Protection Rules da main:
             -> Requer PR (bloqueia push direto)? 
             -> Requer N aprovações de outra pessoa?
             -> Aprovado por code owner / time específico?
                  TODAS atendidas -> PR pode ser mergeado
                  ALGUMA pendente -> merge bloqueado até resolver
        -> Reviewer aprova -> Merge (commit de merge / squash / rebase)
             -> [Branch main atualizada no GitHub]
             -> git pull necessário na máquina local para sincronizar
```

### 4. Links e Referências Oficiais
- **Pull Requests:** [About pull requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) — documentação oficial sobre criação, revisão e merge de pull requests.
- **Branch Protection Rules:** [About protected branches](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches) — detalha as regras de proteção como aprovação obrigatória e bloqueio de push direto.
- **Tipos de merge (merge, squash, rebase):** [About pull request merges](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges) — explica as diferenças entre merge commit, squash merge e rebase merge.
- **Vincular issues a pull requests:** [Linking a pull request to an issue](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue) — documentação sobre fechar issues automaticamente via PR.

---
**Salvar como:** `06-rocketseat-git-github-pull-requests-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.