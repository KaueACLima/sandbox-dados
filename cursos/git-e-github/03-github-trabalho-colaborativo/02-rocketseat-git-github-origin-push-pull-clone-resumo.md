# 📌 Origin, push, pull e clone

### 1. Conceito Central
Esta aula explica como o Git local se conecta ao GitHub através do conceito de **origin** — e como essa conexão é usada na prática pelos comandos `clone`, `push` e `pull`. A ideia central é: o Git, por si só, sabe versionar arquivos na sua máquina, mas **não sabe automaticamente para qual repositório remoto enviar ou buscar esses arquivos** até que um `origin` seja explicitamente configurado, seja via clonagem de um repositório já existente, seja ligando manualmente um repositório local vazio a um repositório recém-criado no GitHub.

### 2. Pontos-chave e Sintaxe
- **Origin:** é um apelido (alias) para o endereço do repositório remoto — geralmente um repositório no GitHub. Por convenção de mercado, quase sempre é chamado de `origin`, mas o nome não é obrigatório.
- **Por que `git push` falha sem configuração prévia:** o Git não sabe (1) para qual repositório remoto enviar os arquivos (não existe origin) e, mesmo tendo um origin, (2) pode não saber a qual branch remota a branch local deve se conectar.
- **Duas formas de criar um origin:**
  - **Via `clone`:** copia um repositório já existente (commits, autores, datas, histórico completo) para a máquina local e automaticamente cria o origin apontando para a URL de onde foi clonado.
  - **Via repositório criado do zero:** cria-se um repositório vazio no GitHub e liga-se manualmente ao repositório local já existente na máquina.
- **Comandos usados na aula:**

```bash
# Tentativa de push sem origin configurado -> erro
git push

# Clonar um repositório existente (cria o origin automaticamente)
git clone <url-do-repositorio>
cd <pasta-do-projeto-clonado>

# Verificar para qual URL remota o repositório está apontando
git remote -v

# Listar as branches locais (a "main" é criada por padrão em todo repositório novo)
git branch

# Conectar um repositório local vazio a um repositório remoto recém-criado
git remote add origin <url-do-repositorio>
git branch -M main
git push -u origin main   # emparelha a branch local "main" com a branch remota "main"

# Trazer alterações que existem no remoto mas não na máquina local
git pull

# Verificar o estado dos arquivos / listar arquivos da pasta
git status
ls -la
```
- **Push x Pull x Clone:**
  - `push` = envia commits da máquina local para o GitHub.
  - `pull` = traz commits do GitHub para a máquina local, igualando os dois lados.
  - `clone` = copia um repositório inteiro (local ou remoto, público ou privado com acesso) para a máquina, já deixando o origin configurado.
- ⚠️ **Ponto de atenção:** um `push` pode falhar por conflito quando existem arquivos no remoto que não existem (ou estão diferentes) na máquina local — nesse caso, a aula mostra que é preciso rodar `git pull` antes, para sincronizar as duas pontas, só então repetir o `push`.
- 💡 **Dica:** tanto no clone quanto na conexão com HTTPS/SSH, a URL de origem segue o padrão `git@github.com:usuario/repositorio.git` (SSH) ou o equivalente em HTTPS — reforçando a configuração de autenticação já feita na aula anterior.

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[Repositório local (Git)] -> Existe um "origin" configurado?
  -> NÃO: [git push] -> erro (Git não sabe pra onde enviar)
  -> SIM: [origin aponta para a URL do repositório remoto no GitHub]

Como o origin é criado:
  [Quero copiar um repositório já existente]
    -> git clone <url> -> [baixa commits, autores e histórico] -> [origin criado automaticamente]

  [Quero conectar um repositório local vazio a um repositório novo no GitHub]
    -> git remote add origin <url>
    -> git branch -M main
    -> git push -u origin main
    -> [branch local "main" emparelhada com a branch remota "main"]

Depois de conectado:
  -> git push -> [commits locais sobem para o GitHub]
  -> git pull -> [commits remotos descem para a máquina local]
  -> Se houver arquivos diferentes nos dois lados -> conflito no push -> rodar git pull primeiro -> repetir o push
```

### 4. Links e Referências Oficiais
- **git remote** — comando usado para ver/gerenciar os repositórios remotos ligados ao local (`git remote -v`). Documentação: [git-scm.com/docs/git-remote](https://git-scm.com/docs/git-remote).
- **git clone** — copia um repositório remoto inteiro para a máquina local. Documentação: [git-scm.com/docs/git-clone](https://git-scm.com/docs/git-clone).
- **git push** — envia commits locais para o repositório remoto. Documentação: [git-scm.com/docs/git-push](https://git-scm.com/docs/git-push).
- **git pull** — traz commits do repositório remoto para o local. Documentação: [git-scm.com/docs/git-pull](https://git-scm.com/docs/git-pull).
- **branch main** — branch padrão criada automaticamente em todo repositório Git novo, citada na aula ao lado das branches `feature A` e `feature B` já vistas antes.
- **README, .gitignore, licença de software** — opções mencionadas na criação de um novo repositório no GitHub (não detalhadas nesta aula, ficaram marcadas como "assunto futuro").

### 🏛️ Conexão de Engenharia (Medallion & GCP)
Este conteúdo não mapeia diretamente para uma camada Bronze/Silver/Gold — é infraestrutura de versionamento, não processamento de dado. A conexão honesta aqui é com a **Frente 6 (Projeto de Portfólio)**: entender `origin`, `push`, `pull` e `clone` é o que vai permitir, na prática, subir cada estágio do pipeline (scripts de ingestão, transformação, modelos Dataform/BigQuery) para o repositório remoto do projeto conforme cada frente destravar uma etapa — sem isso, não há como versionar nem compartilhar o código que efetivamente vai rodar nas camadas de dado mais adiante.

---
**Salvar como:** `NN-rocketseat-git-github-origin-push-pull-clone-resumo.md` — no caderno (à mão) + repo do projeto (por ser aula de comandos, considere commitar na Frente 6). **Não** sobe na base de conhecimento.

Me diz o número desta aula dentro do módulo "GitHub e trabalho colaborativo" pra eu fechar o `NN` do nome — não vou chutar.