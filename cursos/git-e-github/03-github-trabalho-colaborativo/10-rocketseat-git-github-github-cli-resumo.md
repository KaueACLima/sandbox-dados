# 📌 GitHub CLI — Automatizando o GitHub pelo Terminal

### 1. Conceito Central
Esta aula apresenta o **GitHub CLI** (`gh`), uma ferramenta de linha de comando que permite interagir com recursos do GitHub (repositórios, pull requests, issues, gists, releases, etc.) diretamente do terminal, sem precisar abrir o navegador para cada ação. A ideia central é reduzir trabalho manual repetitivo na interface web — especialmente relevante à medida que fluxos automatizados (incluindo IA) passam a criar e revisar pull requests com frequência, tornando útil ter comandos rápidos para inspecionar e agir sobre esse fluxo direto do terminal.

### 2. Pontos-chave e Sintaxe
- **Instalação**: disponível para Mac (ex: via Homebrew), Linux e Windows — o site oficial do GitHub CLI traz instruções para cada sistema.
- **Autenticação**: feita com o comando de login, que guia por um fluxo de escolha de host (`github.com`), método de autenticação (chave SSH, navegador, passkey) e gera um token de acesso.
```bash
# Autentica a CLI com a conta do GitHub
gh auth login

# Verifica o status da autenticação atual (conta logada, protocolo, escopos do token)
gh auth status
```
- **Gerenciar repositórios** com `gh repo`:
```bash
# Lista os repositórios da conta autenticada
gh repo list

# Cria um novo repositório (pergunta interativamente: nome, dono, descrição,
# visibilidade público/privado, se quer README/.gitignore/licença)
gh repo create
```
- **Gists**: recurso do GitHub (não detalhado em aulas anteriores) para publicar publicamente pequenos trechos de código ou arquivos formatados em Markdown, reutilizáveis ou consumíveis por outras pessoas — como uma forma de "postagem" de código.
- **Pull Requests** via `gh pr`:
```bash
# Lista os pull requests abertos do repositório atual
gh pr list

# Cria um novo pull request a partir da branch atual
# (pede título, corpo/descrição, e permite marcar como draft)
gh pr create
```
- Fluxo demonstrado na prática: criar uma branch nova, alterar um arquivo, commitar, dar `git push` (configurando o upstream da branch), e então usar `gh pr create` para abrir o PR sem precisar acessar a interface web do GitHub — o comando já sugere automaticamente título com base no último commit.
- A CLI também cobre, segundo a aula, comandos adicionais para issues, organizações, projetos, releases, repositórios, GitHub Actions, labels e licenças — um escopo amplo que não foi percorrido por completo na aula.
- 💡 **Dica:** o GitHub CLI é especialmente útil para automação e integração com ferramentas de IA, já que permite que um agente crie ou liste pull requests programaticamente pelo terminal, sem depender da interface gráfica do GitHub.

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[Terminal local] 
   -> gh auth login -> [Autenticado com a conta GitHub via SSH/token]
   -> gh repo create -> [Novo repositório criado na conta, sem precisar abrir o navegador]
   -> Alterações feitas localmente (branch + commit)
        -> git push (configura upstream da nova branch)
        -> gh pr create -> [Pull Request aberto diretamente do terminal, com link de retorno para visualizar no GitHub]
   -> gh pr list / gh repo list -> [Consulta rápida do estado atual sem abrir a interface web]
```

### 4. Links e Referências Oficiais
- **GitHub CLI:** [GitHub CLI - cli.github.com](https://cli.github.com/) — página oficial com instruções de instalação para Mac, Linux e Windows.
- **Manual de comandos do GitHub CLI:** [GitHub CLI Manual](https://cli.github.com/manual/) — referência completa de todos os comandos (`gh repo`, `gh pr`, `gh issue`, `gh gist`, `gh release`, entre outros).
- **GitHub Gist:** [About Gists](https://docs.github.com/en/get-started/writing-on-github/editing-and-sharing-content-with-gists/about-gists) — documentação oficial sobre criação e uso de gists.

---
**Salvar como:** `10-rocketseat-git-github-github-cli-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.