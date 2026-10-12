# 📌 README, License e Boas Práticas de Branch

### 1. Conceito Central
Esta aula cobre três elementos de "vitrine e governança" de um repositório GitHub: o **README** (a apresentação/cardápio do projeto), a **License** (o que terceiros podem ou não fazer com o código) e a disciplina de **manter branches limpas**. O fio que une os três é organização e comunicação: o README comunica o que o projeto faz, a licença comunica o que pode ser feito com ele, e branches limpas comunicam ao time o estado real do trabalho em paralelo.

### 2. Pontos-chave e Sintaxe
- **README**: é a "primeira impressão" do repositório — se alguém não entende minimamente o projeto depois de ler o README, ele falhou no propósito. Deve conter, no mínimo: nome e descrição, demonstração, como instalar, como usar, tecnologias utilizadas e como contribuir.
  - Escrito em **Markdown** (mesma linguagem de marcação usada em issues e PRs).
  - Ferramentas como o site **README.so** ajudam a gerar seções prontas (badges, autores, licença, variáveis de ambiente, etc.), mas o conteúdo final deve refletir o projeto real.
- **License**: define legalmente o que outras pessoas podem fazer com o código. **Sem licença declarada, na teoria ninguém pode usar/copiar o projeto livremente** — mesmo que, na prática, isso seja difícil de fiscalizar.
  - **MIT**: licença permissiva — permite uso comercial, modificação, distribuição e uso privado, desde que os créditos ao autor original sejam mantidos. Não permite uso de marca registrada (*trademark*) e isenta o autor de responsabilidade/garantia sobre o código.
  - **GPL**: além de permitir uso e modificação, **obriga que qualquer projeto derivado também seja aberto/público** — diferente da MIT, que permite criar algo proprietário/comercial a partir do código.
  - **Apache**: inclui proteção jurídica adicional contra uso indevido de patentes.
  - É possível criar o arquivo de licença manualmente (`LICENSE.md`) ou usar o template automático do GitHub, que já mostra um resumo das permissões, limitações e condições de cada licença antes de confirmar.
  - ⚠️ **Ponto de atenção:** colocar uma licença só faz sentido real em repositórios **públicos** — em um repositório privado, só quem já tem acesso (convidado) pode clonar, então a licença perde parte da utilidade prática.
- **Boas práticas de branch no GitHub** (reaproveitando os mesmos padrões já vistos em Git, ex: GitFlow, branches de feature/bugfix):
  - **Sempre apagar branches que já cumpriram seu propósito** (ex: após o merge de um pull request). Deixar branches antigas acumuladas gera dois problemas: (1) toda vez que alguém clona o repositório, todas as branches vêm junto, inflando o projeto; (2) a quantidade de branches ativas deveria refletir quanto trabalho paralelo realmente está em andamento — muitas branches "mortas" distorcem essa leitura para o time.
  - Apagar uma branch pode ser feito diretamente ao fechar um pull request, ou manualmente na visualização "View All Branches" do repositório.
  - A **branch padrão** (tag "default", geralmente `main`) é onde o GitHub entende que está o código mais atualizado/correto do projeto em produção — **essa branch não pode ser apagada**, e o GitHub também não permite deletar a última branch restante do repositório.
  - Deixar claro para o time **qual é o padrão de branching adotado** é tão importante quanto seguir o padrão em si — cada empresa pode adaptar o fluxo à sua cultura, desde que o time inteiro entenda e siga o mesmo critério.

### 3. 🧭 Implicações Práticas
- Um README incompleto afasta contribuidores em potencial: sem saber instalar, usar ou entender o propósito do projeto, ninguém se engaja nele.
- Publicar um projeto sem licença declarada deixa sua situação legal ambígua — quem quiser reutilizar o código tecnicamente não tem permissão clara para isso, mesmo que na prática aconteça.
- Escolher entre MIT e GPL depende do objetivo: MIT se você não se importa que o código vire parte de produtos fechados/comerciais; GPL se você quer garantir que qualquer trabalho derivado permaneça aberto.
- Repositórios com dezenas de branches obsoletas tornam mais difícil para o time enxergar, de forma confiável, quanto trabalho realmente está em andamento em paralelo — manter o hábito de apagar branches após o merge evita esse ruído acumulado.

### 4. Links e Referências Oficiais
- **README:** [About READMEs](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes) — documentação oficial sobre estrutura e boas práticas de README.
- **Licensing a repository:** [Licensing a repository](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository) — cobre como adicionar licença e os templates disponíveis no GitHub (MIT, GPL, Apache, entre outras).
- **Markdown:** [Basic writing and formatting syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) — sintaxe básica do Markdown usada em README, issues e PRs.
- **Choose a License:** [choosealicense.com](https://choosealicense.com/) — site independente, mas amplamente referenciado pela comunidade (inclusive pelo próprio GitHub), para comparar licenças de código aberto.

---
**Salvar como:** `08-rocketseat-git-github-readme-license-branch-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.