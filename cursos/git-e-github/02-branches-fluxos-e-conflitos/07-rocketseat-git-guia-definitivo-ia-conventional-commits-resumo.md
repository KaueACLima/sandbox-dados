# 📌 Conventional Commits

### 1. Conceito Central
Conventional Commits é uma convenção para escrever mensagens de commit de forma padronizada e estruturada, tornando-as legíveis tanto por humanos quanto por máquinas. O ganho prático vai além de organização: mensagens padronizadas permitem automações — por exemplo, um robô de CI pode analisar o prefixo do commit e decidir, sem intervenção humana, se deve rodar testes automatizados, gerar uma nova versão do software ou disparar outro processo. A estrutura básica é **tipo(escopo opcional): descrição curta**, escrita diretamente na mensagem do commit (`git commit -m "tipo: descrição"`), sem alterar nenhum outro aspecto do fluxo de commit já conhecido.

### 2. Pontos-chave e Sintaxe
```bash
# Estrutura geral: tipo(escopo opcional): descrição curta
git commit -m "feat(carrinho): adicionar cálculo automático de frete"
git commit -m "fix(login): corrigir erro ao autenticar usuários com senha longa"
```

**Tipos de Conventional Commits apresentados na aula:**
- **feat** — nova funcionalidade adicionada ao sistema. Ex: `feat(carrinho): adicionar cálculo automático de frete`.
- **fix** — correção de bug. Ex: `fix(login): corrigir erro ao autenticar usuários com senha longa`.
- **docs** — alteração em documentação, geralmente interna (README, Wiki). Ex: `docs: atualizar instruções de instalação do README`.
- **style** — mudança que não altera o comportamento do código, só a forma como ele é escrito (espaçamento, indentação, ponto e vírgula). Ex: `style(botao): ajustar indentação e remover espaços desnecessários`.
- **refactor** — mudança interna no código que não altera o comportamento externo (reorganização, separação de lógica). Ex: `refactor(auth): separar lógica de autenticação em um service`.
- **perf** — melhoria de performance/velocidade para o usuário final. Ex: `perf(api): otimizar consulta de usuários com cache`.
- **test** — adição ou correção de testes automatizados. Ex: `test(usuario): adicionar testes unitários para criação de usuários`.
- **build** — mudanças relacionadas à build final da aplicação ou às dependências externas do projeto (ex: React, Node, Webpack, Docker). Ex: `build: atualizar dependências do projeto`.
- **ci** — alterações em pipelines de CI/CD (ex: GitHub Actions, GitLab CI, Jenkins). Ex: `ci: adicionar pipeline de testes no GitHub Actions`.
- **chore** — tarefas gerais que não afetam o código em si (configuração de ferramentas, scripts de manutenção). Usado também quando nenhuma outra categoria se encaixa bem. Ex: `chore: configuração do ESLint`.
- **revert** — reverte um commit anterior, removendo algo do histórico. Ex: `revert: remover integração com a API antiga de pagamentos`.
- **BREAKING CHANGE** — indica quebra de compatibilidade (o código deixa de funcionar como antes a partir daquele ponto). Sinalizado com uma exclamação após o tipo/escopo e detalhado no corpo da mensagem. Ex: `feat(api)!: mudança não funciona mais em conjunto com o HubSpot`.
- 💡 **Dica:** a categorização exata pode variar por empresa/projeto — os tipos mais consolidados e difíceis de não encontrar em qualquer convenção são `feat`, `fix`, `docs` e `style`; os demais são frequentes, mas passíveis de adaptação.
- 🔎 **Observação:** Conventional Commits **não depende** de um fluxo de branches estruturado como o GitFlow. Um projeto individual, sem clientes e sem necessidade de múltiplas branches, pode perfeitamente adotar Conventional Commits mesmo commitando tudo numa única branch — as duas práticas são independentes e se complementam quando usadas juntas.
- Existe uma extensão de VS Code chamada "Conventional Commits" (do Vivax) que auxilia a padronizar e adicionar ícones às mensagens de commit seguindo essa convenção.

### 3. 🧠 Raciocínio Lógico
- Um commit é feito → uma automação de CI pode ler o prefixo da mensagem → se o prefixo indicar `feat`, a automação pode, por exemplo, disparar testes automatizados → se não corresponder a nenhum tipo relevante para aquela automação, nada é disparado.
- Ao longo do desenvolvimento de uma funcionalidade, é comum encadear vários tipos de commit em sequência dentro da mesma branch — por exemplo: `feat` (a funcionalidade nova) → `fix` (correção de um problema encontrado) → `refactor` (reorganização da lógica) → `test` (adição de testes) → `docs` (documentação do flufo) — cada um representando uma etapa distinta e rastreável do mesmo trabalho, que no final se consolida numa entrega coesa quando a branch é integrada.

### 4. Links e Referências Oficiais
- **Conventional Commits (especificação):** convenção formal de mensagens de commit estruturadas. Documentação oficial: [conventionalcommits.org](https://www.conventionalcommits.org/).
- **feat / fix / docs / style / refactor / perf / test / build / ci / chore / revert:** tipos padrão da convenção, cada um mapeando uma categoria distinta de mudança no código ou no projeto.
- **BREAKING CHANGE:** marcação formal dentro da convenção para indicar quebra de compatibilidade — geralmente ligada também ao versionamento semântico (SemVer), mencionado de forma indireta ao se falar em "gerar uma nova versão do software".
- **GitHub Actions / GitLab CI / Jenkins:** ferramentas de CI/CD citadas como exemplo de onde essas automações baseadas em tipo de commit efetivamente rodam — tema que a aula adianta ser aprofundado mais à frente no curso.

---
**Salvar como:** `NN-rocketseat-git-guia-definitivo-ia-conventional-commits-resumo.md` — no caderno (à mão) + repo do projeto (considere commitar na Frente 6, já que é uma convenção diretamente aplicável ao histórico de commits do projeto). **Não** sobe na base de conhecimento.

Me diga o número desta aula dentro do módulo "Branches, fluxos e conflitos" pra eu fechar o nome do arquivo (troca o `NN`).

### 🏛️ Conexão de Engenharia (Medallion & GCP)
Conventional Commits se conecta diretamente a pipelines de dados automatizados: num repositório Dataform, um commit `feat(gold): adicionar agregação de receita mensal` ou `fix(silver): corrigir tipo de coluna em transformação de datas` permite que uma pipeline de CI/CD (por exemplo, rodando no Cloud Build) decida automaticamente se deve apenas compilar/validar o projeto (`style`, `docs`, `refactor`) ou também rodar um deploy completo dos models alterados no BigQuery (`feat`, `fix`). Isso também facilita a rastreabilidade em produção: se uma tabela Gold apresentar dado incorreto, procurar por commits `fix` ou `feat` recentes que tocaram aquele model é muito mais rápido do que vasculhar mensagens genéricas sem padrão. Vale adotar essa convenção desde já no repositório do seu projeto de portfólio (Frente 6), mesmo trabalhando sozinho — o hábito compensa quando o projeto crescer ou for usado como peça de portfólio para mostrar a recrutadores.