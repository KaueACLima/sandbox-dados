# 📌 Deploy Automatizado (CD com GitHub Pages)

### 1. Conceito Central
O **CD** (entrega contínua) automatiza a parte final: levar o código validado até o usuário. Sem ele, você teria que entrar na plataforma de hospedagem e gerar e subir a versão manualmente a cada entrega. Com ele, um **push** (ou o fim de um pull request) em uma branch específica dispara o deploy sozinho.

A aula monta isso na prática: um site estático (`index.html`) publicado no **GitHub Pages** por um workflow. Pelo caminho, aparecem os erros comuns de um primeiro deploy e as boas práticas de ambientes, segredos e aprovação manual.

### 2. Pontos-chave e Sintaxe
#### Onde o CD se encaixa
- Quem entrega o código pode ser você, uma IA ou uma automação (commits, PRs, merges).
- **CI** valida a qualidade: testes automatizados, lint, revisão de código com IA, *code smell* (sinal de que o código pode estar mal escrito).
- **CD** faz o **deploy**: entrega para o cliente final consumir.

#### Escolhas antes de automatizar
- **Gatilho:** push, pull request ou commit. Defina como e quando a entrega acontece.
- **Build do projeto** depende da stack. Em React, por exemplo, instala dependências com npm e segue o processo que o React pede. Na aula usa-se só um `index.html`, para não prender o conteúdo a uma tecnologia.
- **Onde hospedar:**
  - **GitHub Pages:** simples e fácil de integrar com o GitHub. Bom para documentação (atualiza sozinha a cada commit), portfólios e projetos simples.
  - **Vercel** (a transcrição grafa "Verso"): menos configuração, deploy automático pronto. Foco em front-end, como React e Next.
  - **AWS** (ex.: S3 + CloudFront): mais controle, mais escalável e customizável, porém bem mais complexa.
  - A escolha depende da tecnologia do projeto e de onde o time prefere subir.

#### Boas práticas de CD
- **Nunca exponha variáveis sensíveis.** Para dado sensível (ex.: chave da OpenAI), use **secret**. Para configuração (ex.: em qual ambiente está), use **variável de ambiente**.
- **Separe os ambientes:**
  - *development:* onde devs testam; assume-se que pode ter falhas.
  - *staging:* onde o time interno (ex.: QA) testa. Se o QA pedir para limpar o ambiente, o banco pode ir embora, e é por isso que não se mistura com produção.
  - *production:* onde o cliente final usa; o ambiente mais seguro.
- **Valide antes de fazer deploy:** o CI vem antes.
- **Branches controláveis:** um fluxo de deploy por branch (`main`, `staging`, `dev`), não um único fluxo para todas. Analise caso a caso.
- **Aprovação manual em alguma etapa:** um push acidental (ou de uma IA) dispararia o gatilho e atualizaria produção sem você querer. Entregas hoje são muito rápidas (também por causa da IA), e uma etapa manual evita problemas.

#### Workflow de deploy (GitHub Pages)
- Arquivo: `.github/workflows/deploy.yaml`, com nome "Deploy Site Estático".
- Gatilho: push na branch `main`. Um job `deploy` roda em `ubuntu-latest`.
- **Permissões** do job: leitura de conteúdo (`contents: read`) e escrita em Pages (`pages: write`). O professor cita ainda uma terceira permissão, mas a transcrição está truncada. Confira no código da aula.
- **Steps** (todos com actions prontas do GitHub):
  1. checkout do repositório;
  2. configurar Pages;
  3. enviar os arquivos como **artefato** (o conteúdo da raiz, `path: ./`);
  4. publicar no GitHub Pages (action de deploy).

```yaml
# Reconstrução ilustrativa a partir do que o professor descreveu e digitou (a aula mostra o YAML na tela)
name: Deploy Site Estático
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: read      # ler o conteúdo do repositório
      pages: write        # escrever no GitHub Pages
      # (há uma terceira permissão dita no áudio, mas truncada na transcrição)
    steps:
      - name: Checkout
        uses: actions/checkout@v6
      - name: Configurar Pages
        uses: actions/configure-pages@v6
      - name: Enviar arquivos
        uses: actions/upload-pages-artifact@v5   # versão final citada na aula
        with:
          path: ./                               # todos os arquivos da raiz do projeto
      - name: Publicar site
        uses: actions/deploy-pages@v5
```
> As versões mudam ao longo da aula (veja os erros abaixo). Confira as atuais na documentação de cada action.

- **Fluxo na prática:**
  1. criar `index.html` simples (doctype, `pt-br`, `head` com título, corpo com mensagem);
  2. criar o repositório no GitHub e fazer o primeiro push;
  3. criar o workflow;
  4. commit e push, que dispara a action.

#### Erros que apareceram (e como foram resolvidos)
- ⚠️ **Falha no primeiro run:** o erro indicava que não conseguiu obter a configuração do site de Pages, pedindo para verificar se o Pages estava habilitado e configurado para build via GitHub Actions. **Causa:** o Pages ainda estava no modo de deploy manual. **Correção:** em *Settings > Pages*, trocar a fonte de publicação para **GitHub Actions**.
- ⚠️ **Actions desatualizadas:** o log avisava que `checkout` e `configure-pages` rodavam em versão do Node que deixaria de funcionar. O professor consultou as releases de cada action, e as versões mais novas rodam em **Node 24**. Atualizou `checkout` para v6 e `configure-pages` para v6.
- ⚠️ **Novos avisos no segundo run (deploy funcionou):** `deploy-pages` e um *upload artifact* desatualizados. Atualizou o `deploy-pages` (v5). Depois percebeu que o aviso vinha do `upload-pages-artifact`, que usa o *upload artifact* por baixo dos panos. Com esse ajuste, o run passou limpo.
- 💡 **Warning não é erro.** É normal aparecer depois de um tempo sem mexer em CI. O caminho é olhar a documentação e as releases da action que **você** usa, não da dependência interna dela.
- 🔎 **Código sugerido por IA/autocomplete pode trazer versões antigas.** O editor sugeriu versões desatualizadas (ex.: checkout v3, upload v3), e o professor trocou por conta própria. Confira as versões atuais antes de aceitar.
- 🔎 **Mensagens de commit:** o professor admite que `update deps 2` e `fix` não são boas mensagens (o correto seria nomear o que foi atualizado). Foi só para ganhar tempo.
- 🔎 **Onde ver o resultado:** *Settings > Pages* mostra o link do site, no padrão `https://<conta ou organização>.github.io/<nome-do-repositório>`. Funciona também com CSS e JavaScript simples. Para frameworks ou técnicas avançadas, procure fluxos de CI/CD mais completos (testes, lint, build, verificação com IA).

### 3. 🏗️ Arquitetura / Diagrama Lógico
**Pipeline completo (CI -> CD):**
```
[Entrega de código: você / IA / automação (commits -> PRs -> merge)]
-> [CI: testes automatizados, lint, review com IA, code smell]
-> [CD: deploy] -> [Ambiente: dev | staging | production] -> [Cliente final]
```

**Workflow do exemplo:**
```
[Push na main] -> [Job deploy em ubuntu-latest, permissões contents:read + pages:write]
-> [checkout] -> [configure-pages] -> [upload-pages-artifact (path ./)] -> [deploy-pages]
-> [Site publicado em https://conta.github.io/repositorio]
```

**Decisão de gatilho e aprovação:**
```
[Houve push/PR numa branch com deploy configurado?]
   SIM: Esse ambiente é sensível (ex.: produção)? -> SIM: [exigir aprovação manual] | NÃO: [deploy automático]
   NÃO: [nada acontece]
```

**Diagnóstico de erro de deploy:**
```
[Run falhou] -> Mensagem aponta que o Pages não está configurado?
   SIM: [Settings > Pages > fonte = GitHub Actions] -> [novo push]
   NÃO (só warning de versão): [conferir releases da action usada] -> [atualizar versão] -> [novo push]
```

### 4. Links e Referências Oficiais
- [**GitHub Pages**](https://docs.github.com/pages): hospedagem de sites estáticos direto do repositório. A fonte de publicação é configurada em *Settings > Pages*.
- [**actions/configure-pages**](https://github.com/actions/configure-pages): prepara o Pages para o deploy.
- [**actions/upload-pages-artifact**](https://github.com/actions/upload-pages-artifact): empacota os arquivos do site como artefato.
- [**actions/deploy-pages**](https://github.com/actions/deploy-pages): publica o artefato no GitHub Pages.
- [**Vercel**](https://vercel.com): plataforma de deploy automático com foco em front-end (React, Next).
- [**Amazon S3**](https://aws.amazon.com/s3/) e [**CloudFront**](https://aws.amazon.com/cloudfront/): armazenamento e distribuição (CDN) da AWS, opção mais escalável e complexa.
- [**GitHub Actions**](https://docs.github.com/actions): documentação oficial. Lá estão permissões, secrets e variáveis de ambiente.
- **Secret / variável de ambiente:** dado sensível (ex.: chave de API) vai em secret. Configuração (ex.: ambiente) vai em variável de ambiente. Vale buscar a página de secrets na documentação.
- **Staging / production / development:** os três ambientes citados, conforme a seção 2.
- **Artefato:** arquivo(s) gerado(s) por um passo e entregue(s) ao próximo (aqui, o site que sobe ao Pages).

---
**Salvar como:** `05-rocketseat-git-github-actions-deploy-automatizado-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.