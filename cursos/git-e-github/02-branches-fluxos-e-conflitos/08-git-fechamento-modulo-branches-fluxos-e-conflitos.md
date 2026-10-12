# 🏆 Fechamento de Módulo e Teste de Fixação — Branches, Fluxos e Conflitos

### 1. Resumo Executivo
Este módulo transformou o entendimento de branches de um conceito abstrato ("ramificações que isolam trabalho") em um conjunto de ferramentas concretas para gerenciar múltiplas linhas de desenvolvimento com segurança. A base é operacional: criar, listar e trocar de branch (`git branch`, `git checkout`/`git switch`), entendendo que cada branch herda o histórico da origem e depois evolui de forma independente até ser integrada de volta. A partir daí, o módulo se aprofunda em **como** integrar essas mudanças — e aqui está a grande lição técnica: merge, rebase e cherry-pick resolvem o mesmo problema de formas diferentes, e a escolha entre eles não é estética, é uma decisão sobre **preservar rastreabilidade vs. manter um histórico linear**. Merge é a escolha segura para branches compartilhadas (preserva quem fez o quê e quando); rebase é ideal para organizar o próprio trabalho local antes de entregar, mas nunca deve tocar uma branch que outras pessoas usam, sob risco de apagar rastreabilidade crítica; cherry-pick deve ser exceção, não rotina, porque duplica commits no histórico.

Essa camada de comandos ganha sentido de verdade quando confrontada com processo: o GitFlow (main, develop, feature, release, hotfix) mostra que um time saudável não decide "na hora" de onde criar uma branch ou para onde mandar um merge — isso é convenção, não intuição individual. Conventional Commits complementa essa disciplina no nível da mensagem de commit, dando a cada alteração um tipo (`feat`, `fix`, `refactor` etc.) que humanos entendem rapidamente e máquinas conseguem usar para automação (CI/CD, versionamento semântico). Por fim, o módulo fecha com stash (pausar trabalho em progresso sem sujar o histórico) e conflitos — o mecanismo pelo qual o Git devolve ao desenvolvedor, de forma segura e não automática, a decisão sobre qual versão de um trecho de código deve prevalecer quando duas alterações concorrem pela mesma linha.

A lição central para o dia a dia de um Analista/Engenheiro de Dados Júnior: versionamento sério não é sobre "saber o comando certo", é sobre entender a **consequência de cada escolha no histórico compartilhado** — especialmente relevante em repositórios de pipeline de dados (Dataform/BigQuery), onde um histórico corrompido ou reescrito na hora errada pode custar horas de investigação quando algo quebra em produção.

### 2. Glossário Técnico
- **Branch:** ramificação isolada do histórico de commits, usada para desenvolver algo sem afetar a linha principal do projeto.
- **Checkout / Switch:** comandos para trocar de branch; `switch` é a versão moderna e mais específica (não restaura arquivos como `checkout` faz).
- **Merge:** integra o histórico de uma branch em outra preservando a divergência real (cria um commit de união). É a escolha segura para branches compartilhadas e para consolidar um trabalho já organizado.
- **Rebase:** reaplica commits de uma branch sobre outra, reescrevendo o histórico para ficar linear — seguro apenas em branch **local e não compartilhada**, antes de abrir um Pull Request.
- **Cherry-pick:** traz um commit específico de uma branch para outra, criando um commit novo (hash diferente, mesmo nome) — duplica histórico se usado antes de um merge/rebase posterior; deve ser exceção, não rotina.
- **Stash:** guarda temporariamente alterações não commitadas, permitindo trocar de branch sem perder o trabalho em progresso e sem criar um commit incompleto.
- **GitFlow:** modelo de workflow com papéis fixos por branch — main (produção), develop (integração do time), feature (funcionalidade nova), release (preparação de lançamento), hotfix (correção urgente a partir da main, para não herdar mudanças ainda não lançadas que estão na develop).
- **Conventional Commits:** convenção de mensagens de commit no formato `tipo(escopo): descrição`. Tipos centrais: `feat` (funcionalidade nova), `fix` (correção de bug), `refactor` (mudança interna sem alterar comportamento externo) — a distinção entre esses três é o que permite automações precisas de CI/CD.
- **Conflito de merge:** situação em que o Git não consegue decidir sozinho qual de duas alterações concorrentes numa mesma região de arquivo deve prevalecer. A resolução correta raramente é "escolher um lado" — muitas vezes exige combinar manualmente as duas alterações (uma terceira versão) e validar (testes/compilação) antes de commitar a resolução.
- **WIP (Working in Progress):** nome padrão que o Git dá a um stash, indicando que aquele conteúdo é trabalho ainda não finalizado.

### 3. Correção Comentada do Teste de Fixação

**Questão 1 — Rebase local + entrega via merge.**
Acerto no núcleo: usar `rebase` para limpar um histórico pessoal desorganizado antes de compartilhar é a prática correta. O ajuste necessário: a **entrega para a branch compartilhada (`develop`) deve ser feita com `merge`**, não com outro rebase — a partir do momento em que a branch vira Pull Request contra uma branch compartilhada, aquele histórico não é mais reescrito. Regra de ouro: rebase é seguro **antes** de compartilhar; merge é seguro **para** compartilhar. Uso de Conventional Commits nos commits reorganizados é um acerto complementar.

**Questão 2 — Fluxo correto do hotfix.**
Sequência certa: stash → checkout na `main` → hotfix → merge na `main` (resolve produção) → merge também na `develop` (evita que o bug reapareça numa release futura) → volta à branch original → aplica e descarta o stash. Precisão sobre o *porquê* da origem na main: não é "porque é de lá que vem o bug" (o bug está no código, não na branch) — é porque a `main` é o espelho exato do que está em produção, e o hotfix precisa nascer desse estado exato, sem herdar mudanças ainda não lançadas que estão na `develop`.

**Questão 3 — Tipos de commit corrigidos; risco do conflito aprofundado.**
(a) Nenhum dos dois casos é `feat`. Reorganizar a lógica de uma agregação **sem mudar o resultado** é `refactor`. Corrigir a agregação que gerava valores errados é `fix`. `feat` seria reservado para uma funcionalidade nova — não é o caso aqui.
(b) O risco vai além de "perder uma feature de um colega": se a versão aceita for a do `refactor` (feita **antes** da correção do bug), o conflito resolvido incorretamente **reintroduz silenciosamente o bug de valores errados em produção**, porque a reorganização não incorporava a correção. A resposta certa quase nunca é escolher um lado — é combinar manualmente as duas alterações (refactor + fix) e rodar a compilação/testes do Dataform antes de commitar, para confirmar que a versão final não quebrou nem a lógica nem o dado.

---
**Definição de Pronto (DoD): 100%** — 8 aulas resumidas + quiz oficial do módulo (10/10) + teste de fixação corrigido.

**Salvar como:** `git-fechamento-modulo-branches-fluxos-e-conflitos.md` — na base de conhecimento.