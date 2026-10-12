# 📌 Interface do GitHub, Fork e Issues

### 1. Conceito Central
Esta aula faz um tour pelos principais recursos da interface de um repositório no GitHub, complementando o que já foi visto sobre fluxo de comandos (clone, push, pull, fetch). Os destaques centrais são o **README** (documentação de apresentação do projeto), as **Issues** (tarefas ou problemas do projeto, organizáveis por labels e milestones), o **Fork** (cópia independente de um repositório de outra pessoa para a própria conta, sem vínculo de push direto com o original) e o quadro de **Projects** (gestão de tarefas em estilo Kanban integrado a issues).

### 2. Pontos-chave e Sintaxe
- **Repositório:** pasta central do projeto, podendo existir localmente (Git) ou remotamente (GitHub).
- **README:** arquivo que aparece na página principal do repositório, escrito em Markdown (linguagem de marcação, análoga ao HTML), usado para resumir do que se trata o projeto. Pode ser criado tanto pela interface do GitHub quanto localmente (ex: no VS Code) e depois enviado via push/pull.
- **Issues:** representam tarefas ou problemas do projeto. Podem receber **labels** (categorias, com opções padrão do GitHub ou customizadas), **assignees** (pessoa responsável por resolver), vínculo a **milestones** e a **projects**. Podem ser fechadas, reabertas, comentadas (também em Markdown) e marcadas como "Not Planned".
- **Milestones:** metas do projeto que agrupam um conjunto de issues — o GitHub calcula automaticamente a porcentagem de conclusão da milestone com base em quantas issues vinculadas estão fechadas.
- **Fork:** cópia de um repositório de outra pessoa para a própria conta. Diferente do clone, o fork não mantém vínculo de push direto com o repositório original — para enviar mudanças de volta, é necessário um **pull request** (assunto de aula futura). Ainda assim, o fork mantém referência ao repositório de origem, permitindo ações como "sync" (puxar atualizações de lá) ou tentar contribuir de volta.
- 🔎 **Observação:** não é possível fazer fork de um repositório para a mesma conta onde já existe um repositório com o nome idêntico — mas é possível ter repositórios de mesmo nome em contas diferentes.
- **Projects (quadro Kanban):** visão de gestão de tarefas vinculada a issues do repositório, com colunas como *Backlog* (não iniciadas), *Ready* (prontas para começar), *Em progresso*, *Em review* e *Done* (finalizada — e quando uma issue entra em Done, ela é automaticamente fechada/"closed"). Também oferece visões alternativas como *Priority board*, *Team items* e *Roadmap* (com datas de entrega).
- **Wiki:** espaço de documentação mais estruturado do repositório, com múltiplas páginas, aceitando Markdown, podendo ser clonado localmente para edição.
- **Outros elementos de interface citados:** branches e tags (navegáveis na mesma tela de arquivos), estrelas (indicam interesse de outros usuários), watch (monitorar atualizações do repositório), releases (versões lançadas, mais comuns em projetos open source), packages (pacotes do projeto), contribuidores (pessoas com acesso ativo ao projeto), seção de linguagens (porcentagem de cada linguagem de programação usada no repositório), segurança (políticas de reporte de vulnerabilidades, code scanning, secret scanning) e insights (métricas como issues/pull requests abertos e fechados, frequência de código, gráfico de dependências).
- 💡 **Dica:** a aula reforça que Wiki e Projects têm equivalentes em outras ferramentas de mercado (ex: Trello para gestão de tarefas) — o GitHub os integra nativamente ao repositório.

### 3. 🧭 Implicações Práticas
- Um README bem escrito é o primeiro contato de qualquer pessoa com o projeto — vale a pena mantê-lo atualizado conforme o projeto cresce.
- Organizar issues com labels e milestones permite acompanhar o progresso de uma entrega (ex: um fluxo de autenticação) de forma visual, sem depender de ferramentas externas.
- Fazer fork é o caminho indicado quando se quer experimentar ou acompanhar o código de outra pessoa (ex: repositórios de aula da Rocketseat) sem correr o risco de alterar o projeto original.
- O quadro de Projects (Kanban) permite enxergar o estado de todas as tarefas do repositório num só lugar, já automatizando o fechamento de issues quando movidas para "Done".
- A seção de Insights serve como termômetro de saúde do repositório — útil tanto em projetos pessoais quanto para avaliar o nível de atividade de projetos de terceiros antes de depender deles.

### 4. Links e Referências Oficiais
- **GitHub Issues** — gestão de tarefas/problemas do repositório. Documentação: [docs.github.com/issues](https://docs.github.com/en/issues).
- **GitHub Projects** — quadro Kanban integrado a issues do repositório. Documentação: [docs.github.com/issues/planning-and-tracking-with-projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects).
- **Fork** — cópia independente de um repositório de terceiros. Documentação: [docs.github.com/pull-requests/collaborating-with-pull-requests/working-with-forks](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks).
- **GitHub Wiki** — documentação integrada ao repositório. Documentação: [docs.github.com/communities/documenting-your-project-with-wikis](https://docs.github.com/en/communities/documenting-your-project-with-wikis).
- **Markdown** — linguagem de marcação usada em README, issues, comentários e Wiki. Documentação: [docs.github.com/get-started/writing-on-github](https://docs.github.com/en/get-started/writing-on-github).
- **Pull Request** — mecanismo para propor mudanças de um fork (ou branch) de volta ao repositório de origem; a própria aula adia o detalhamento para um conteúdo futuro.

### 🏛️ Conexão de Engenharia (Medallion & GCP)
Esta aula é sobre recursos de gestão e colaboração do GitHub (README, issues, fork, Kanban, wiki) — não há código de processamento de dado nem uma camada Bronze/Silver/Gold para conectar honestamente aqui. A ligação real é organizacional: issues e o quadro de Projects são a ferramenta natural para rastrear, na **Frente 6 (Projeto de Portfólio)**, cada "etapa de projeto" que as outras frentes forem destravando — por exemplo, abrir uma issue para "implementar camada Silver com Dataform" quando esse estágio for alcançado, em vez de deixar essas tarefas soltas fora do repositório.

---
**Salvar como:** `NN-rocketseat-git-github-interface-fork-issues-resumo.md` — no caderno (à mão) + repo do projeto (opcional, cópia digital). **Não** sobe na base de conhecimento.

Me diz o número desta aula dentro do módulo "GitHub e trabalho colaborativo" pra eu fechar o `NN` do nome — não vou chutar.