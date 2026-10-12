# 🏆 Fechamento de Módulo e Teste de Fixação
**Trilha:** Rocketseat — Formação Data Analytics
**Nível:** 1 — Primeiros Passos
**Módulo:** O Trabalho de um Analista de Dados
**Data do fechamento:** 09/10/2026

### 1. Resumo Executivo
O módulo estabelece a base conceitual de toda a formação: antes de tocar em ferramenta técnica, é preciso entender o que é análise de dados, quem faz esse trabalho e com que princípio ele deve ser conduzido. A primeira aula ancora a ideia central — análise de dados é usar registros históricos para gerar insights que sustentem decisões de negócio, algo que já está presente em praticamente qualquer setor (redes sociais, bancos, agro, moda), não só em tecnologia. A segunda aula desdobra essa prática em três personas — analista, cientista e engenheiro de dados — que ocupam posições diferentes entre a camada de negócio e a camada técnica, mas que na prática têm limites fluidos e frequentemente se sobrepõem.

A terceira aula mostra que essa prática não segue um único caminho: CRISP-DM, Lean Analytics, DataOps e A/B Testing são metodologias distintas, cada uma adequada a um ritmo e a um tipo de pergunta — da análise pontual e profunda do CRISP-DM à decisão rápida e contínua do Lean Analytics. A quarta aula amarra tudo com os princípios que atravessam qualquer uma dessas metodologias: dado é meio, não fim; os quatro tipos de análise (descritiva, diagnóstica, preditiva, prescritiva) crescem em complexidade; os níveis de estruturação do dado (estruturado, semi-estruturado, não estruturado) afetam diretamente a dificuldade da análise; e uma estatística isolada (como a média) pode mentir se usada sem entender a distribuição completa dos dados.

A grande lição para um Analista Júnior: técnica sem contexto de negócio não gera valor. O módulo inteiro empurra para a mesma direção — antes de abrir qualquer ferramenta, entenda a pergunta, entenda os dados disponíveis, e nunca entregue um número sem verificar se ele realmente ajuda alguém a decidir algo.

### 2. Glossário Técnico
*Análise de dados:* avaliação de registros históricos para extrair insights que sustentem decisões de negócio — distinta de predição/machine learning, que ficam a cargo de outras personas do campo de dados.

*Analista, Cientista e Engenheiro de dados:* três personas do ecossistema de dados, posicionadas num espectro entre negócio (analista) e técnica pura (engenheiro), com o cientista fazendo a ponte via análises preditivas/prescritivas.

*CRISP-DM:* metodologia de mineração de dados estruturada em ciclo (compreensão do negócio → compreensão do dado → preparação → modelagem → avaliação → implantação), indicada para responder uma pergunta de negócio pontual e bem definida.

*Lean Analytics:* abordagem de análise contínua e rápida, baseada em definir métricas/KPIs e testar hipóteses constantemente, comum em empresas de tecnologia com decisão de alta frequência.

*DataOps:* metodologia derivada do DevOps, focada em automação e governança do ciclo de vida do dado — integração/entrega contínua, monitoramento e garantia de que o dado está íntegro e documentado.

*Tipos de análise (descritiva, diagnóstica, preditiva, prescritiva):* classificação pelo momento/intenção da análise — o que aconteceu, por que aconteceu, o que vai acontecer, o que fazer a respeito — em ordem crescente de complexidade.

*Dados estruturados, semi-estruturados e não estruturados:* classificação pelo nível de organização do dado (tabular / tipo JSON-logs / texto-vídeo-áudio), que afeta diretamente a dificuldade de análise.

*Outlier:* valor atípico dentro de um conjunto de dados que pode distorcer uma estatística resumo (como a média) e levar a uma leitura equivocada do comportamento real dos dados.

### 3. Desafio de Fixação (Quiz Interativo)

**Cenário:** Você é analista júnior numa rede de academias. A diretoria pergunta: "por que a taxa de renovação de matrícula caiu 15% no último trimestre?" e pede uma resposta rápida, em até duas semanas.

1. Dentre CRISP-DM, Lean Analytics, DataOps e A/B Testing, qual metodologia você escolheria como abordagem principal para responder a essa pergunta específica da diretoria? Justifique com base na natureza da pergunta (pontual vs. contínua) e não apenas no nome da metodologia.
2. Você reúne os dados de frequência dos alunos nos últimos 6 meses e calcula a média de visitas semanais por aluno: 3,2 visitas/semana. Um colega conclui: "a média está estável, então o problema não é frequência". Sem fazer nenhum cálculo adicional, aponte uma limitação dessa conclusão baseada só na média — o que ela pode estar escondendo?
3. Entre os dados que você teria disponível — frequência de check-in (tabela do sistema da academia), comentários de cancelamento no formulário de saída (texto livre), e um log de eventos do app (JSON com cliques e telas acessadas) — classifique cada um pelo nível de estruturação (estruturado, semi-estruturado, não estruturado) e diga qual deles provavelmente vai exigir mais trabalho de preparação antes de poder ser analisado.

### 4. Correção Comentada

**Questão 1 — ⚠️ Metodologia certa, justificativa incompleta.**
CRISP-DM é de fato a escolha certa aqui — mas o motivo não é "ter uma visão mais ampla do cenário" nem envolve teste A/B. O ponto-chave da aula 3 é que o CRISP-DM serve para responder **uma única pergunta de negócio pontual e fechada** ("por que a renovação caiu 15%?" é exatamente esse tipo de pergunta), enquanto Lean Analytics e A/B Testing servem para acompanhamento **contínuo** de métrica ou teste de variação de elemento — nenhum dos dois serviria bem para uma investigação diagnóstica única como essa. Vale reler esse critério (pontual vs. contínuo) porque é o que decide entre as quatro metodologias na prática, não o quão "ampla" é a análise.

**Questão 2 — ✅ Correta, e bem argumentada.**
Pegou exatamente o ponto: a média pode "estabilizar" escondendo um outlier (o aluno muito frequente puxando a média para cima, mascarando quem quase não aparece) — é o mesmo raciocínio do exemplo da sala com os 10 jovens e a pessoa mais velha, só que aplicado a um cenário novo. Reconhecer que uma média estável não garante frequência uniforme é a lição central da aula.

**Questão 3 — ⚠️ Duas certas, uma errada.**
Check-in (tabela do sistema) = **estruturado** ✅. Comentários de cancelamento (texto livre) = **não estruturado** ✅. Mas o **log de eventos do app em JSON** não é estruturado — a aula 4 cita JSON e logs de sistema como o exemplo-padrão de dado **semi-estruturado**: não está em formato tabular, mas também não é um texto solto — fica no meio-termo. Sobre a pergunta final (qual exige mais preparo): os comentários de cancelamento (não estruturado) são os que exigem mais trabalho antes de virarem algo analisável — texto livre não tem nenhuma organização prévia, enquanto o JSON do log, mesmo semi-estruturado, já carrega alguma hierarquia de campos reconhecível.

**Resultado:** 1 de 3 totalmente correta (Q2), 2 com acerto parcial (Q1 na escolha, não na justificativa; Q3 em 2 de 3 classificações). Vale fixar dois pontos: o critério pontual × contínuo pra escolher metodologia, e que JSON/logs são semi-estruturados, não estruturados.

---
**Nota de origem:** este módulo faz parte do "buraco de contexto" registrado no Core (aulas assistidas via gem do Gemini, antes do uso do notetaker). As transcrições originais foram recuperadas e processadas normalmente — não houve reconstrução por memória.
