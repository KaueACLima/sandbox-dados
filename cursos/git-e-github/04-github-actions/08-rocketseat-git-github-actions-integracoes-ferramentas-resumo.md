# 📌 Integrações com Outras Ferramentas (Discord)

### 1. Conceito Central
O poder do GitHub Actions aparece quando ele **conversa com outras ferramentas**. O problema que a aula resolve: o GitHub avisa de falhas por e-mail, e e-mail muitas vezes passa despercebido. O time acha que o deploy está subindo, mas o lint nem passou e o deploy nem começou.

A solução é **notificar onde o time já está**. A aula faz isso com um **webhook do Discord**: o workflow envia uma mensagem automática para um canal. Serve igual para Slack ou outra ferramenta de comunicação.

### 2. Pontos-chave e Sintaxe
- **Webhook:** forma de integrar aplicações em que uma delas **fica "ouvindo"** e, quando recebe um aviso, realiza uma ação. Aqui: o workflow avisa o Discord e o Discord posta a mensagem no canal.
- **Passo 1, criar o webhook no Discord:**
  1. criar um canal de texto (ex.: "Notificações PR");
  2. *Editar canal > Integrações > Webhooks*, e criar um webhook;
  3. dar um nome ao bot que posta as mensagens;
  4. **copiar a URL do webhook** e salvar.
- **Passo 2, guardar a URL como secret no GitHub:** *Settings > Environments*, entrar no environment e criar um **environment secret**. O professor nomeou com "Discord Webhook" e depois acrescentou "URL" no nome, para ficar claro que é a URL do webhook.
- **Passo 3, workflow que dispara a mensagem:**
  - nome do workflow `notify`;
  - gatilho: push na `main` (ele cogitou trocar para pull request na `main`, mas testou com push);
  - roda em `ubuntu-latest`;
  - um step executa **`curl`** (ferramenta de requisição HTTP), fazendo um **POST** em JSON para a URL do secret, com a mensagem.

```yaml
# Reconstrução ilustrativa (a aula mostra o YAML na tela; o texto exato da mensagem e do comando não são ditos em voz alta)
name: notify
on:
  push:
    branches: [main]
jobs:
  notify:
    runs-on: ubuntu-latest
    environment: github-pages        # nome do environment que guarda o secret (ver erro abaixo)
    steps:
      - name: Enviar mensagem no Discord
        run: |
          curl -X POST -H "Content-Type: application/json" \
               -d '{"content": "Build finalizada com sucesso"}' \
               "${{ secrets.DISCORD_WEBHOOK_URL }}"   # a URL vem do secret, nunca no código
```
> O nome exato do environment (a transcrição o grafa de formas diferentes) e do secret são ilustrativos. Confira com o seu repositório e com o código que o professor deixou na descrição da aula.

- **Resultado:** depois do ajuste abaixo, o bot postou no canal a mensagem de "build finalizada com sucesso".
- **O mesmo repositório rodou dois jobs** (`notify` e `hello`, de um workflow anterior). Sem dependência declarada, jobs rodam **em paralelo**.

#### O erro da aula
- ⚠️ **Sintoma:** o job `notify` falhou com `exit code 2` e a mensagem **"No URL specified"**. A URL do secret chegou **vazia** ao `curl`, mesmo o secret existindo.
- **Causa:** o secret estava em um **environment secret**, e o job **não declarava o environment**. Sem isso, o ambiente (e seus secrets) **não é carregado automaticamente**.
- **Correção:** adicionar `environment: <nome do environment>` no job. Depois disso, funcionou.
- 💡 **Regra:** usou environment secret? **Declare o environment no job**, manualmente.
- 🔎 **Alternativa:** guardar a URL como secret (ou variável) de **repositório**, que dispensa declarar o ambiente. O professor prefere o environment secret porque o secret só roda no ambiente certo (ex.: o do Pages).
- 🔎 **Dica de depuração:** abrir o log do step, ver o comando como foi executado e checar se o valor do secret apareceu.

#### Boas práticas e ideias de evolução
- ⚠️ **A URL do webhook é sensível:** quem a tiver consegue postar no canal. Por isso vai para secret. O professor avisa que apagou o webhook mostrado na gravação.
- 🔎 **Personalização:** incluir variáveis (ex.: nome de quem abriu o PR) e **marcar a pessoa** (@) na mensagem, porque ela não vê notificação se só postar no canal. Dá para fazer para PR, bug e outros eventos, e para outros canais (ex.: Slack).
- 💡 **Mensagem do professor:** automação demanda **pesquisa e tentativa**. Errar e reestruturar é normal. Se não funcionou, pause e tente de novo.
- 🔎 **Problema de git no meio da aula (não era do tema):** o push foi recusado porque o remoto tinha alterações novas. O professor copiou o arquivo, fez `git reset`, trouxe as alterações (`fetch` e `pull`), colou o arquivo de volta, fez novo commit e push. Poderia ter usado `git stash` (guardar alterações temporariamente).

### 3. 🏗️ Arquitetura / Diagrama Lógico
**Fluxo da notificação:**
```
[Evento: push (ou PR) na main] -> [Workflow notify dispara]
-> [Job em ubuntu-latest, com environment declarado]
-> [curl POST JSON para a URL do webhook (lida do secret)]
-> [Discord recebe no webhook] -> [Bot posta a mensagem no canal]
```

**Onde mora a URL do webhook:**
```
[Discord: URL do webhook copiada] -> [GitHub: environment secret (valor oculto)]
-> [Workflow lê via secrets.<NOME>] -> nunca aparece no código
```

**Diagnóstico do erro "No URL specified":**
```
[curl falhou com "No URL specified"] -> O secret existe?
   SIM: Ele é um environment secret? -> SIM: Job declara "environment:"?
            NÃO: [adicionar environment: <nome>] -> [novo push]
            SIM: [conferir nome do secret e do environment]
   NÃO: [criar o secret]
(alternativa: secret/variável de repositório, sem precisar declarar o ambiente)
```

### 4. Links e Referências Oficiais
- [**Webhooks do Discord**](https://discord.com/developers/docs/resources/webhook): referência oficial do formato da requisição. Vale conferir os campos além de `content`.
- [**curl**](https://curl.se/docs/): ferramenta de linha de comando para requisições HTTP. É o padrão para fazer POST na API do webhook.
- [**GitHub Actions**](https://docs.github.com/actions): documentação oficial. Lá estão environments, secrets e permissões.
- **Webhook:** mecanismo em que uma aplicação reage quando outra a avisa de um evento.
- **Slack:** a aula cita como alternativa ao Discord para o mesmo tipo de integração. Vale buscar a documentação oficial de webhooks do Slack.
- **Environment secret vs. repository secret:** ver aula 07. O primeiro exige declarar o `environment` no job.
- **DevOps (Rocketseat):** o professor indica novamente o conteúdo da plataforma para aprofundar CI/CD.

---
**Salvar como:** `08-rocketseat-git-github-actions-integracoes-ferramentas-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.