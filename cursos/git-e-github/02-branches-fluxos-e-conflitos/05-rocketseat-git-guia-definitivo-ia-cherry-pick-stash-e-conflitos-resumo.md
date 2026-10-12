# 📌 Cherry Pick, Stash e um Pouco Sobre Conflitos

### 1. Conceito Central
Esta aula apresenta duas ferramentas que fogem do fluxo linear de "criar commit → trocar de branch → criar próximo commit": o **stash**, que permite guardar temporariamente alterações não commitadas para trocar de branch sem perder esse trabalho em progresso, e o **cherry-pick**, que permite trazer um commit específico de uma branch para outra, sem precisar integrar todo o histórico dela (como merge ou rebase fariam). Ambos resolvem problemas pontuais do dia a dia — urgência de trocar de contexto sem "sujar" o histórico com um commit incompleto, ou resgatar exatamente uma mudança específica — mas os dois têm um efeito colateral em comum: podem gerar **conflitos**, situações em que o Git não consegue decidir sozinho qual versão de um trecho de código deve prevalecer, exigindo intervenção manual do desenvolvedor.

### 2. Pontos-chave e Sintaxe

#### Subtema A — Git Stash
```bash
# Guarda as alterações não commitadas (working directory) sem criar commit,
# limpando o diretório de trabalho para permitir trocar de branch
git stash

# Lista os stashes salvos (funcionam como uma pilha: último criado, primeiro a aplicar)
git stash list

# Cria um stash com um nome/descrição customizado
git stash save -m "meu stash"

# Aplica o último stash, MANTENDO ele na lista
git stash apply

# Aplica o último stash e REMOVE ele da lista
git stash pop

# Remove um stash específico sem aplicá-lo
git stash drop stash@{0}

# Inclui também arquivos não rastreados (untracked) no stash
git stash -u
```
- O stash salva um WIP (*Working in Progress*) — um estado intermediário do trabalho, sem criar um novo ponto no histórico. A lógica por trás: um commit representa uma versão nova e "fechada" do código; se o trabalho ainda está incompleto, commitar não faz sentido semântico.
- O stash guarda arquivos modificados e na área de trabalho, mas **não** guarda arquivos não rastreados pelo Git por padrão (é preciso usar a flag `-u` para isso).
- ⚠️ **Ponto de atenção:** o stash **não substitui o commit**. Commits existem para dar rastreabilidade ao código; o stash é só um "corrimão" temporário para pausar um trabalho e retomá-lo depois — usos e motivações diferentes.
- 💡 **Dica:** não acumule stashes antigos. Se um stash não faz mais sentido, use `git stash drop`; se você quer preservar aquele código como backup, faça um commit em vez de manter um stash esquecido — não existe caso de uso prático para "coleção de stashes".
- ⚠️ **Ponto de atenção:** quanto mais tempo um stash fica pendente em relação à base de código, maior a chance de gerar conflito ao aplicá-lo — o ideal é aplicar o stash o quanto antes.

#### Subtema B — Cherry Pick
```bash
# Identifica o hash do commit desejado em outra branch
git log

# Vai para a branch que vai RECEBER o commit
git checkout main

# Traz apenas aquele commit específico para a branch atual,
# criando um commit NOVO (hash diferente, mesmo nome/mensagem)
git cherry-pick <hash-do-commit>

# Em caso de conflito durante o cherry-pick:
git cherry-pick --continue   # resolve o conflito manualmente e continua o processo
git cherry-pick --abort      # cancela o cherry-pick e volta ao estado anterior
```
- Diferente do merge/rebase (que trazem o histórico inteiro de uma branch), o cherry-pick traz **apenas um commit específico**, ignorando os demais.
- O commit resultante do cherry-pick tem o **mesmo nome/mensagem**, mas um **hash diferente** do commit original — ou seja, não é uma referência ao commit antigo, é uma cópia dele como novo ponto do histórico.
- ⚠️ **Ponto de atenção (o mais importante da aula):** cherry-pick duplica o histórico — se depois a branch de origem for integrada via merge/rebase, o mesmo commit (com o mesmo nome) vai aparecer duas vezes na branch de destino, com hashes diferentes. Isso prejudica a rastreabilidade que o versionamento deveria garantir.
- Casos de uso citados: corrigir bugs em produção rapidamente, aproveitar uma única feature específica sem trazer o restante dos commits, ou recuperar um commit que foi feito na branch errada.
- 💡 **Dica:** cherry-pick deve ser uma exceção, não uma prática recotidiana. Se você se vê fazendo cherry-picks com frequência, é sinal de que há muitos bugs no código ou de que o fluxo de lançamento de features do time não está saudável.

#### Sobre conflitos (introduzido nesta aula)
- Conflito ocorre quando o Git se depara com duas versões diferentes de um mesmo trecho de código e não consegue decidir sozinho qual delas deve prevalecer.
- Em commits normais, o Git entende a ordem cronológica (um commit substitui o anterior). No stash, isso não existe da mesma forma — o stash não é um "degrau" do histórico, então o Git não tem como julgar automaticamente qual versão (a do stash ou a do commit atual) é a correta, e aí surge o conflito.
- A resolução de conflitos em si será aprofundada em aulas futuras — esta aula só introduz o conceito para contextualizar por que stash e cherry-pick podem gerá-los.

### 3. 🧠 Raciocínio Lógico
- **Decisão sobre commitar ou usar stash:** Estou no meio de uma alteração incompleta → preciso trocar de branch urgentemente (ex: resolver um bug) → o trabalho ainda não é uma versão "fechada" → não faz sentido commitar → uso `git stash` para guardar o progresso sem criar um ponto falso no histórico → troco de branch, resolvo a urgência → volto à branch original → aplico o stash (`apply` ou `pop`) e retomo o trabalho exatamente de onde parei.
- **Decisão sobre merge/rebase vs. cherry-pick:** Preciso trazer mudanças de outra branch → quero **todo** o histórico dela? → SIM: uso merge (preserva histórico) ou rebase (linebida) → NÃO, quero só **um commit específico**: uso cherry-pick, aceitando que isso vai duplicar aquele commit no histórico (mesmo nome, hash novo) caso as branches sejam integradas depois.
- **Por que ambos podem gerar conflito:** sempre que o Git precisa decidir entre duas versões de um mesmo trecho de código sem ter um caminho cronológico claro entre elas (como acontece ao aplicar um stash antigo sobre uma base que já mudou, ou ao cherry-pickar um commit cujo contexto original já foi alterado na branch de destino), a decisão final tem que ser humana.

### 4. Links e Referências Oficiais
- **git stash:** guarda temporariamente alterações não commitadas. Documentação oficial: [git-stash](https://git-scm.com/docs/git-stash).
- **git cherry-pick:** aplica as alterações de um commit específico de outra branch como um novo commit. Documentação oficial: [git-cherry-pick](https://git-scm.com/docs/git-cherry-pick).
- **Conflito de merge (merge conflict):** situação em que o Git não consegue combinar automaticamente duas alterações concorrentes no mesmo trecho de um arquivo — conceito introduzido aqui e que será aprofundado em aulas futuras do módulo.
- **WIP (Working in Progress):** termo usado pelo Git para nomear automaticamente um stash, indicando que aquele conteúdo é um trabalho ainda não finalizado.

---
**Salvar como:** `NN-rocketseat-git-guia-definitivo-ia-cherry-pick-stash-e-conflitos-resumo.md` — no caderno (à mão) + repo do projeto (considere commitar na Frente 6, já que traz comandos de terminal reproduzíveis). **Não** sobe na base de conhecimento.

Me diga o número desta aula dentro do módulo "Branches, fluxos e conflitos" pra eu fechar o nome do arquivo (troca o `NN`).

### 🏛️ Conexão de Engenharia (Medallion & GCP)
O stash tem aplicação direta no dia a dia de um repositório Dataform: se você está no meio de uma alteração num model Silver e precisa urgentemente trocar de branch para corrigir um bug num model Gold já em produção, o `git stash` evita ter que commitar um SQLX incompleto (que poderia até quebrar a compilação do projeto se alguém puxar aquela branch por engano). Já o cherry-pick tem um caso de uso real, porém arriscado, em pipelines de dados: trazer isoladamente um commit de correção de um model específico para a branch principal antes de um deploy — mas, como a aula destaca, isso duplica o histórico, o que é especialmente problemático em Dataform/BigQuery porque dificulta rastrear qual commit efetivamente gerou uma mudança de schema ou de lógica de transformação em produção. Vale tratar cherry-pick como exceção também no seu projeto de portfólio (Frente 6), reservando-o para hotfixes pontuais na camada Gold, não como rotina.