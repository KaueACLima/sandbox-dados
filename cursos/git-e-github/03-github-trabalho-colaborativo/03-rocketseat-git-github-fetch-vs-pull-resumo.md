# 📌 Git fetch vs Git pull

### 1. Conceito Central
Esta aula aprofunda o comando `git pull` visto anteriormente, mostrando que ele na verdade é a combinação de dois passos: um `git fetch` seguido de um `git merge` automático. O `fetch` **busca** as informações que existem no repositório remoto (quais commits novos existem lá) e as traz para a máquina local, mas **não aplica nada** — o Git local fica sabendo que está desatualizado, porém o conteúdo dos commits novos ainda não foi incorporado ao histórico local. Já o `pull` faz o fetch **e** aplica automaticamente o merge, unindo o que veio do remoto com o que já existe localmente.

### 2. Pontos-chave e Sintaxe
- **Por que o Git não avisa sozinho sobre mudanças remotas:** o Git local não fica monitorando o repositório remoto continuamente — ele só verifica e traz informações quando um comando como `fetch` ou `pull` é executado.
- **`git fetch`:** busca no repositório remoto (GitHub) os objetos/commits que existem lá e que a máquina local ainda não tem, e só *dá esse contexto* ao Git local — sem mesclar nada no histórico de trabalho.
- **`git pull`:** por baixo dos panos, executa um `fetch` e, em seguida, um `git merge` automático, deixando o repositório local nivelado com o remoto (o mesmo conceito de merge já visto ao falar de branches — a união de duas linhas de commits).
- ⚠️ **Ponto de atenção:** usar `pull` direto é cômodo na maioria dos casos (deixa os dois lados sincronizados automaticamente), mas tem uma limitação: se você quiser **ver** as mudanças remotas sem aplicá-las de imediato — por exemplo, para revisar um código antes de mesclar — o `pull` não serve, porque ele já mescla sozinho. É aí que o `fetch` isolado se torna útil.
- 🔎 **Observação:** depois de um `git fetch`, comandos como `git diff origin/main` passam a funcionar e mostrar diferenças, porque agora o Git local tem o contexto das mudanças remotas — antes do fetch, o mesmo comando não retornava nenhum resultado.
- **Comandos usados na aula:**

```bash
# Inicializar um repositório do zero
git init
git add .
git commit -m "primeiro commit"

# Conectar ao GitHub e subir (três comandos oferecidos pelo GitHub ao criar o repo vazio)
git remote add origin <url-do-repositorio>
git branch -M main
git push -u origin main

# Ver diferenças entre o repositório local e o remoto
git diff origin/main

# Buscar informações novas do remoto SEM aplicar (sem merge)
git fetch

# Buscar informações novas do remoto E aplicar automaticamente (fetch + merge)
git pull
```
- **Fluxo demonstrado na aula:** o professor cria um 3º commit diretamente no GitHub (via interface web). No Git local, ainda restam apenas 2 commits. Um `git diff origin/main` nesse ponto não retorna nada, porque o Git local ainda não tem contexto da mudança. Depois de rodar `git fetch`, o `git diff origin/main` passa a mostrar a diferença (o 3º arquivo), mas o commit ainda não está aplicado ao histórico local. Rodando `git pull` em seguida, o merge é aplicado e o repositório fica novamente "up to date".
- 💡 **Dica:** "up to date" é a mensagem que o Git mostra quando o repositório local e o remoto têm exatamente os mesmos commits — ela só muda para "desatualizado" depois que um `fetch` ou `pull` revela que existem commits novos no remoto.

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[Repositório remoto (GitHub) recebe novo commit] -> [Repositório local ainda não sabe disso]
  -> Quero só ver o que mudou sem aplicar?
     -> SIM: git fetch -> [traz contexto dos commits novos] -> [git local sabe que está desatualizado, mas histórico local permanece igual] -> git diff origin/main agora mostra diferenças
     -> NÃO, quero já sincronizar: git pull -> [executa fetch + merge automaticamente] -> [histórico local atualizado, "up to date" novamente]

Se depois de um fetch eu quiser aplicar as mudanças:
  -> git merge (manual) OU simplesmente rodar git pull de novo -> [aplica o que já foi buscado pelo fetch]
```

### 4. Links e Referências Oficiais
- **git fetch** — busca atualizações do repositório remoto sem aplicá-las ao histórico local. Documentação: [git-scm.com/docs/git-fetch](https://git-scm.com/docs/git-fetch).
- **git pull** — combinação de `fetch` + `merge` automático. Documentação: [git-scm.com/docs/git-pull](https://git-scm.com/docs/git-pull).
- **git merge** — une duas branches (ou o conteúdo buscado pelo fetch com a branch local), conceito já visto em aulas anteriores sobre branches. Documentação: [git-scm.com/docs/git-merge](https://git-scm.com/docs/git-merge).
- **git diff** — mostra diferenças entre dois pontos do histórico (ex: local vs. `origin/main`). Documentação: [git-scm.com/docs/git-diff](https://git-scm.com/docs/git-diff).
- **git init** — inicializa um repositório Git do zero numa pasta. Documentação: [git-scm.com/docs/git-init](https://git-scm.com/docs/git-init).

### 🏛️ Conexão de Engenharia (Medallion & GCP)
Assim como na aula anterior, este conteúdo é infraestrutura de versionamento, não processamento de dado — não há uma camada Bronze/Silver/Gold ou serviço GCP para conectar honestamente aqui. A relevância prática está na **Frente 6 (Projeto de Portfólio)**: entender a diferença entre `fetch` (buscar sem aplicar) e `pull` (buscar e aplicar) é especialmente útil quando o projeto crescer e envolver revisão de código antes de mesclar mudanças — por exemplo, ao trabalhar em colaboração ou revisar um código gerado por IA antes de integrá-lo ao histórico do repositório.

---
**Salvar como:** `NN-rocketseat-git-github-fetch-vs-pull-resumo.md` — no caderno (à mão) + repo do projeto (por ser aula de comandos, considere commitar na Frente 6). **Não** sobe na base de conhecimento.

Me diz o número desta aula dentro do módulo "GitHub e trabalho colaborativo" pra eu fechar o `NN` do nome — não vou chutar.