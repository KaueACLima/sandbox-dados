# 📌 Colaboração no GitHub com PRs

### 1. Conceito Central
Esta aula aprofunda o lado humano e processual do Pull Request, com exemplo real de um PR da própria Rocketseat. O foco sai da mecânica técnica (já vista na aula anterior) e vai para **como revisar código e colaborar bem em equipe**: o que de fato cabe revisar num PR, o que não cabe, como dar feedback sem ser hostil ou impositivo, como lidar com conflitos como parte natural da colaboração (não como erro), e boas práticas que evitam que código quebrado chegue à produção.

A mensagem central: código review não é apontar erros nem impor estilo pessoal — é **compartilhar contexto** (padrões da empresa, do projeto) com quem está entregando o código, de forma objetiva e respeitosa.

### 2. Pontos-chave e Sintaxe
- Fluxo revisado de um PR: criar branch → commits pequenos e claros (foco em poucas mudanças por commit) → abrir PR → revisão por outro dev → ajustes → **merge controlado** (só depois que o código foi validado como o melhor possível para aquela branch alvo).
- 💡 **Insight da aula:** branches não são só uma técnica de versionamento — são **isolamento de contexto**: protegem o projeto enquanto o trabalho acontece em paralelo, e o PR garante que só código revisado chegue à `main`.
- **Casos de uso típicos de PR:** features novas, bug fixes urgentes (mesmo urgentes, idealmente passam por revisão — um dev sênior com muito contexto pode, em alguns casos, agir sozinho) e refatorações feitas **separadamente** de novas funcionalidades (evitar misturar os dois).
- **O que revisar em um PR:**
  - **Clareza de código**: dá para entender o que o código faz ao lê-lo, tendo o contexto do projeto.
  - **Padrões do projeto**: ex. se o padrão do time é `function nome() {}` e o dev escreveu uma arrow function (`const funcao = () => {}`), isso é um ponto a trazer — ambos funcionam, mas fugir do padrão do projeto prejudica a consistência.
  - **Possíveis bugs** introduzidos pela mudança.
  - **Legibilidade**: nomes de variáveis claros, facilidade de leitura (diferente de clareza, que é sobre o propósito do código).
- **O que NÃO revisar:** preferência pessoal de estilo ("se eu fosse você, eu faria assim") quando o código já está claro, legível, sem bugs e seguindo os padrões do projeto — isso é revisão enviesada, não técnica.
- **Como dar feedback de revisão:**
  - Seja objetivo; evite tom pessoal/informal demais (o PR é documentação, não uma conversa entre amigos).
  - **Sugira, não imponha** — trazer o porquê da sugestão, não só a ordem.
  - Nunca diga "isso está errado/ruim"; prefira formulações como "esta abordagem pode gerar problema em X cenário, o que você acha de tentar Y?" ou "talvez possamos melhorar a legibilidade estendendo esta função".
  - Code review é sobre **compartilhar contexto** (padrões da empresa/projeto), não apenas apontar falhas — alguém tecnicamente competente pode simplesmente não conhecer ainda os padrões daquele time específico.
- **Resolução de conflitos em equipe:** atualizar a branch → identificar o conflito → escolher ou combinar as mudanças → testar → commitar a solução. ⚠️ **Ponto de atenção:** conflito não é erro, é sinal natural de colaboração (várias pessoas mexendo no mesmo código); resolver no automático sem entender o porquê pode gerar problemas na base de código — converse com quem fez a outra mudança, ou com alguém mais experiente, antes de decidir.
- **Boas práticas reforçadas:** nunca aprovar/mergear sem revisão real; rodar testes automatizados antes do merge; usar CI/CD quando possível. Um PR aprovado sem teste e sem boas práticas quebra código em produção.
- **Mini checklist antes de aprovar um PR:** é pequeno? tem nome claro? foi testado? teve review feito? não tem conflitos (ou já foram resolvidos)?
- Exemplo real trazido: um PR do autor para um bot interno da Rocketseat teve revisão de um colega (Elias) pedindo para remover alterações de arquivos fora do escopo da feature (mudanças de build/melhorias gerais misturadas com a feature principal) — o autor então fez um novo commit só com a feature pedida, sem refatorações extras, e o PR foi aprovado e mergeado.

### 3. 🧭 Implicações Práticas
- Um PR grande demais, mesmo tecnicamente correto, pode gerar mais atrito na revisão — PRs pequenos e focados em uma única entrega facilitam tanto a revisão quanto a comunicação de contexto.
- Misturar refatoração com feature nova no mesmo PR dificulta a revisão, porque o revisor precisa separar mentalmente "isso é mudança de comportamento" de "isso é só reorganização" — por isso a recomendação de mantê-las em PRs separados.
- O padrão de PR (tamanho, tom, nível de detalhe) varia de empresa para empresa — não existe um "jeito certo" universal, mas existe o padrão daquele time específico, que se aprende com os primeiros PRs e com a comunicação ativa com o time.
- Tratar o conflito como comunicação (e não como obstáculo técnico a ser resolvido no automático) reduz o risco de "resolver errado" e gerar um novo bug na base de código.
- Dar feedback com sugestões em vez de ordens tende a gerar evolução real no dev que recebe a revisão, em vez de só obediência pontual.

---
**Salvar como:** `07-rocketseat-git-github-colaboracao-com-prs-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.