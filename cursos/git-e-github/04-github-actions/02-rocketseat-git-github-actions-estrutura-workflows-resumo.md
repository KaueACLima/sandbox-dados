# 📌 Estrutura e Exemplos de Workflows

### 1. Conceito Central
Um workflow se customiza em três eixos: **quando** roda (triggers), **o que** roda e em que ordem (jobs) e **como** cada passo é executado (steps, via `uses` ou `run`). Combinando esses eixos, o mesmo mecanismo cobre validação de PR, deploy automático e tarefas agendadas.

A aula também traz uma ressalva de arquitetura: **nem toda automação precisa ser um workflow próprio**. Antes de criar um, vale perguntar se o GitHub, ou uma ferramenta externa, já entrega isso pronto.

### 2. Pontos-chave e Sintaxe
#### Triggers (quando dispara)
- **`push`:** roda a cada push. Bom para rotinas **leves e rápidas**, como *lint* (verificação automática de estilo e erros simples de código).
- **`pull_request`:** roda a cada PR. Bom para rotinas **mais pesadas**, como análise de qualidade de código com IA, que demora mais e gera custo.
- **`schedule`:** roda em horários definidos usando a sintaxe de **cron** (agendador de tarefas por dia, hora e semana). Usos citados: backup, limpeza e verificação de dependências, diária ou semanal.
  - A transcrição grafa "Chrome", mas o contexto (horário, dia da semana) mostra que é **cron**.
- **Combinar triggers:** o mesmo workflow pode disparar em mais de um evento (ex.: push e pull request).
- ⚠️ **Não repita a mesma rotina em push e PR:** você roda o mesmo código várias vezes à toa. Deixe o leve no push e o caro no PR.
- 🔎 **Verificação de dependências agendada:** uma dependência pode ser atualizada sem você saber, e o agendamento cobre esse ponto cego.

#### Jobs (os "capítulos do roteiro")
- Um workflow pode ter **vários jobs** (ex.: `build` e `test`).
- Por padrão rodam **em paralelo** (ao mesmo tempo).
- Dá para criar **dependência** entre eles: o `test` só roda se o `build` terminar com sucesso. Assim você controla a ordem e encadeia processos (na sintaxe do GitHub, a palavra-chave é `needs`, que não foi dita no áudio).
- Cada job pode rodar em **máquinas diferentes**.

#### Steps (os passos dentro do job)
- **`uses`:** usa uma **action pronta**, um código reutilizável.
- **`run`:** roda um **comando manual**, como o `echo` (comando que imprime texto no terminal).
- Exemplo de sequência: baixar o código -> preparar o ambiente -> rodar testes.

```yaml
# Reconstrução ilustrativa a partir do que foi descrito na aula
on:
  push:                       # trigger 1: a cada push
  pull_request:               # trigger 2: a cada pull request
  schedule:
    - cron: '0 3 * * 1'       # agendado: segunda (1) às 3h (3); o "0" dos minutos não foi dito
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6   # uses = action pronta (baixa o código)
      # ...passos de "instalar" e "testar" (comandos não mostrados no áudio)
      - run: echo "exemplo"         # run = comando manual
```
> Os comandos de instalar e testar não são citados na aula. Por isso aparecem só como comentário.

#### Exemplos de uso do dia a dia
- **Validar pull request:** job `test` com steps checkout -> instala -> testa.
- **Deploy automático:** a cada push na `main`, faz o deploy. O código dos steps **depende de onde você publica** (ex.: Amazon S3, Vercel). A transcrição grafa "Verso", mas pelo contexto é Vercel (plataforma de hospedagem e deploy). Por isso a aula não traz um exemplo fixo.
- **Tarefa agendada:** pipeline toda **segunda às 3h** (o `1` = segunda). Um job roda no Ubuntu com checkout, instala dependências e roda testes. Um segundo job, em paralelo e possivelmente em outra máquina, faz uma rotina semanal de manutenção do código e depois uma análise com IA.

#### Nem tudo precisa de workflow
- Existem automações **nativas do GitHub**, sem Action própria. Exemplo: o **review do Copilot** no pull request.
- Dá para customizar esse review com um arquivo de **Copilot Instructions** dentro da pasta `.github`. Exemplos citados de instruções: responder em espanhol, aplicar os checks numa pasta específica, focar em legibilidade e não permitir operadores ternários aninhados (a transcrição grafa "alinhados").
  - **Operador ternário** (JavaScript): um `if/else` em uma linha, com `?` e `:`.
- **Demonstração da aula:** `git checkout -b exemplo` -> alteração -> `git add .`, commit e push -> abre PR da `exemplo` para a `main` -> solicita o review do Copilot.
- 🔎 **Observações da demo:** o review aparece como comentário no PR, mas **não é obrigatório para o merge**. O Copilot **esperou os checks** (CodeQL) terminarem antes de revisar.
- 💡 **Pergunta antes de criar um workflow:** preciso mesmo de algo customizado, ou já existe uma solução pronta (do GitHub ou de ferramenta externa, como a automação de CD da Vercel)?
- ⚠️ **Custo de customizar:** uma Action própria consome tempo e recursos do time e precisa de **manutenção** se parar de funcionar ou exigir atualização. Customize quando o fluxo é realmente específico e o pronto não supre.

### 3. 🏗️ Arquitetura / Diagrama Lógico
**Escolha do trigger por custo e peso da rotina:**
```
[Rotina a automatizar] -> É leve e rápida (ex.: lint)?
   SIM: [rodar no push]
   NÃO (pesada ou custa, ex.: análise com IA): [rodar no pull request]
-> Precisa rodar em horário fixo (backup, limpeza, dependências)? SIM: [schedule/cron]
```

**Encadeamento de jobs:**
```
[Job build] -> terminou com sucesso? -> SIM: [Job test roda] | NÃO: [test não roda]
(sem dependência declarada: build e test rodam em paralelo)
```

**Exemplo agendado (segunda 3h):**
```
[cron: segunda 3h] -> [Job 1: checkout -> instala dependências -> testes]
                   -> [Job 2 (paralelo): manutenção semanal -> análise com IA]
```

**Decisão: workflow próprio ou solução pronta?**
```
[Quero automatizar X] -> Existe solução pronta (GitHub nativo / ferramenta externa) que supre?
   SIM: [usar a pronta: menos custo e manutenção]
   NÃO (fluxo específico demais): [criar workflow customizado e manter]
```

### 4. Links e Referências Oficiais
- [**GitHub Actions**](https://docs.github.com/actions): documentação oficial. Lá estão a lista de eventos (triggers), a sintaxe de `schedule` e a de dependência entre jobs.
- [**Vercel**](https://vercel.com): plataforma de hospedagem e deploy, citada como alternativa pronta a montar o CD à mão.
- [**Amazon S3**](https://aws.amazon.com/s3/): serviço de armazenamento da AWS, citado como um dos destinos possíveis de deploy.
- **Cron:** sintaxe de agendamento por minuto, hora, dia e semana, usada em várias linguagens. Vale buscar uma referência para entender os campos.
- **Lint:** análise automática de estilo e erros simples de código. Rápida, ideal para o push.
- **GitHub Copilot (code review) e Copilot Instructions:** review automático no PR, customizável por arquivo dentro de `.github`. Vale buscar a documentação oficial do GitHub Copilot.
- **CodeQL:** análise de qualidade e segurança de código, citada como check rodando no PR.

---
**Salvar como:** `02-rocketseat-git-github-actions-estrutura-workflows-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.