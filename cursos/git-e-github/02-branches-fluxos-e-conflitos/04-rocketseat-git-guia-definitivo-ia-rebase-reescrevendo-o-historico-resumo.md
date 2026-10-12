# 📌 Rebase: Reescrevendo o Histórico

### 1. Conceito Central
Esta aula compara `merge` e `rebase` — dois comandos que resolvem o mesmo problema (integrar mudanças de uma branch em outra), mas produzem históricos com formatos visuais diferentes. O `merge` preserva o histórico real de como as branches divergiram e se uniram, criando um commit específico de união — o resultado é um histórico fiel, porém ramificado (várias bifurcações visíveis). O `rebase` faz algo distinto: ele remove temporariamente os commits da branch atual, atualiza a base a partir da branch de destino, e reaplica esses commits como se tivessem sido criados a partir dali — o resultado é um histórico linear, sem bifurcações, mas que **reescreve** a origem real dos commits. A escolha entre os dois não é sobre qual é "melhor", e sim sobre se você quer manter o histórico real (merge) ou um histórico limpo e linear (rebase) — isso tem implicações diretas de segurança quando a branch é compartilhada.

### 2. Pontos-chave e Sintaxe
```bash
# Puxa (integra) os commits da branch feature para a branch atual (main),
# preservando o histórico de divergência e criando um commit de união
git checkout main
git merge feature

# Reaplica os commits da branch atual sobre o topo da branch indicada,
# reescrevendo o histórico para ficar linear
git checkout main
git rebase feature
```
- **Merge:** o Git identifica o ponto comum entre as branches, combina os commits e cria um commit de união (exceto em casos de *fast-forward*, quando não há necessidade de commit extra). Mantém histórico fiel e auditável — dá para rastrear quem fez o quê e quando.
- **Rebase:** reescreve o histórico para ficar linear. Na prática, os commits da branch atual são temporariamente removidos, a base é atualizada, e os commits são "reaplicados" como se tivessem acontecido depois — por isso o histórico final não tem bifurcação.
- ⚠️ **Ponto de atenção (o mais importante da aula):** **nunca faça rebase numa branch que outras pessoas estão usando.** Como o rebase reescreve o histórico, ele apaga o rastro de quem fez cada alteração e quando — em uma branch compartilhada isso pode tornar praticamente impossível rastrear quem introduziu um bug.
- 💡 **Dica:** merge é a escolha mais segura para branches compartilhadas (main, develop) e para times grandes, justamente porque preserva o histórico real. Rebase é indicado para branches locais e individuais — organizar o próprio trabalho antes de abrir um pull request.
- 🔎 **Observação:** o fluxo recomendado combina os dois: usar `rebase` localmente para limpar/unificar o histórico de várias branches pessoais, e depois usar `merge` para entregar esse resultado já organizado na branch principal do time — assim você ganha histórico limpo na sua parte sem sacrificar a rastreabilidade na branch compartilhada.
- Desvantagem do merge: com o tempo, o histórico fica poluído/complexo, dificultando a leitura para quem chega no projeto depois. Desvantagem do rebase: perde-se a informação de data/autoria original dos commits, e conflitos podem se repetir de forma mais agressiva durante o processo.
- Na regra de bolso da aula: "na dúvida, use merge" — é a opção mais segura na maioria dos casos.

### 3. 🧠 Raciocínio Lógico
- Duas branches (main e feature) divergem de um ponto comum de commits.
- Se a integração for feita com **merge**: o Git cria um commit adicional que conecta explicitamente as duas pontas → histórico mostra a bifurcação real, com data e autoria de cada lado preservadas.
- Se a integração for feita com **rebase**: o Git remove os commits da branch atual, reposiciona a base, e os reaplica em sequência sobre a outra branch → histórico final parece uma única linha reta, sem marca visível de que houve divergência.
- O conteúdo final do código é o mesmo nos dois casos (o último commit da feature é idêntico) — a diferença é exclusivamente na forma como o histórico registra o caminho até ali.
- Decisão prática: branch é compartilhada com outras pessoas? → merge. Branch é só sua, local, antes de abrir PR? → rebase é seguro e deixa o histórico mais limpo para quem for revisar depois.

### 4. Links e Referências Oficiais
- **git merge:** integra branches preservando o histórico de divergência. Documentação oficial: [git-merge](https://git-scm.com/docs/git-merge).
- **git rebase:** reaplica commits sobre outra base, linearizando o histórico. Documentação oficial: [git-rebase](https://git-scm.com/docs/git-rebase).
- **Fast-forward:** tipo de integração em que o Git não precisa criar um commit de união porque não há divergência real entre as branches — mencionado como exceção ao comportamento padrão do merge.
- **Pull Request:** citado como o momento em que o código de uma branch é proposto para entrar na branch principal — contexto em que a escolha entre merge/rebase prévio faz diferença na legibilidade do histórico final.

---
**Salvar como:** `NN-rocketseat-git-guia-definitivo-ia-rebase-reescrevendo-o-historico-resumo.md` — no caderno (à mão) + repo do projeto (considere commitar na Frente 6, já que traz comandos de terminal reproduzíveis). **Não** sobe na base de conhecimento.

Me diga o número desta aula dentro do módulo "Branches, fluxos e conflitos" pra eu fechar o nome do arquivo (troca o `NN`).

### 🏛️ Conexão de Engenharia (Medallion & GCP)
A regra de ouro desta aula — "nunca faça rebase numa branch compartilhada" — é diretamente aplicável ao seu repositório de pipeline Dataform/BigQuery: se a branch principal do projeto (a que representa o estado real da camada Gold em produção) for reescrita via rebase por engano, você perde a rastreabilidade de qual model/alteração causou uma quebra específica num job de transformação — informação crítica quando o pipeline falha em produção e é preciso investigar "quem mudou o quê e quando". O padrão recomendado na aula (rebase local para organizar commits próprios + merge para entregar na branch principal) se encaixa bem como convenção a adotar já na etapa de projeto (Frente 6): mantém seu histórico de desenvolvimento limpo sem sacrificar a auditabilidade da branch que efetivamente alimenta o pipeline em produção.