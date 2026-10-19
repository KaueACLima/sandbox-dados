# 📌 Como Armazenar Actions Reutilizáveis e Escaláveis (e JS Actions)

### 1. Conceito Central
Existem **três formas de reutilizar automação** no GitHub Actions. A escolha depende do contexto de uso: **Composite Actions**, **Reusable Workflows** e **JS Actions** (actions customizadas escritas em JavaScript, não em YAML puro).

A aula também cobre **onde guardar e como versionar** essas actions (na pasta `.github` do projeto ou em repositório à parte), quais **boas práticas** evitam que o reuso vire dor de cabeça, e **quando o YAML não basta** e vale migrar para JavaScript.

### 2. Pontos-chave e Sintaxe
#### As 3 formas de reuso e quando usar cada uma
- **Composite Actions:** reaproveitam **steps**. É a forma mais comum, geralmente dentro do próprio repositório. Ideal para **lógica procedural simples** (baseada em procedimento: passo a passo, constante, com pouca variação).
  - Use para steps como build, install e checkout repetidos em vários projetos (ex.: monorepo, ou consultoria com vários clientes).
- **Reusable Workflows** (acionados por `workflow_call`; a transcrição grafa "workflow call"): reaproveitam **workflows inteiros**. Menos comuns que as Composite.
  - Use para **padronizar CI/CD** entre projetos ou **orquestrar muitos jobs** (fluxo cadenciado, com muitos níveis).
- **JS Actions:** mais poder e mais complexidade. Use quando há **lógica de programação** que o YAML não supre (`for`, `if`, `switch`).

#### Como criar e usar
- A estrutura é a mesma das aulas anteriores. Fica na pasta de actions do projeto (`.github/actions/...`), com nome, descrição, input e o que roda.
- **Composite:** chamada com `uses`, mas apontando para o **caminho da pasta** em vez de uma action externa. Ex.: uma action de setup do Node usada por vários projetos da empresa.
- **Reusable workflow:** definido de forma parecida, mas o reuso é do workflow inteiro (nível de abstração maior). Ao ser chamado, recebe informações (ex.: versão do Node) e executa os processos (reserva a versão, faz o setup). Quem chama passa a versão como input, dentro de um job.

```yaml
# Reconstrução ilustrativa do que foi descrito (a aula mostra o YAML na tela; as chaves exatas não são ditas em voz alta)
# --- Composite action, usada do mesmo repo apontando para a pasta ---
# - uses: ./.github/actions/setup-node
#   with:
#     nodeVersion: 22

# --- Reusable workflow ---
# on: workflow_call            # o workflow aceita ser chamado por outro
#   inputs: nodeVersion        # recebe a versão do Node como parâmetro
# jobs: ... faz o setup do Node com a versão recebida

# --- De outro repositório (org ou usuário), com versão fixa ---
# uses: <org-ou-usuario>/<repositorio>/<caminho>@v1   # @v1, nunca @main
```
> O professor comenta que errou uma formatação do YAML na gravação, mas diz que o importante são as boas práticas.

#### Boas práticas
- **Parametrização forte:** a action roda em ambientes e circunstâncias diferentes, então deve receber parâmetros. Se `22` ficar fixo e o projeto passar para outra versão, você perde o reuso, que é o objetivo.
- **Nunca *hardcodar*:** não deixe valores explícitos dentro do código. Ex.: não presuma que sempre roda em produção; receba o ambiente por input.
- **Evite lógica complexa no YAML:** muitas condicionais e scripts longos são sinal para migrar para JS Action.
- **Versionamento:** use repositório à parte (`org/usuario` + repositório + pasta) e **fixe a versão** (`@v1`), nunca `@main`.
- **Isolamento:** a action chamada não deve depender de arquivos do repositório onde está guardada. Quem chama só **pega a resposta** dela.
- **Não assumir estrutura de arquivos:** se a action fizer `npm install` na pasta `front-end` e o projeto chamar a pasta de `web`, ela quebra. Receba o **nome da pasta como input**.
- **Encadeamento (actions dentro de actions):** uma action precisa dizer o que **devolve** (outputs), para a outra usar o resultado no resto da automação.
- **Organização:** a pasta `.github` guarda tanto actions quanto workflows reutilizáveis (ex.: o CD). Isso é muito útil em **monorepos** (um repositório grande com vários projetos) e em consultorias (ex.: 15 clientes com o mesmo CI/CD): publica-se **uma vez** em repositório externo que serve a todos, em vez de copiar, colar e testar de novo a cada projeto.
- Para vários projetos novos, mova as actions para uma org ou repositório pessoal seu ou do time.

#### Problemas comuns
- ⚠️ **Action genérica demais** (ex.: "CI") é difícil de entender: o que ela contempla, testes, lint? Documente na própria action ou em documentação de empresa.
- ⚠️ **Falta de versionamento quebra pipelines:** se 5 projetos dependem de uma action sem versão, uma mudança que quebra derruba todos. Lance **nova versão** quando a mudança puder quebrar a anterior.
- ⚠️ **Dependência implícita do repositório** torna impossível reutilizar. Se algo do repo ou externo ficar indisponível, os projetos quebram.
- ⚠️ **YAML gigante** (ex.: mil linhas) não é reutilizável, deixa casos sem atender e dificulta manutenção e escalabilidade.
- 💡 **O CI/CD é a base, não o produto.** O usuário final não vê o GitHub Actions. Se o reuso falha, a automação vira gargalo, quando deveria dar uma base sólida.
- 🔎 **Arquitetura em camadas:** você pode combinar tudo: uma action lógica que usa Composite Actions, que usam blocos de workflows, orquestrando JS Actions com lógica complexa.

#### JS Actions
- **Quando usar:** quando o YAML tem limitação. Situações típicas:
  - processar dados (JSON, APIs, arquivos);
  - lógica condicional complexa (`if`, `switch`, `for`);
  - integrar com serviço externo;
  - manipular outputs dinamicamente.
- **Sinais de que é hora:** muitos `if` no YAML, muitos scripts Bash (comandos de terminal), YAML virando "gambiarra". JavaScript em action **não é gambiarra**: é uma forma correta de fazer, e mais escalável.
- **Estrutura de arquivos** (diferente do YAML puro): o YAML da action + `index.js` (a lógica) + `package.json` (arquivo do Node que acompanha o projeto).
  - O YAML traz as informações gerais: nome, descrição, input, output, e que roda no **Node 20** usando o arquivo principal.
  - O `index.js` tem o núcleo da lógica e usa o `core`, ferramenta de `@actions` para usar JavaScript dentro das actions.
- **Exemplo da aula (um "hello world"):** uma função `run` tenta pegar o nome (input), monta uma mensagem e a devolve (output). Se der erro dentro do `try`, informa qual foi o erro.
- **Uso no workflow:** igual a uma action reutilizável. Ganha um `id` (identificador único), recebe a variável `nome` por `with`, e um step seguinte lê a mensagem de saída.

```yaml
# Reconstrução ilustrativa (nomes exatos não ditos no áudio)
# action.yml  -> informações gerais da action
name: Minha action
description: Devolve uma mensagem
inputs:
  nome:
    description: nome a saudar
outputs:
  mensagem:
    description: mensagem devolvida
runs:
  using: node20        # roda no Node 20
  main: index.js       # arquivo com a lógica
```
```javascript
// index.js -> núcleo da lógica
const core = require('@actions/core');   // ferramenta para usar JS dentro das actions

function run() {
  try {
    const nome = core.getInput('nome');          // lê o input definido no YAML
    const mensagem = `Olá, ${nome}`;             // texto ilustrativo (não citado no áudio)
    core.setOutput('mensagem', mensagem);        // devolve o valor
  } catch (error) {
    core.setFailed(error.message);               // falha controlada: informa o erro e interrompe o job
  }
}
run();
```
```yaml
# No workflow
steps:
  - id: saudacao            # identificador único da action
    uses: ./.github/actions/minha-action
    with:
      nome: Fulano          # valor ilustrativo
  - run: echo "${{ steps.saudacao.outputs.mensagem }}"   # usa a saída
```
> O professor não mostra o código completo em voz alta. A reconstrução acima segue o que ele descreveu.

- **Como funciona por dentro:** o workflow chama a action -> o GitHub executa o Node -> o arquivo roda -> inputs e outputs são unidos e retornados.
- **Pontos importantes:**
  - defina as **entradas no YAML** e puxe no JavaScript;
  - **sempre devolva valores**;
  - tenha **falhas controladas** (`try/catch`): a falha interrompe o job. Em um job de consulta de IA, por exemplo, isso cancela antes de uma chamada pesada que geraria custo à toa;
  - **logs:** `core.info` para mensagens, `core.warning` para avisos, `core.error` para erros.
- **Vantagens:** mais poderoso que o YAML, bom com loops e condicionais, manipula dados de forma estruturada, código organizado e funções reutilizáveis, e é **testável** (com Jest ou outra biblioteca de testes).
- **Quando não usar:** sequência simples e linear de comandos (a "receita de bolo": quebra o ovo, mistura, assa). Fique com YAML, Composite ou workflow. A JS Action faz sentido quando há repetição condicional (ex.: "enquanto não ficar homogêneo, continue misturando", um `while`).
- 💡 **Analogia da aula:** se o YAML é a receita de bolo, o JavaScript é o mercado, com muitas variantes possíveis (fila cheia ou vazia). Por isso a complexidade maior e o cuidado com erros.
- 🔎 **TypeScript** (JavaScript com tipos): dá para escrever em TS e fazer o *build* para gerar o JS. O professor cita como tema avançado e fora do foco.
- 🔎 **Observação:** o exemplo desta aula usa Node 20, versão que a aula 01 mostrou como depreciada no aviso do `checkout@v4`. Confira a versão ao criar a sua.

### 3. 🏗️ Arquitetura / Diagrama Lógico
**Qual forma de reuso escolher:**
```
[Quero reutilizar automação] -> O que preciso?
   Reaproveitar steps simples e lineares (build, install, checkout) -> [Composite Action]
   Padronizar CI/CD ou orquestrar muitos jobs -> [Reusable Workflow (workflow_call)]
   Lógica de programação (for / if / switch, API, JSON, arquivos) -> [JS Action]
```

**Quando migrar do YAML para JS:**
```
[YAML está ficando assim?] -> Muitos ifs / muitos scripts Bash / "gambiarra"?
   SIM: [migrar para JS Action]
   NÃO (sequência simples e linear): [manter YAML / Composite / workflow]
```

**Arquitetura em camadas (combinação):**
```
[Action de lógica] -> usa [Composite Action] -> usa [blocos de Reusable Workflow]
                   -> orquestra [JS Actions com lógica complexa]
```

**Distribuição e versionamento:**
```
[Actions/workflows em repositório externo (org ou usuário)]
   <- chamado por [Projeto 1] [Projeto 2] ... [Projeto N], via uses: org/repo/caminho@v1
Mudança que pode quebrar? -> SIM: [lançar nova versão (@v2)] -> projetos antigos continuam estáveis
```

**Execução de uma JS Action:**
```
[Workflow chama a action (id + with)] -> [GitHub executa o Node] -> [index.js roda com core.getInput]
-> Deu erro no try? SIM: [catch: informa o erro e interrompe o job] | NÃO: [core.setOutput]
-> [Outputs retornam] -> [Step seguinte usa o output]
```

### 4. Links e Referências Oficiais
- [**GitHub Actions**](https://docs.github.com/actions): documentação oficial. Lá estão a criação de actions (Composite, Docker, JavaScript) e os reusable workflows.
- [**actions/toolkit**](https://github.com/actions/toolkit): repositório do `@actions/core`, o `core` usado no JS (`getInput`, `setOutput`, `info`, `warning`, `error`).
- [**Node.js**](https://nodejs.org): ambiente que executa as JS Actions. O `package.json` é o arquivo do Node que acompanha a automação.
- [**Jest**](https://jestjs.io): biblioteca de testes citada para testar o JavaScript da action.
- [**TypeScript**](https://www.typescriptlang.org): JavaScript com tipos. Dá para escrever a action em TS e fazer o build para gerar o JS.
- **Monorepo:** repositório grande com vários projetos dentro. É onde a organização em `.github` mais ajuda.
- **Hardcode:** deixar valores fixos no código. A aula orienta passar tudo por input.
- **`workflow_call`:** evento que permite um workflow ser chamado por outro. Vale conferir a sintaxe na documentação do GitHub Actions.

---
**Salvar como:** `04-rocketseat-git-github-actions-armazenar-actions-reutilizaveis-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.