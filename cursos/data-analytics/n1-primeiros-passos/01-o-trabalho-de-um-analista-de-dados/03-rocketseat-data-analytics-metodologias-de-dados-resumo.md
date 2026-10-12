# 📌 Metodologias de Análise de Dados

### 1. Conceito Central
Nem toda análise de dados segue o mesmo processo — existem diferentes metodologias, cada uma adequada a um tipo de problema e a um ritmo de entrega diferente. A aula apresenta quatro: **CRISP-DM** (a mais completa e o foco principal da formação), **Lean Analytics** (voltada para decisão rápida e contínua), **DataOps** (automação e governança do ciclo de vida do dado, mais ligada a engenharia/ciência de dados) e **A/B Testing** (experimentação baseada em dados, herdada de UX/Marketing). Essas quatro não são excludentes — é comum usar mais de uma ao mesmo tempo, dependendo do problema — e, segundo a aula, três delas podem ser vistas como aplicações mais específicas do que o CRISP-DM já cobre de forma ampla, com exceção do DataOps, que tem foco mais técnico/estrutural.

### 2. Pontos-chave e Sintaxe
- **CRISP-DM** é indicada para análises pontuais, com objetivo de responder a **uma pergunta de negócio fechada** — diferente de, por exemplo, construir um dashboard de acompanhamento contínuo de indicadores.
- **Lean Analytics** ("enxuta") prioriza testar e decidir rápido, reduzindo o tempo de desenvolvimento da análise; segue a lógica de definir métricas/KPIs, medir constantemente e testar hipóteses em cima disso.
  - Exemplos citados: a Netflix personaliza as thumbnails de filmes/séries conforme o gosto de cada usuário (romance, terror etc.) para testar o que gera mais cliques; e-commerces acompanham métricas de carrinho abandonado; apps de transporte (Uber) ajustam precificação dinâmica das corridas.
- **DataOps** vem da lógica do DevOps, aplicada ao ciclo de vida do dado. Seus componentes principais: integração e entrega contínua de dados, automação de coleta/processamento/análise, e monitoramento + **governança de dados** contínuos.
  - ⚠️ **Ponto de atenção:** governança de dados envolve garantir que o dado está íntegro e documentado (ex: colunas de uma tabela cujo significado ninguém sabe mais explicar) e que segue regras como a LGPD — a ausência disso é sinal de falta de governança, problema que o DataOps busca resolver.
- **A/B Testing** é um processo de experimentação: definir uma hipótese, criar duas ou mais versões de um elemento, testar com um grupo de usuários, analisar os resultados e aplicar a versão vencedora. É mais comum em empresas de tecnologia com produto B2C (contato direto e em massa com o público final).
- 💡 **Observação:** dados não pertencem só a analistas e cientistas de dados — o A/B Testing é um exemplo de como outras áreas (como UX) também praticam análise de dados dentro da própria especialidade.

### 3. 🏗️ Arquitetura / Diagrama Lógico
Ciclo de fases do CRISP-DM (com idas e voltas entre etapas adjacentes, não é um fluxo estritamente linear):

```
[Compreensão do Negócio] -> definição do problema + conversa com stakeholders
      -> [Compreensão do Dado] -> quais dados existem/faltam para responder a pergunta?
            (pode voltar para Compreensão do Negócio se faltar dado)
      -> [Preparação do Dado] -> limpeza e normalização
      -> [Modelagem] -> aplicação de estatística/machine learning sobre o dado preparado
            (pode voltar para Preparação do Dado se surgir problema no dado durante a modelagem)
      -> [Avaliação] -> validação dos resultados pelos stakeholders definidos
      -> [Implantação/Deploy] -> automatiza o modelo para que continue funcionando sem refazer a análise manualmente
```

### 4. Links e Referências Oficiais
- **CRISP-DM:** metodologia de mineração de dados citada como a mais completa da aula. Vale buscar a documentação/descrição oficial do processo (ex: [CRISP-DM Guide](https://www.ibm.com/docs/en/spss-modeler/18.5.0?topic=guide-crisp-dm-help-overview)) para aprofundar cada fase.
- **LGPD:** mencionada no contexto de governança de dados dentro do DataOps — mesma referência oficial já indicada na aula anterior ([gov.br/LGPD](https://www.gov.br/cidadania/pt-br/acesso-a-informacao/lgpd)).

---
**Salvar como:** `03-rocketseat-data-analytics-metodologias-de-dados-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.
Resta 1 aula neste módulo ("O Trabalho de um Analista de Dados").