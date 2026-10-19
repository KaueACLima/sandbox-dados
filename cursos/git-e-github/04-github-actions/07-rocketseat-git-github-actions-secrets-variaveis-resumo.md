# 📌 Secrets e Variáveis no GitHub Actions

### 1. Conceito Central
Complemento da aula 06 (segurança). O GitHub separa dois tipos de informação que o workflow pode usar:

- **Secrets:** informações **sensíveis**. Se alguém malicioso tiver acesso, há problema.
- **Variáveis (*environment variables*, ou "informações de ambiente"):** valores que **mudam conforme o ambiente** (produção, testes do time) e **não são sensíveis**.

A diferença central é a **visibilidade do valor**. O secret fica oculto. A variável mostra o valor.

### 2. Pontos-chave e Sintaxe
- **Exemplos de secret:** chave de API (ex.: chave da OpenAI) e senha de banco de dados. São exemplos gerais, não algo que necessariamente esteja nos seus workflows.
- **Exemplos de variável:**
  - `environment`: guarda em que ambiente você está (desenvolvimento, staging, produção);
  - uma variável de decisão, como `should apply on restart` (o nome vem da fala, sem a grafia exata), com valor `true`/`false`: ao reiniciar o servidor, aplicar ou não uma modificação. O valor muda conforme o ambiente.
- **Onde cadastrar:** no repositório, em *Settings > Secrets and variables > Actions*. Há abas para **Secrets** e **Variables**.

#### Escopo: repositório vs. environment
- **Repository secrets/variables:** ficam disponíveis em **todo o repositório**, em qualquer ambiente.
- **Environment secrets/variables:** ficam disponíveis **só naquele environment**.
- Em *Manage environments* dá para criar novos ambientes (a aula mostra um já existente, o do GitHub Pages) e configurar **regras de proteção** (reviewers, tempo de espera) e secrets e variáveis próprios. O ambiente da demo não tinha reviewers nem tempo de espera, mas daria para configurar.
- ⚠️ **Secret preso a um ambiente** não pode ser usado em outros locais. Use quando quiser restringir o acesso a uma informação sensível. Já o secret de repositório serve para algo seguro, mas que qualquer ambiente pode acessar.
- A escolha depende do seu workflow e de como o time gerencia essas informações.

#### Diferenças práticas na hora de cadastrar
- **Secret:**
  - nome em **maiúsculas com underline** (o padrão);
  - depois de salvo, **ninguém vê o valor**: nem pela interface, nem por chamadas ou integrações. O campo fica travado;
  - depois de salvar, ele aparece listado no ambiente.
- **Variável:** o valor fica **visível** depois de salvo. Pode ser cadastrada no environment ou no repositório.
- 💡 **Regra prática:** sensível -> secret. Muda por ambiente e não é sensível -> variável.
- 🔎 O professor diz que "informação sensível" é um termo mais correto que "secreta".

### 3. 🏗️ Arquitetura / Diagrama Lógico
**Secret ou variável?**
```
[Informação para o workflow] -> O valor é sensível (chave de API, senha de banco)?
   SIM: [Secret: valor oculto e travado depois de salvo]
   NÃO: [Variável: valor visível, muda conforme o ambiente]
```

**Qual escopo?**
```
[Secret / variável cadastrado] -> Quem pode usar?
   Qualquer ambiente do repositório: [Repository secret / variable]
   Só um ambiente específico (ex.: restringir uso): [Environment secret / variable]
        -> Environment ainda aceita regras de proteção (reviewers, tempo de espera)
```

### 4. Links e Referências Oficiais
- [**GitHub Actions**](https://docs.github.com/actions): documentação oficial. Lá estão secrets, variáveis e environments.
- **Secrets:** informações sensíveis. O valor fica oculto e não é consultável depois de salvo.
- **Environment variables (variáveis de ambiente):** valores que variam conforme o ambiente, sem sensibilidade. Valor visível.
- **Environments:** ambientes configuráveis no repositório, com regras de proteção e secrets e variáveis próprios (ex.: reviewers, tempo de espera).
- **Repository secrets vs. environment secrets:** o primeiro vale para todo o repositório, o segundo só para o ambiente em que foi criado.

---
**Salvar como:** `07-rocketseat-git-github-actions-secrets-variaveis-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.