# 📝 Gabarito Consolidado — Git e GitHub Actions

> Módulo: **Git e GitHub Actions** (Rocketseat — Git e GitHub: Guia definitivo na era da IA) · fechado em 19/10/2026.
> Arquivo de **estudo** (caderno + repo). **Não sobe na base**: o fechamento da base fica limpo para a revisão de 30 dias (a partir de 18/11/2026).
> Cada questão traz: a pergunta, a resposta como foi enviada e a resposta corrigida e completa.
> **Nota de origem:** as respostas da Q2 e da Q3 foram coladas de outra fonte (texto de IA), não escritas à mão. Estão aqui como foram enviadas, para registro. Na revisão de 30 dias, vale refazer essas duas com as próprias palavras.

**Placar da correção:** Q1 parcial (a certa, b não respondida) · Q2 parcial · Q3 certa com ajustes.

---

## Questão 1 — Diagnóstico

**Pergunta.** Você cadastrou um *environment secret* chamado `API_URL` no environment `staging`. Seu workflow tem um job de deploy que chama `curl` usando esse secret, mas o job falha dizendo que nenhuma URL foi especificada. O nome do secret está certo e ele aparece cadastrado. (a) Qual é a causa mais provável e como você corrige? (b) Qual outra forma de cadastrar esse valor dispensaria essa correção, e o que você perderia ao usá-la?

**Resposta original**
- (a) "Pode ser que o secret estava em um environment secret, e o job não declarava o environment. Sem isso, o ambiente (e seus secrets) não é carregado automaticamente."
- (b) "Adicionar environment: <nome do environment> no job. Depois disso, funcionou."

**Resposta corrigida e completa**
- **(a) Causa e correção. ✅ Certa.** O secret está num **environment**, e o job não declarou qual environment usa. Sem a declaração, o ambiente (e os secrets dele) **não é carregado automaticamente**. O `curl` recebe o valor vazio e falha com "No URL specified" (`exit code 2`). A correção é declarar o environment no job:

```yaml
# Ilustrativo: nomes de job e de secret são exemplos
jobs:
  deploy:
    runs-on: ubuntu-latest
    environment: staging          # declara o environment: carrega os secrets dele
    steps:
      - run: curl "${{ secrets.API_URL }}"
```

- **(b) Outra forma de cadastro. ⚠️ Não respondida.** Você repetiu a correção do item (a). A pergunta pedia **outra forma de cadastrar o valor**: cadastrá-lo como secret (ou variável) de **repositório**, que vale em qualquer ambiente e dispensa o `environment:` no job.
  - **O que se perde:**
    - A **trava por ambiente**: qualquer workflow do repositório passa a poder usar o valor, em vez de ele ficar preso a um ambiente específico.
    - A **separação por ambiente** (dev, staging, prod): se vazar uma chave de repositório, o impacto é maior do que o de uma chave isolada num ambiente.
    - Se fosse variável em vez de secret, o valor ficaria **visível** (nada de dado sensível).

> **Reforço:** a regra de ouro é "usou environment secret, declare o `environment` no job". A escolha repositório × environment é uma escolha de **escopo**: repositório é mais prático, environment é mais seguro.

---

## Questão 2 — Escolha de trigger e de reuso

**Pergunta.** Sua equipe tem 4 repositórios com o mesmo bloco de CI (checkout, instalar dependências e rodar lint). Agora vocês querem adicionar duas rotinas: (i) uma análise de qualidade com IA, que demora e gera custo a cada execução; (ii) uma verificação de dependências feita toda semana. Em qual trigger você colocaria cada rotina (incluindo o lint) e por quê? E qual forma de reuso (Composite Action, Reusable Workflow ou JS Action) você usaria para o bloco repetido dos 4 repositórios? Justifique.

**Resposta original** *(colada de outra fonte; trechos introdutório e final omitidos, eram instruções do gerador sem conteúdo técnico)*

> **1. Definição dos Triggers (Gatilhos)**
>
> - **Bloco Repetido (Checkout, Dependências e Lint):**
>   - Trigger: `pull_request` e `push` (na branch principal, ex: `main`).
>   - Justificativa: O Lint é uma validação rápida e barata. Ele deve rodar em cada Pull Request para garantir que nenhum código saia dos padrões antes de ser mesclado, e na branch principal após o merge para garantir a integridade do código compartilhado.
> - **Rotina (i) — Análise de qualidade com IA (Demorada e com Custo):**
>   - Trigger: `pull_request` com filtro de tipo (ex: apenas quando o PR for aberto ou quando receber uma label específica como `ready-for-review`), ou idealmente apenas no `push` na branch principal (`main`).
>   - Justificativa: Como a ferramenta gera custos e é demorada, não deve rodar a cada commit/push em branches de desenvolvimento. Rodar apenas na branch principal pós-merge garante que o custo seja controlado e que apenas o código consolidado seja analisado. Se for estritamente necessário rodar antes do merge, o gatilho deve ser restrito (ex: via aprovação manual ou label no PR) para evitar execuções redundantes durante o desenvolvimento.
> - **Rotina (ii) — Verificação semanal de dependências:**
>   - Trigger: `schedule` (cronograma agendado, ex: `cron: '0 0 * * 1'` para toda segunda-feira à meia-noite).
>   - Justificativa: Vulnerabilidades de dependências e atualizações surgem independentemente de novas alterações no código. Rodar de forma agendada garante segurança contínua sem inflar o tempo de feedback dos desenvolvedores no dia a dia.
>
> **2. Escolha da Forma de Reuso**
>
> - **Abordagem Recomendada: Reusable Workflows (Workflows Reutilizáveis).**
>   - Justificativa: Como o bloco repetido envolve um processo completo de CI (que inclui passos estruturais como checkout, setup de ambiente/instalação e execução de scripts), os Reusable Workflows são ideais. Eles permitem centralizar um arquivo `.yml` inteiro em um repositório central de DevOps/Ferramentas. Os 4 repositórios precisam apenas "chamar" esse workflow (`uses: organizacao/repo-central/.github/workflows/ci.yml@v1`). Isso facilita a manutenção centralizada: se a versão do Node ou do Linter mudar, você altera em um só lugar e todos os 4 repositórios herdam a mudança imediatamente.
> - **Por que não as outras opções?**
>   - Composite Actions: São excelentes para agrupar passos (`steps`) sequenciais, mas rodam no contexto do repositório que as chama e não encapsulam segredos ou logs de forma tão isolada e robusta quanto os Reusable Workflows quando cruzamos fronteiras de múltiplos repositórios.
>   - JS Actions (Custom Actions em JavaScript): Exigem desenvolvimento de código Node.js, empacotamento (`dist/index.js`) e manutenção de um repositório de software dedicado. Seria um overengineering (complexidade desnecessária) para apenas executar comandos nativos de terminal como `npm install` e `npm run lint`.

**Resposta corrigida e completa**

*Triggers (regra do módulo: cada rotina no trigger que combina com seu custo e peso):*

| Rotina | Trigger correto | Por quê (como o módulo ensinou) |
|---|---|---|
| Lint (e o bloco de CI leve) | `push` | Lint é rápido e leve, o exemplo que a aula 02 dá para o push. |
| Análise de qualidade com IA | `pull_request` | Demora e gera custo, então fica no PR, onde roda no momento da revisão. Não repete a rotina leve do push. |
| Verificação de dependências | `schedule` (cron, semanal) | Uma dependência pode ser atualizada sem você saber, e o agendamento cobre esse ponto cego. |

- **Lint em `pull_request` e `push` ao mesmo tempo: ⚠️.** O professor alerta que a mesma rotina nos dois triggers roda o mesmo código várias vezes. A regra é leve no push e pesado no PR.
- **IA só depois do merge: ⚠️.** O módulo coloca a análise paga e pesada no PR, antes do merge. Rodar só na `main` acha o problema quando o código já está integrado. Os filtros por tipo de evento e por label da sua resposta não foram vistos no módulo, então confira na documentação do GitHub Actions.
- **Dependências no `schedule`: ✅ certo.**

*Forma de reuso:*
- O bloco repetido é uma **sequência de steps** (checkout → instalar dependências → lint). Pelo critério do módulo, isso pede **Composite Action**: ela reaproveita steps, e a regra prática da aula 03 é "se um bloco de steps se repete mais de duas vezes, vira uma action". Com 4 repositórios, o critério é atingido. A action pode ficar num repositório central e ser chamada com versão fixa (`org/repo/caminho@v1`).
- **Reusable Workflow** (`workflow_call`) reaproveita um **workflow inteiro**, indicado para padronizar pipelines de CI/CD ou orquestrar muitos jobs. É uma escolha **defensável** para este caso, mas seria a mais indicada se o objetivo fosse padronizar o pipeline completo entre os repositórios, não só um bloco de steps.
- **JS Action:** descartada, e o motivo está certo. A lógica é uma sequência simples de comandos, e a aula 04 manda manter YAML/Composite quando a execução é linear.
- Em qualquer caso: **fixar a versão** (`@v1`), nunca `@main`.
- ⚠️ O argumento da resposta original de que a Composite "não encapsula segredos nem logs de forma isolada" **não aparece no módulo**. Não o use como regra de estudo.

> **Reforço:** Composite Action = reaproveitar **steps**. Reusable Workflow = reaproveitar **o workflow inteiro**. JS Action = quando o YAML não dá conta de `if`/`for`/`switch`, API ou JSON.

---

## Questão 3 — Entrega segura

**Pergunta.** Um projeto tem deploy automático em produção a cada push na `main`. Numa sexta, uma automação com IA fez um push na `main` sem querer, e a produção foi atualizada antes de qualquer revisão. Descreva, usando o que o módulo ensinou, ao menos três mudanças de processo e de configuração que reduziriam esse risco (considere ambientes, validação antes do deploy, fluxos por branch e as permissões do job de deploy).

**Resposta original** *(colada de outra fonte)*

> 1. Regras de Proteção de Branch e Fluxo de PR Obrigatório
>
> - A Mudança: Configurar Branch Protection Rules na branch `main` para proibir qualquer `push` direto (seja de humanos ou de bots/automações).
> - Como reduz o risco: Toda e qualquer alteração que precise entrar na `main` deverá passar obrigatoriamente por um Pull Request (PR). A branch deve exigir pelo menos uma revisão humana (Code Review) e a aprovação bem-sucedida dos testes de CI (como o lint e testes unitários) antes que o botão de Merge seja liberado. Isso impede que commits acidentais ou automações sem supervisão atualizem a branch principal diretamente.
>
> 2. Separação de Ambientes com Aprovação Manual (Environments & Gates)
>
> - A Mudança: Criar ambientes distintos na esteira de deploy (ex: `Staging/Homologação` e `Production`). O deploy na `main` deve disparar automaticamente apenas para `Staging`. Para avançar para o ambiente de `Production`, deve-se configurar uma regra de proteção de ambiente (Environment Protection Rule) exigindo Aprovação Manual (Required Reviewers).
> - Como reduz o risco: Mesmo que um push acidental aconteça na `main`, a alteração ficará retida no ambiente de Staging. O deploy em produção só acontecerá após um responsável técnico revisar visualmente e aprovar o gatilho manualmente, eliminando deploys automáticos catastróficos, especialmente em momentos críticos como sextas-feiras.
>
> 3. Restrição de Permissões de Escrita do Bot e do Job de Deploy
>
> - A Mudança: Ajustar o escopo de permissões (least privilege). A automação baseada em IA não deve possuir credenciais compermissão de escrita (`write`) direta na branch `main`. Além disso, o Job que realiza o deploy deve utilizar o princípio de privilégio mínimo (usando o bloco `permissions` no workflow do GitHub Actions, por exemplo, limitando para `contents: read` ou exigindo OIDC para autenticação com o provedor de nuvem).
> - Como reduz o risco: Ao retirar o acesso de escrita da automação na branch principal, o bot simplesmente receberá um erro de "Acesso Negado" se tentar fazer um push direto. Se a IA precisar sugerir código, ela será forçada por configuração a abrir um Pull Request em uma branch secundária, onde o código poderá ser auditado com segurança.

**Resposta corrigida e completa** *(✅ certa, com dois ajustes)*

Mudanças que o módulo sustenta, com a aula de origem:

1. **Aprovação manual em algum ponto do fluxo** (aula 05). Um push acidental, inclusive de IA, dispara o gatilho e atualiza produção sem querer. Uma etapa manual evita isso, e o professor diz que ela é ainda mais importante porque hoje as entregas são muito rápidas.
2. **Separar ambientes** (aulas 05 e 07). Production é o mais seguro e não deve receber alteração sem controle; staging é onde o time testa. O environment aceita **regras de proteção** (reviewers, tempo de espera), que é o mecanismo para travar o avanço para produção.
3. **Validar antes de fazer deploy** (aula 05). O CI (testes, lint, review) vem antes do CD, e o deploy só segue se a validação passar.
4. **Fluxos diferentes por branch** (aula 05). Em vez de um único deploy para todas as branches, `main`, `staging` e `dev` têm fluxos distintos (ex.: deploy automático só em staging e production com aprovação). *(Este ponto faltou na resposta original.)*
5. **Menor privilégio** (aula 06). `permissions` começando do zero e adicionando só o necessário, por job. No exemplo do módulo, o job de deploy para o GitHub Pages precisou de `contents: read` e `pages: write`. A resposta original acertou o princípio, mas fixar "`contents: read`" como valor do deploy não vale: **o valor depende do que o job faz**.
6. **Branch protection na `main`** (módulo anterior, "GitHub e trabalho colaborativo"). Exigir PR, aprovação de terceiros e Code Scanning verde antes do merge. Está certo na resposta original e é o que impede o push direto.

- **Ajuste 1:** as `permissions` do workflow limitam o **`GITHUB_TOKEN`**. Se a IA usar outra credencial (um token pessoal, por exemplo), quem a segura é a branch protection do item 6, não o `permissions`. *(Raciocínio de apoio, não conteúdo de aula.)*
- **Ajuste 2:** o OIDC aparece no módulo só como a permissão `id-token`, uma integração para login mais seguro em ferramentas como a AWS, sem guardar credenciais fixas. Citar OIDC está correto, mas ele resolve **autenticação na nuvem**, não o problema do push acidental.

> **Reforço:** a defesa é em camadas. Branch protection impede o push direto; CI valida; environment com reviewers trava production; `permissions` mínimas limitam o estrago de qualquer action ou token.

---
**Salvar como:** `rocketseat-git-gabarito-modulo-github-actions.md` — no caderno (à mão) + repo. **Não** sobe na base de conhecimento (mantém o fechamento sem spoiler para a revisão de 30 dias).