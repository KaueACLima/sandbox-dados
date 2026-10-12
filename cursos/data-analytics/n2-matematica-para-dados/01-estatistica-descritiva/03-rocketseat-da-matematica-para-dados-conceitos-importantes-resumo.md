# 📌 Conceitos Importantes: População, Amostra e Variáveis

### 1. Conceito Central
Antes de entrar em média, moda e mediana, a aula estabelece três conceitos-base da estatística: a diferença entre **população** e **amostra**, e a classificação das **variáveis** em qualitativas ou quantitativas. Esses conceitos definem o que exatamente está sendo analisado e como cada coluna de uma tabela deve ser tratada — sem isso, o risco é tirar conclusões que não refletem a realidade do todo analisado.

### 2. Pontos-chave e Sintaxe
#### População e Amostra
- **População:** o todo que está sendo analisado (ex: todas as pessoas do Brasil, todos os funcionários de uma empresa). Cada elemento desse todo é chamado de **indivíduo**.
- **Amostra:** uma parcela/parte da população, usada quando não se analisa o todo (ex: analisar só o estado de São Paulo em vez do Brasil inteiro).
- ⚠️ **Ponto de atenção:** uma amostra precisa ser **representativa** da população. Uma amostra pequena demais, ou coletada de forma muito específica (ex: pesquisar só mulheres, ou só idosos), compromete a validade da análise — a conclusão pode não refletir o todo.

#### Variáveis
- **Variável** = cada coluna de uma tabela; representa uma característica ou informação de cada indivíduo (ex: idade, valor da compra, cidade, nome, sexo).
- Variáveis se dividem em dois tipos:
  - **Qualitativas:** representam categorias ou características (não numéricas por natureza de uso).
  - **Quantitativas:** representam valores numéricos que indicam quantidade ou medida (permitem soma, média).
- 💡 **Insight:** ser número não significa automaticamente ser quantitativa, e ser palavra não significa automaticamente ser qualitativa — o que importa é **o que a análise pretende fazer** com aquele dado.

#### Exemplos aplicados (tabela de cadastro de funcionários)
- Nome → qualitativa (não se soma ou tira média de nomes).
- Matrícula → quantitativa (permite soma, média).
- Sexo (masculino/feminino) → qualitativa.
- Idade → quantitativa.
- Mês de aniversário → quantitativa.
- **Data de nascimento** → por natureza é quantitativa (permite calcular idade, fazer contas entre datas). Porém, se usada para **categorizar** (ex: agrupar por signo, ou por período de nascimento), nesse uso específico ela está sendo tratada como qualitativa — mesmo sem mudar sua natureza.

### 3. 🧠 Raciocínio Lógico
- Primeiro, identifica-se o escopo da análise: está se olhando o todo (população) ou uma parte dele (amostra)?
- Se for amostra, pergunta-se: essa amostra é representativa, ou foi coletada de forma pequena/específica demais?
- Em seguida, para cada coluna de dados (variável), pergunta-se: essa informação pode ser somada/ter média calculada (quantitativa), ou representa uma categoria (qualitativa)?
- Mesmo quando a variável é quantitativa por natureza (como data de nascimento), o uso dado a ela na análise pode classificá-la como qualitativa (ex: categorizar por signo) — a decisão final depende da intenção da análise, não só do tipo de dado bruto.

---
**Salvar como:** `03-rocketseat-da-matematica-para-dados-conceitos-importantes-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.