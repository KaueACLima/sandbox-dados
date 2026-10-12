# 📌 Criando uma Release

### 1. Conceito Central
Esta aula explica o conceito de **Release**: o marco oficial de uma nova versão publicada de um projeto, destinada a quem vai efetivamente usar o produto (cliente, outro dev, usuário final). A motivação central é que **commits, pull requests e issues não são, por si só, uma linha do tempo confiável do que o cliente realmente recebeu** — muita coisa no histórico técnico é refatoração, ajuste interno ou trabalho em andamento que nunca chega a ser "lançado". A release resolve isso: ela empacota um conjunto de mudanças em uma versão testada, revisada e pronta para o usuário final, de forma análoga a baixar uma nova versão de um app numa loja (você nunca baixa "commits", você baixa uma versão).

A aula também introduz o **versionamento semântico** (major.minor.patch) como o padrão de mercado para nomear essas versões de forma que qualquer pessoa entenda o impacto de cada lançamento só pelo número.

### 2. Pontos-chave e Sintaxe
- **Release** = versão publicada oficialmente do projeto, geralmente associada a uma **tag**. Marca não só um ponto do código, mas um ponto do *produto* — pronto para o usuário testar/usar.
- **Tag**: marcador em um commit específico, um checkpoint do histórico do Git. Pode ser criada via comandos na CLI e depois enviada (`push`) para o GitHub, ou diretamente pela interface ao criar a release.
- **Versionamento semântico (SemVer)** — padrão `MAJOR.MINOR.PATCH` (ex: `1.2.1`):
  - **Major** (1º número): incrementado quando a mudança **quebra compatibilidade** — ou seja, quem usava a versão anterior pode ter problemas ao atualizar (ex: uma versão de app que para de funcionar em dispositivos antigos).
  - **Minor** (2º número): incrementado ao adicionar uma **nova funcionalidade sem quebrar nada** do que já existia — quem já usava o projeto continua usando normalmente, só ganha recursos novos.
  - **Patch** (3º número): incrementado para **correção de bug**, sem alterar a forma como o usuário utiliza o produto — só conserta algo que estava quebrado.
  - Exemplo ilustrado na aula: `1.0.0` (sistema inicial) → `1.1.0` (login com Google, nova feature) → `1.1.1` (correção de um erro no login).
- **Como criar uma release no GitHub**: criar/selecionar uma tag (padrão comum: `v1.0.0`) → dar um título à release → escrever as notas de lançamento (o próprio GitHub pode gerar com IA a partir dos commits) → publicar (ou salvar como rascunho para revisar depois).
  - A release gera automaticamente um pacote de código baixável e referencia o último commit incluído naquele lançamento.
  - 💡 **Dica:** usar títulos claros nas notas de release (ex: indicando se há *fixes*, *features* ou *breaking changes*) ajuda a traduzir o trabalho técnico em algo compreensível para quem não acompanhou o desenvolvimento dia a dia.
- **Packages**: uma seção/conceito relacionado, mas distinto — é a forma de publicar um projeto como **pacote instalável** via um *registry* específico da tecnologia (ex: NPM para JavaScript, RubyGems para Ruby, NuGet para .NET, Apache Maven para Java, Containers para imagens Docker). Usado principalmente quando o projeto é uma biblioteca que outros devs vão instalar via linha de comando — diferente da release, que serve para qualquer tipo de produto.
- ⚠️ **Ponto de atenção:** repositórios populares (ex: React) podem ter **centenas de releases** acumuladas ao longo do tempo, cada uma documentando uma versão específica — é assim que o histórico de evolução de um produto open source fica visível e navegável publicamente.

### 3. 🧭 Implicações Práticas
- Sem releases, atualizar um projeto é como "atualizar um app sem saber se ele vai quebrar" — não há um marco claro de qual conjunto de mudanças compõe uma versão estável e testada.
- O versionamento semântico permite que qualquer pessoa, só olhando o número da versão, saiba se uma atualização é segura (patch/minor) ou exige atenção redobrada (major, risco de quebra de compatibilidade).
- Releases facilitam rollback: se uma versão nova tiver problema, é possível voltar para a release anterior enquanto o time corrige o bug via um novo pull request.
- Releases e packages atendem necessidades diferentes: releases documentam o produto/projeto como um todo para quem o usa; packages atendem especificamente quem vai instalar aquele código como dependência em outro projeto.

### 4. Links e Referências Oficiais
- **Releases no GitHub:** [About releases](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases) — documentação oficial sobre como criar, categorizar e publicar releases.
- **Versionamento Semântico (SemVer):** [Semantic Versioning 2.0.0](https://semver.org/) — especificação oficial do padrão major.minor.patch usado como referência de mercado.
- **GitHub Packages:** [About GitHub Packages](https://docs.github.com/en/packages/learn-github-packages/introduction-to-github-packages) — explica os registries suportados (npm, Maven, NuGet, RubyGems, containers) e como vincular pacotes ao repositório.

---
**Salvar como:** `09-rocketseat-git-github-criando-release-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.