# 📌 Actions Reutilizáveis

### 1. Conceito Central
Duplicar lógica de automação gera retrabalho. Se a versão do Node muda, por exemplo, você teria que corrigir em seis ou sete workflows. O ideal é trocar em **um só lugar**.

O GitHub oferece duas formas de reaproveitar lógica: **reusable workflows**, que reaproveitam um workflow inteiro, e **custom actions**, que reaproveitam um bloco de steps. Quanto mais fluxos iguais você tem, mais vale centralizar.

### 2. Pontos-chave e Sintaxe
- **Problema (duplicação):** cinco repositórios que fazem build de Node, cada um com seu YAML, exigem atualizar em cinco lugares.
- **Solução:** um workflow central faz o build e os outros só o **chamam**. Atualizando só o central, todos ficam certos.

#### Actions da comunidade
- Evitam reinventar a roda. Exemplos: `checkout` (já usado nas aulas) e `setup` do Node.
- **`with`:** passa uma informação variável para a action usar internamente. Ex.: `with: node-version: 18` faz a action trabalhar para o Node 18.
- ⚠️ **Nem toda action da comunidade é segura.** Verifique estrelas, mantenedores e versões. No repositório, olhe:
  - data do último commit;
  - engajamento de pessoas;
  - issues e pull requests abertos (sinal de uso e manutenção ativa).
- Uma action parada há cerca de seis anos pode ter falhas de segurança, features desatualizadas e dependências incorretas.

#### Custom actions (criar as suas)
- Não precisa publicar: dá para usar só internamente nos seus projetos.
- **Três tipos:**
  - **JavaScript** (roda via Node): para lógicas complexas. Caso de uso raro.
  - **Docker:** ambiente isolado, útil para testes e afins.
  - **Composite:** agrupa vários steps. É a ideal para a maioria dos casos: um fluxo usado em várias aplicações vira uma action só.
- Custom actions já caminham para **DevOps**. A aula indica o conteúdo de DevOps da Rocketseat para aprofundar. Na prática, o professor diz que o dia a dia costuma ficar no Composite.

#### Exemplo de Composite (instala dependências + build)
- Recebe um **input** obrigatório: a versão do Node.
- Roda em modo composite, com steps que usam esse input (é a forma de ter uma "variável" no YAML do Actions).
- Cada comando roda no **Bash** (terminal): `npm install` e `npm run build`.
- Fica dentro de `.github/actions/install` e é chamada passando `nodeVersion` = 22.

```yaml
# Reconstrução ilustrativa a partir do que foi descrito (a aula mostra o YAML na tela; os nomes exatos das chaves não são ditos em voz alta)
# --- definição da action (dentro de .github/actions/install) ---
inputs:
  nodeVersion:            # input: versão do Node
    required: true        # obrigatório para a action rodar
runs:
  using: composite        # tipo Composite: agrupa steps
  steps:
    # step que prepara o Node usando a versão recebida em inputs
    - run: npm install    # instala dependências
      shell: bash         # roda no terminal Bash
    - run: npm run build  # build do projeto
      shell: bash

# --- chamada dentro de um workflow ---
# - uses: <caminho da action em .github/actions/install>
#   with:
#     nodeVersion: 22     # passa o valor do input
```
> O professor reconhece que o exemplo é didático: em projeto simples faz pouco sentido.

- 💡 **Regra prática:** se um bloco de steps se repete **mais de duas vezes**, ele deveria virar uma action. Instalar dependências e preparar o ambiente é muito comum em CIs: com quatro fluxos de CI, é melhor fazer em um lugar só.
- 🔎 **Projetos simples** (só HTML, CSS e JavaScript) raramente precisam de workflows complexos: há menos coisa para testar e validar. Workflows mais elaborados aparecem com frameworks e ferramentas associadas.

#### Reusable workflows
- Aqui o reaproveitamento é de **workflows inteiros**: pipelines e fluxos completos, não só steps.
- Quando o workflow é **chamado** por outro, ele executa o job dele. Dentro de um job de outro workflow, você chama o build apontando para o arquivo.
- Comparação: custom action reaproveita **steps**; reusable workflow reaproveita **o workflow**.

#### Boas práticas
- ⚠️ **Fixe a versão, nunca dependa de código que pode mudar sem aviso.** Evite `checkout@main`, que usa a versão mais recente da branch principal. Se a action muda a forma de uso (ex.: passa a exigir parâmetro da v4 para a v5), sua automação pode quebrar sem você ter mexido em nada.
- **Evite duplicação:** se o mesmo fluxo é automatizado mais de uma vez, torne-o reutilizável (job ou steps reutilizáveis).
- **Nomes claros e objetivos:** ex.: "setar variáveis de ambiente do Node", "rodar testes", "fazer deploy de um app".
- **Parametrize quando necessário:** em vez de quatro jobs, um por versão do Node, crie um job que se comporte conforme a versão recebida.
- **Documente:** README com exemplos, inputs e outputs claros, variáveis a passar e configurações prévias.
- **Segurança:** evite actions desconhecidas e use versões fixas, tanto das suas automações quanto dos pacotes externos.
- 💡 **Resumo do professor:** automação não é só fazer funcionar, é fazer funcionar **sem dor**.
- ⚠️ **Não copie workflow sem entender.** Um workflow copiado e colado pode trazer problemas de performance, de custo ou de funcionalidade fora do esperado. Use a documentação (ou uma IA) para pesquisar e fundamentar. O conteúdo é agnóstico de linguagem: Node serve só de exemplo.

### 3. 🏗️ Arquitetura / Diagrama Lógico
**Sem reutilização vs. com reutilização:**
```
SEM:  [Repo A: YAML de build] [Repo B: YAML de build] ... [Repo E: YAML de build]
      -> mudou algo no build do Node? -> [atualizar em 5 lugares]

COM:  [Workflow central de build]
      <- chamado por [Repo A] [Repo B] ... [Repo E]
      -> mudou algo? -> [atualizar só o central]
```

**Qual tipo de reuso usar:**
```
[Quero reaproveitar lógica] -> O que repete?
   Um bloco de steps -> [Custom action]
        -> Composite (maioria dos casos) | Docker (ambiente isolado) | JavaScript (lógica complexa, raro)
   Um workflow/pipeline inteiro -> [Reusable workflow]
```

**Fluxo da action Composite do exemplo:**
```
[Workflow chama a action em .github/actions/install] -> with: nodeVersion = 22
-> [Input obrigatório recebido] -> [Steps no Bash: npm install -> npm run build]
```

**Decisão ao usar uma action de terceiros:**
```
[Quero usar uma action da comunidade] -> Repositório tem manutenção ativa (commits recentes, engajamento, issues/PRs)?
   SIM: [usar, com versão fixa (ex.: @v4), nunca @main]
   NÃO: [evitar: risco de falhas de segurança e dependências incorretas]
```

### 4. Links e Referências Oficiais
- [**GitHub Actions**](https://docs.github.com/actions): documentação oficial. Lá estão a criação de actions (Composite, Docker, JavaScript) e os reusable workflows.
- [**actions/setup-node**](https://github.com/actions/setup-node): action pronta para preparar o Node numa versão específica via `with`. É o tipo de exemplo citado na aula.
- [**Docker**](https://docs.docker.com): ambiente isolado (contêiner), base do tipo de custom action "Docker".
- [**Node.js**](https://nodejs.org): base do tipo de action "JavaScript". `npm install` e `npm run build` são comandos do ecossistema Node.
- **Bash:** terminal onde os comandos dos steps rodam (campo `shell`).
- **DevOps:** o professor indica o conteúdo de DevOps da Rocketseat para aprofundar GitHub Actions e outras formas de CI/CD.

---
**Salvar como:** `03-rocketseat-git-github-actions-actions-reutilizaveis-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.