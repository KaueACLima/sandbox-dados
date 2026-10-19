# 📌 Segurança e Boas Práticas no GitHub Actions

### 1. Conceito Central
Automação mal protegida é risco: credenciais expostas, permissões demais e actions que mudam sem aviso. Esta aula junta três eixos de segurança no GitHub Actions: **secrets** (proteger credenciais), **permissões mínimas** (o princípio do menor privilégio) e **versionamento fixo das actions** (nunca depender de código que muda sozinho).

Ideia de fundo: proteger não é só esconder o valor no código. É garantir que ele **nunca apareça em lugar nenhum** (código, logs, commits, revisões) e que cada parte da automação tenha **só o acesso de que precisa**.

### 2. Pontos-chave e Sintaxe
#### Secrets (credenciais)
- **Secret:** variável de **valor oculto**, para informação que precisa ser protegida: chave de API, dado de banco, chave de serviço pago (ex.: AWS), bot, automação.
- **Nunca *hardcodar* credenciais** (escrever o valor direto na linha do código, onde fica público). Use os secrets do próprio GitHub.
- **Nomeie com clareza** (ex.: o nome deixa claro que é a *access key* da AWS), para localizar depois no painel do serviço.
- Esconder a chave não é esconder que existe uma chamada de API no fluxo. O ponto é a chave não estar explícita no código.
- **Separe por ambiente** (dev, staging, prod): se vazar um, o impacto é bem menor do que vazar o de produção.
- **Environment secrets:** use sempre que a informação tiver o mínimo de necessidade de ser mais segura.

#### Onde o secret pode vazar além do código
- **Logs:** mesmo sem a URL do banco no código, uma mensagem de log como "tentando conectar na URL ..." a expõe. Atenção especial aos **logs de erro**, que costumam mostrar a informação.
- **Commits:** remover a chave de um commit não basta se ela está em **commits anteriores**; quem buscar o histórico a encontra.
- **Revisões:** comentário em PR (inclusive de IA) que traga a informação. Apague para que o valor não apareça em lugar nenhum.
- **Auditoria de logs:**
  - nunca mostre secret com `echo`;
  - revise logs de falha;
  - use **mascaramento** (ferramentas que trocam o valor por `***`).
- 💡 **Trate logs como se qualquer pessoa pudesse vê-los**, mesmo que sejam "internos do time".

#### Permissões mínimas (`GITHUB_TOKEN`)
- A cada execução, o GitHub entrega uma **chave temporária** (`GITHUB_TOKEN`) ao workflow. As **permissões definem o que essa chave pode abrir**. Ela vem com permissões padrão, e o certo é **reduzir ao mínimo necessário**.
- **Granularidade:** defina por workflow (arquivo todo) ou **por job**. Ex.: o job de build só lê o conteúdo do código.
- **Princípio do menor privilégio** (nomeado aqui por mim; o professor descreve a ideia sem dar o nome): cada parte roda com o mínimo que precisa.
- ⚠️ **Actions de terceiros herdam as permissões do workflow.** Se houver exagero, uma action maliciosa pode alterar código, abrir pull requests ou vazar dados.
- **Exemplo prático:** um workflow de CI só **lê** o código para testar, então não faz sentido ter escrita em `contents`.
- 💡 **Analogias da aula:**
  - o app de jogo que pede acesso à lista de contatos: "por que precisa disso?";
  - permissão em excesso é como deixar as portas da casa abertas: talvez nada aconteça hoje, mas você está convidando o problema.

#### Permissões disponíveis
- **`contents`:** acesso ao repositório. Read: clonar. Write: commits, pushes e releases.
- **`pull-requests`:** comentar, aprovar ou criar PRs (ex.: bot que comenta resultado de testes no PR).
- **`issues`:** criar, gerenciar, comentar ou fechar issues.
- **`actions`:** cancelar runs de workflow ou disparar workflows externos.
- **`id-token`** (a transcrição grafa "Edge Token"): usado com **OIDC**, integração para login mais seguro em ferramentas como a AWS, sem armazenar credenciais fixas.
- **`checks`:** os *status checks* de commit. Ex.: publicar o resultado de um CI como "all checks have passed".
- **`statuses`:** atualizar o status de um commit. O professor cita quatro estados: sucesso, falha, pendente (ainda carregando) e cancelado (um run em andamento pode ser cancelado). Se um dos processos falha, o status vira falha.
- **`packages`:** gerenciar pacotes no **GitHub Packages** (armazenar pacotes junto do código). O professor diz que é **pouco usado** no mercado, nunca usou e não aprofunda. Se precisar, vá à documentação.
- **`security-events`:** usado por ferramentas de segurança para acessar informações de qualidade e segurança do GitHub.
- **Níveis:** leitura, escrita ou omitido. A transcrição diz que "omitido" dá acesso total, mas o contexto sugere que ele quis dizer o valor padrão ou *none*. Confira na documentação.

```yaml
# Reconstrução ilustrativa a partir do que foi descrito (a aula não mostra código nesta parte)
permissions: {}              # começar com zero: nenhuma permissão

jobs:
  build:
    permissions:
      contents: read         # só o necessário, por job
```
> A sintaxe é ilustrativa. O professor só descreve o princípio ("começa com zero e adiciona o necessário"). Confira o formato exato na documentação.

#### Erros comuns e o que fazer
- ⚠️ **Erros:** permissões amplas; não definir nada (fica o padrão, que pode ser alto demais); dar `write` para tudo, quando nem tudo que precisa de escrita deve tê-la.
- **Na prática:**
  - **começar com zero** (permissões vazias);
  - se der erro por falta de permissão, adicionar **apenas a necessária**;
  - **separar por jobs**.

#### Versionamento das actions
- **Nunca use `latest` ou `main`.** Fixe uma versão específica: se der problema, você troca depois.
- ⚠️ **Falso positivo:** uma action em `main` pode passar o commit por causa de um erro dela mesma. Em CI/CD isso é grave: você acredita que o código foi revisado e está bom, e na prática não está.
- **Fixar pelo commit SHA** (o hash do commit): garante **sempre a mesma versão**. Útil em projeto grande ou com receio de uma action. Na maioria dos casos, a versão fixa já basta.
- **Terceiros:** revise sempre e **prefira as oficiais**. Se for usar uma de terceiro, escolha uma recomendada por alguém, já usada no dia a dia, usada por empresa ou com projeto grande e manutenção ativa.
- Sem versão fixa, você executa algo que pode mudar sem perceber: falso positivo, quebra ou gasto indevido nas actions.
- 💡 **A action não entrega valor direto ao usuário.** Ela traz segurança para você entregar melhor. Se ela atrasa ou toma o tempo das entregas, virou problema.

### 3. 🏗️ Arquitetura / Diagrama Lógico
**Por onde um secret pode vazar:**
```
[Secret / chave de API] -> deve ficar só em [secrets do GitHub]
   Pode vazar em: [código] | [logs (echo, mensagens de erro)] | [histórico de commits] | [comentários de PR/IA]
   Defesa: [não hardcodar] + [mascaramento] + [revisar logs] + [secrets separados por ambiente: dev/staging/prod]
```

**Como definir permissões do `GITHUB_TOKEN`:**
```
[Workflow rodando] -> GitHub entrega [token temporário com permissões padrão]
-> Começa com [permissions vazias] -> O job precisa de algo?
   SIM: [adicionar só a permissão necessária (read antes de write), no nível do job]
   NÃO: [manter sem permissão]
```

**Escolher a versão de uma action:**
```
[Quero usar uma action] -> É oficial ou recomendada, com manutenção ativa?
   NÃO: [evitar / revisar bem]
   SIM: [fixar versão: @vN ou commit SHA, nunca @main/latest]
        -> Projeto grande ou receio extra? SIM: [fixar pelo SHA]
```

**Risco da permissão em excesso:**
```
[Permissão ampla no workflow] -> [toda action herda] -> [action maliciosa pode: alterar código | abrir PRs | vazar dados]
```

### 4. Links e Referências Oficiais
- [**GitHub Actions**](https://docs.github.com/actions): documentação oficial. Lá estão secrets, permissões do `GITHUB_TOKEN` e uso de actions de terceiros.
- [**GitHub Packages**](https://docs.github.com/packages): registro de pacotes junto do código. A aula só apresenta e indica a documentação (guia de início rápido).
- **Secrets:** valores ocultos do repositório ou ambiente (ex.: chave de API, dados de banco).
- **`GITHUB_TOKEN`:** chave temporária entregue a cada execução do workflow. As permissões dizem o que ela pode fazer.
- **OIDC:** integração para login mais seguro em ferramentas como a AWS, sem guardar credenciais fixas. Vale buscar a documentação do GitHub sobre OIDC.
- **Commit SHA:** o hash que identifica um commit. Serve para fixar a versão exata de uma action.
- **Mascaramento de logs:** troca de valores sensíveis por `***` nos logs. Há ferramentas que fazem isso automaticamente.
- **Princípio do menor privilégio:** cada parte da automação roda com o mínimo de permissões necessário.

---
**Salvar como:** `06-rocketseat-git-github-actions-seguranca-boas-praticas-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.