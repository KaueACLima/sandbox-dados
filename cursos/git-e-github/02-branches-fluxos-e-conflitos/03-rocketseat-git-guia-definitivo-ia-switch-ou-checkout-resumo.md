# 📌 Trocar de Branches de Forma Atualizada: Switch ou Checkout?

### 1. Conceito Central
Esta aula esclarece por que o Git tem dois comandos aparentemente redundantes para trocar de branch: `checkout` e `switch`. O `checkout` é um comando antigo e sobrecarregado — ele acumulou funcionalidades demais (trocar de branch, restaurar arquivos, navegar entre commits específicos), o que o tornou ambíguo e propenso a erros acidentais (ex: digitar errado e restaurar um arquivo sem querer, quando a intenção era trocar de branch). Como resposta a esse problema de design, o Git moderno dividiu essas responsabilidades em dois comandos mais específicos: `restore` (para restaurar arquivos) e `switch` (para trocar de branch ou navegar entre commits). O `checkout` continua funcionando e não foi removido, mas deixou de ser a opção recomendada — é um caso de evolução de uma ferramenta em direção a comandos mais explícitos e com responsabilidade única.

### 2. Pontos-chave e Sintaxe
```bash
# git checkout acumula 3 funções diferentes:

# 1) Trocar de branch
git checkout outra-branch

# 2) Restaurar um arquivo ao estado do último commit
git checkout -- conteudo.dbt

# 3) Ir para um commit específico usando o hash (obtido via git log)
git checkout <hash-do-commit>

# --- Alternativas modernas ---

# Restaurar arquivos: comando dedicado, sintaxe mais clara
git restore conteudo.dbt

# Navegar entre commits específicos (modo "destacado" do HEAD)
git switch --detach <hash-do-commit>

# Trocar de branch (equivalente direto ao checkout de branch)
git switch nova-branch

# Criar uma nova branch e já mudar para ela:
git checkout -b nova-branch2   # forma antiga
git switch -c nova-branch2     # forma moderna equivalente
```
- 💡 **Dica:** o `switch` é deliberadamente mais limitado que o `checkout` — ele não restaura arquivos. Essa limitação é a própria vantagem: o comando comunica exatamente uma intenção (trocar branch ou navegar entre commits), reduzindo a chance de ação acidental.
- ⚠️ **Ponto de atenção:** o `git switch --detach` coloca você num estado "destacado" (navegando por um commit específico, fora de qualquer branch) — isso é diferente de navegar entre branches normais com `git switch nome-da-branch`. A distinção fica explícita no próprio comando, o que não acontecia com o `checkout`.
- 🔎 **Observação:** a aula reforça que, na prática recomendada, não se deve navegar manualmente para commits antigos como forma de "desfazer" coisas — para isso existem comandos como `revert` (já visto em aulas anteriores). O uso de `switch --detach` é mais voltado a explorar/debugar versões antigas do código, não a operar sobre o histórico.
- O `checkout` ainda é aceitável de usar em projetos legados, com versões antigas do Git, ou por hábito de quem já o utiliza — não é um comando "errado", apenas não é mais o padrão recomendado.

### 3. 🧭 Implicações Práticas
- Se o objetivo é **trocar de branch**, o comando moderno recomendado é `git switch nome-da-branch`, não `git checkout`.
- Se o objetivo é **restaurar um arquivo** ao estado do último commit, o comando correto é `git restore arquivo`, não `git checkout -- arquivo`.
- Se o objetivo é **explorar um commit específico** (navegação histórica, não edição), usa-se `git switch --detach <hash>`.
- Em times ou ao ensinar alguém, adotar `switch`/`restore` reduz o risco de erros por ambiguidade de comando, já que cada um tem uma única responsabilidade.
- `checkout` continua funcional e não é depreciado — a escolha entre ele e `switch`/`restore` é uma questão de clareza e boas práticas modernas, não de compatibilidade.

### 4. Links e Referências Oficiais
- **git checkout:** comando legado multifuncional (troca branch, restaura arquivos, navega commits). Documentação oficial: [git-checkout](https://git-scm.com/docs/git-checkout).
- **git switch:** comando moderno dedicado exclusivamente à troca de branch ou navegação entre commits (`--detach`). Documentação oficial: [git-switch](https://git-scm.com/docs/git-switch).
- **git restore:** comando moderno dedicado à restauração de arquivos ao estado de um commit. Documentação oficial: [git-restore](https://git-scm.com/docs/git-restore).
- **git log:** usado para obter o hash de um commit, necessário para navegar até ele via `switch --detach` ou `checkout`.
- **git revert:** mencionado como a forma correta de desfazer mudanças no histórico, em vez de manipular commits diretamente via checkout/switch.

---
**Salvar como:** `NN-rocketseat-git-guia-definitivo-ia-switch-ou-checkout-resumo.md` — no caderno (à mão) + repo do projeto (considere commitar na Frente 6, já que traz comandos de terminal reproduzíveis). **Não** sobe na base de conhecimento.

Me diga o número desta aula dentro do módulo "Branches, fluxos e conflitos" pra eu fechar o nome do arquivo (troca o `NN`).

### 🏛️ Conexão de Engenharia (Medallion & GCP)
Não há uma camada de dado (Bronze/Silver/Gold) diretamente ligada a esta aula — o conteúdo é sobre higiene de comandos Git, não sobre processamento de dado em si, então forçar essa conexão seria artificial. A ligação honesta aqui é de **disciplina de versionamento**: ao trabalhar com Dataform/BigQuery, preferir `git switch`/`git restore` em vez do `checkout` multifuncional reduz o risco de um erro de comando acidental (por exemplo, restaurar um arquivo `.sqlx` sem querer, achando que estava trocando de branch) corromper silenciosamente um model em desenvolvimento. É um cuidado pequeno, mas relevante à medida que o repositório do seu projeto de portfólio (Frente 6) crescer e passar a ter múltiplas branches de feature simultâneas.