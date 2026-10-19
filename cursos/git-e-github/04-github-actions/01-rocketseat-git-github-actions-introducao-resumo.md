# 📌 Introdução ao GitHub Actions

### 1. Conceito Central
Processo manual (rodar testes, subir o projeto e torcer para dar certo) não escala. Em time grande, quanto mais manual, maior a chance de **erro humano**: teste esquecido, código quebrando em produção, deploy que falha sem ninguém perceber, feature que não sobe.

A solução é **CI/CD**, e o **GitHub Actions** é o motor que executa isso dentro do repositório. Você escreve a automação uma vez, e o GitHub a executa sozinho a cada evento (push, por exemplo).

### 2. Pontos-chave e Sintaxe
- **CI (Integração Contínua):** integrar código com frequência, de forma segura e testada. Valida, testa e tenta fazer a *build* (compilação/empacotamento do projeto).
  - Ex.: abre um *pull request* (pedido de mesclagem), os testes rodam sozinhos; se falharem, **não faz merge** e o dev é avisado de onde falhou.
- **CD (Entrega Contínua):** automatiza a entrega. Se o CI é a inspeção de qualidade, o CD é a entrega: depois de validado, coloca no ar (deploy).
- **GitHub Actions:** roda testes, build, deploy e scripts automáticos dentro do repositório. Os scripts de limpeza e de qualidade de código (CodeQL) que apareceram em aulas anteriores já eram Actions.
- **Onde fica:** `.github/workflows/nome-do-arquivo.yaml` (nomes de pasta exatos, nesse padrão). O arquivo é **YAML** (linguagem de marcação de texto usada para descrever a rotina).
- **Hierarquia (analogia da receita de bolo):**
  - **Workflow:** a receita inteira, o roteiro da automação.
  - **Job:** uma etapa grande da receita (ex.: instalar dependências é um job; rodar testes é outro). Um workflow pode ter vários.
  - **Step:** o passo granular dentro do job. Ex. em Node.js: instalar o Node, `npm install`, `npm test`.
  - **Action:** bloco de lógica **reutilizável** que você encaixa num step (ex.: checkout do código, setup do Node), sem reinventar a roda.
- **Peças do arquivo mostrado na aula:**
  - `name`: nome do workflow, o que aparece na aba Actions do GitHub.
  - `on`: o gatilho (*trigger*). Lê-se "quando acontecer X". Aqui: push na branch `main`. Poderia ser pull request ou outros eventos (ver documentação).
  - `jobs`: aqui, um job chamado *hello job*.
  - `runs-on`: a **máquina virtual** onde o job roda. Aqui: `ubuntu-latest` (Ubuntu, sistema baseado em Linux, na versão mais recente disponível).
  - `steps`: a lista de passos.
  - `uses: actions/checkout@v4`: usa uma action pronta (`actions` = origem, `checkout` = nome da action, `@v4` = versão).

```yaml
name: Primeiro workflow            # nome livre do workflow
on:
  push:
    branches: [main]               # gatilho: push na branch main
jobs:
  hello-job:                       # job "hello job"
    runs-on: ubuntu-latest         # máquina virtual onde o job executa
    steps:
      - name: Checkout do código
        uses: actions/checkout@v4  # action pronta: baixa o repositório na VM
      - name: Exibir mensagem
        run: echo "Hello World"    # a aula diz que o step exibe "Hello World"; o comando exato não aparece no áudio
```
> O YAML acima é reconstruído a partir do que o professor descreveu em voz alta. Confira com o código que ele deixou na descrição da aula.

- **Fluxo prático da aula:** criar `.github/workflows/`, criar o arquivo, `git add`, `git commit`, `git push`. O workflow rodou sozinho, porque o próprio push é o gatilho. Depois, trocou `@v4` por `@v6`, fez novo commit e push, e o workflow rodou de novo.
- ⚠️ **Espaçamento no YAML:** a indentação (dois espaços por nível) tem que estar certa, senão dá erro. Vale instalar a extensão de YAML no VS Code, que dá autocomplete e aponta código incorreto.
- 🔎 **Escolha da máquina:** pegue uma que supra a necessidade, não a mais potente. Máquina maior pode demorar mais para subir e deixar o job mais lento.
- ⚠️ **Warning não é erro:** erro aparece com um **X vermelho**. Já o aviso de que a `checkout@v4` roda em Node 20, versão depreciada (fora de uso recomendado), não quebra o job. Foi resolvido atualizando para `@v6`, e o aviso sumiu. Vale olhar os runs mesmo quando passam.
- 🔎 **O que o checkout faz:** baixa o repositório na máquina virtual (código, versões, arquivos). Sem ele o GitHub não tem acesso ao código para rodar o que vem depois. É o script base de quase todo workflow.
- 🔎 **Anatomia de um run (na aba Actions):** setup do job -> checkout -> steps do workflow -> post-checkout (*cleanup*, limpa o que o checkout usou) -> job completo. O CodeQL segue a mesma lógica, só com mais etapas.
- 💡 **Frase da aula:** se o seu processo depende de você lembrar de rodar algo, ele está errado.

### 3. 🏗️ Arquitetura / Diagrama Lógico
**Hierarquia do workflow:**
```
[Workflow: arquivo .yaml] -> [Job (1 ou mais), roda em runs-on] -> [Step (vários)] -> [Action reutilizável (uses) ou comando próprio]
```

**Fluxo de execução do exemplo:**
```
[Dev faz push na main] -> [Gatilho on: push dispara o workflow]
-> [GitHub sobe VM ubuntu-latest] -> [Step 1: checkout (action @v4/@v6)]
-> [Step 2: exibe mensagem] -> [Post-checkout: limpeza]
-> [Resultado: ✅ completo | ⚠️ warning | ❌ X vermelho]
```

**Lógica CI -> CD:**
```
[Abre pull request] -> Testes passaram?
   SIM: [merge liberado] -> [CD faz o deploy em produção]
   NÃO: [merge bloqueado + aviso ao dev de onde falhou]
```

### 4. Links e Referências Oficiais
- [**GitHub Actions**](https://docs.github.com/actions): documentação oficial. O professor reforça consultá-la para ver os eventos disponíveis e entender erros.
- [**actions/checkout**](https://github.com/actions/checkout): repositório da action que baixa o código do repo na VM. Foi onde ele consultou a versão recomendada.
- [**YAML**](https://yaml.org): linguagem de marcação do arquivo de workflow. A indentação importa.
- [**Node.js**](https://nodejs.org): forma de rodar JavaScript no servidor. É como o GitHub executa as actions por baixo. O aviso de depreciação era sobre a versão 20.
- [**CodeQL**](https://codeql.github.com): análise de qualidade/segurança de código, citada como exemplo de Action pronta já configurada no repo.
- **CI/CD, workflow, job, step, runner (VM):** conceitos da própria aula. O detalhamento vem na documentação do GitHub Actions, linkada acima.

---
**Salvar como:** `01-rocketseat-git-github-actions-introducao-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.