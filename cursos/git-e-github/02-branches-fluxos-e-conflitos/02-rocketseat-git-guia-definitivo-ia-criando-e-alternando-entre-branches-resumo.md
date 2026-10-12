# 📌 Criando e Alternando entre Branches

### 1. Conceito Central
Esta aula sai da teoria e mostra na prática os comandos que operacionalizam o conceito de branches visto anteriormente: como listar, criar e trocar entre ramificações, e como integrar (merge) o conteúdo de uma branch em outra. O ponto central é entender que criar uma branch não é começar do zero — ela herda todo o histórico de commits da branch a partir da qual foi criada. A partir daí, cada branch evolui de forma independente: commits feitos numa branch (feature) não existem nas demais até que sejam explicitamente integrados via merge.

### 2. Pontos-chave e Sintaxe
```bash
# Lista todas as branches do projeto e indica em qual você está (com *)
git branch

# Cria uma nova branch (não troca para ela automaticamente)
# Padrão de mercado citado: feature/nome-da-funcionalidade
git branch feature/login-with-email-and-password

# Troca de uma branch para outra (processo chamado de "checkout")
git checkout feature/login-with-email-and-password

# Volta para a branch main
git checkout main

# Fluxo normal de commit funciona igual dentro de qualquer branch
git add .
git commit -m "login with email and password"

# Junta as mudanças de outra branch na branch atual
# (é preciso estar na branch que vai RECEBER a mudança)
git merge feature/login-with-email-and-password
```
- O nome de branch usado como exemplo segue um padrão de mercado: `feature/` como prefixo + nome descritivo da funcionalidade, em inglês, com palavras separadas por hífen.
- **Checkout** é o comando/processo de sair de uma branch e entrar em outra — o nome remete à ideia de "sair" de um ramo para "entrar" em outro.
- Uma branch nova herda todos os commits existentes da branch de origem no momento da criação; a partir daí, os históricos divergem.
- ⚠️ **Ponto de atenção:** o `git merge` precisa ser executado estando **na branch que vai receber** a mudança — ou seja, o comando não é "mande a feature para a main", é "estando na main, puxe as mudanças da feature". A direção do comando é sempre o inverso do que a leitura em português sugere.
- 🔎 **Observação:** depois do merge, as duas branches ficam com o mesmo conteúdo/commits — mas isso não significa que a branch de origem (feature) deva ser descartada automaticamente; a aula já sinaliza que "o que fazer com a branch depois do merge" será tema da próxima aula (boas práticas de merge e organização quando o projeto acumula muitas features).

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[main] -> git branch feature/login-with-email-and-password
        -> branch criada (herda commits da main), mas ainda estou em [main]

[main] -> git checkout feature/login-with-email-and-password -> agora estou em [feature]

[feature] -> git add . / git commit -> novo commit existe SOMENTE na [feature]

[feature] -> git checkout main -> volto para [main] -> commit da feature NÃO aparece aqui

[main] -> git merge feature/login-with-email-and-password
        -> commits da feature são integrados em [main]
        -> [main] e [feature] ficam com histórico idêntico
```

### 4. Links e Referências Oficiais
- **git branch:** lista, cria ou remove branches. Documentação oficial: [git-branch](https://git-scm.com/docs/git-branch).
- **git checkout:** troca a branch ativa (ou restaura arquivos, em outros usos). Documentação oficial: [git-checkout](https://git-scm.com/docs/git-checkout).
- **git merge:** integra o histórico de uma branch na branch atual. Documentação oficial: [git-merge](https://git-scm.com/docs/git-merge).
- **git add / git commit:** comandos de stage e commit já vistos em aulas anteriores, aqui reaplicados dentro do contexto de uma branch específica.
- **Padrão feature/nome-da-funcionalidade:** convenção de nomenclatura de branches citada como prática de mercado, sem uma página oficial única — vale pesquisar sobre "branch naming conventions" para ver variações comuns (feature/, fix/, hotfix/ etc.).

---
**Salvar como:** `NN-rocketseat-git-guia-definitivo-ia-criando-e-alternando-entre-branches-resumo.md` — no caderno (à mão) + repo do projeto (considere commitar na Frente 6, já que aqui entra código de terminal reproduzível). **Não** sobe na base de conhecimento.

Me diga o número desta aula dentro do módulo "Branches, fluxos e conflitos" pra eu fechar o nome do arquivo (troca o `NN`).

### 🏛️ Conexão de Engenharia (Medallion & GCP)
O fluxo `criar branch → commitar mudanças isoladas → merge na branch principal` é exatamente o padrão recomendado ao desenvolver models no Dataform: uma alteração ou novo model SQLX (por exemplo, uma nova tabela Silver derivando de uma Bronze) nasce numa branch de feature, é testado isoladamente (rodando `dataform compile`/assertions sem afetar a branch principal), e só é integrado à branch principal via merge depois de validado — que é o gatilho real de deploy da mudança no BigQuery em produção. O ponto de atenção sobre a direção do `git merge` (estar na branch que recebe) é especialmente relevante aqui: um merge feito a partir da branch errada pode sobrescrever silenciosamente lógica de produção da camada Gold. Essa disciplina de branch por funcionalidade é a etapa de projeto (Frente 6) que vale já aplicar no repositório do seu pipeline Bronze→Silver→Gold, em vez de commitar tudo direto na main.