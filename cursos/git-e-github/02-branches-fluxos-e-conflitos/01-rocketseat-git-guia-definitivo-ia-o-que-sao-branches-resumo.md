# 📌 O que são Branches?

### 1. Conceito Central
Branches (ramificações) são um dos conceitos mais fundamentais do Git, apesar de não fazerem parte da base mais elementar da ferramenta. A metáfora usada é a de uma árvore: o Git é o tronco principal e as branches são os galhos que se desprendem dele para permitir desenvolvimento paralelo sem interferir na linha principal. Cada branch representa um grupo de commits isolado — geralmente associado a uma funcionalidade ou correção específica — que só se integra ao projeto principal quando estiver pronto. Isso resolve um problema prático real: sem branches, qualquer alteração feita diretamente na linha principal arrisca quebrar o que já está em produção (o ambiente que o cliente final utiliza).

### 2. Pontos-chave e Sintaxe
- A branch principal é chamada de mercado geralmente de **main** ou **master** — é o código que está em produção, ou seja, o que o cliente final está usando.
- Times costumam ter uma branch **develop**, onde funcionalidades já implementadas são testadas internamente (QA, design, produto) antes de seguir para produção.
- **Features** são branches onde novas funcionalidades são desenvolvidas isoladamente; elas seguem para a develop, e só depois (já validadas) a develop é mesclada na main/master.
- Fluxo essencial: cada branch é um espaço de trabalho único e independente — isso permite que múltiplas pessoas (ou times inteiros) trabalhem em paralelo sem conflito, e depois as mudanças são unificadas via **merge**.
- 💡 **Dica:** o valor real de trabalhar com branches não é só "organização" — é a prevenção de erros: problemas são resolvidos *antes* do código alcançar a branch principal, o que resulta em maior estabilidade para quem usa o produto em produção.
- Comandos essenciais citados (sem sintaxe exata de linha de comando, só os conceitos): listar branches existentes, criar uma nova branch, mudar de uma branch para outra, e integrar (mesclar) duas branches.
- A aula adianta que a visualização gráfica das branches será feita na próxima aula usando o **GitGraph** (extensão do VS Code).

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[Feature (branch isolada)] -> desenvolvimento da funcionalidade
        -> merge em [Develop] -> testes internos (QA, design, produto)
                -> validação OK?
                        SIM: merge em [Main/Master] -> cliente final tem acesso
                        NÃO: ajustes continuam isolados na develop/feature, sem afetar produção
```

### 4. Links e Referências Oficiais
- **Branch (Git):** conceito de ramificação que isola um conjunto de commits do histórico principal. Vale consultar a documentação oficial do Git sobre o tema: [Git Branching – Branches in a Nutshell](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell).
- **Merge:** operação de integração que une o histórico de duas branches diferentes — mencionada na aula como o mecanismo usado para unir feature → develop → main.
- **Main/Master:** nome convencional de mercado para a branch de produção.
- **Develop:** branch intermediária de testes internos antes da entrega ao cliente.
- **GitGraph:** extensão citada para visualização gráfica de branches — a aula não detalhou o link oficial; vale buscar a página da extensão no VS Code Marketplace antes de instalar.

---
**Salvar como:** `NN-rocketseat-git-guia-definitivo-ia-o-que-sao-branches-resumo.md` — no caderno (à mão) + repo do projeto (considere commitar na Frente 6, já que documenta o fluxo que o projeto vai seguir no Git). **Não** sobe na base de conhecimento.

Me diga o número desta aula dentro do módulo "Branches, fluxos e conflitos" pra eu fechar o nome do arquivo (troca o `NN`).

### 🏛️ Conexão de Engenharia (Medallion & GCP)
Não há código nesta aula (é puramente conceitual sobre fluxo de branches), então a conexão aqui é sobre **processo**, não sobre camada de dado específica. O padrão feature → develop → main é exatamente a lógica que sustenta pipelines de dados versionados no Dataform/BigQuery: cada model SQLX novo ou alteração de lógica de transformação nasce numa branch de feature, é testado (equivalente à develop, rodando assertions e compilação) e só depois é mesclado na branch principal, que dispara o deploy real dos modelos Silver/Gold em produção. Isso destrava diretamente uma etapa do seu projeto de portfólio (Frente 6): o repositório Git que você está criando nesta trilha é o mesmo que vai versionar o pipeline Bronze→Silver→Gold — vale já nascer com essa disciplina de branch por funcionalidade, em vez de commitar tudo direto na main.