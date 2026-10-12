# 📌 Introdução às Medidas de Dispersão

### 1. Conceito Central
Medidas de dispersão quantificam o quanto os valores de um conjunto de dados estão espalhados ou concentrados em torno da média. A motivação central do módulo é corrigir uma fragilidade das medidas de tendência central (média, moda, mediana): elas resumem um conjunto de dados em um único número, mas duas bases distintas podem compartilhar exatamente a mesma média e, ainda assim, representar realidades completamente diferentes — uma com valores próximos entre si (concentrados), outra com valores muito afastados (dispersos). Sem medir essa dispersão, uma análise apoiada só na média corre o risco de levar a uma conclusão equivocada.

### 2. Pontos-chave e Sintaxe
- O módulo mede a **distância dos dados em relação às medidas de tendência central** (principalmente a média) — é um complemento direto do que foi calculado no módulo anterior, não um conceito isolado.
- **Dados dispersos/espalhados** vs. **dados concentrados**: dois polos que uma mesma média pode esconder.
- ⚠️ **Ponto de atenção:** a média, isoladamente, pode ser "traiçoeira" — ela não diferencia um conjunto de valores homogêneos de um conjunto de valores extremos que por acaso resultam no mesmo valor médio. É exatamente essa lacuna que as medidas de dispersão (próximas aulas) vêm preencher.

### 3. 🧠 Raciocínio Lógico
- Duas bases de dados podem ter a mesma média.
- Calcular só a média não revela como os valores individuais se distribuem ao redor dela.
- Uma base pode ter valores concentrados perto da média → baixa dispersão.
- Outra pode ter valores muito afastados da média → alta dispersão.
- Ao analisar apenas a média, o analista pode tirar uma conclusão precipitada ("um susto") sobre o comportamento real dos dados.
- Logo: medir a dispersão é necessário para validar (ou desconfiar d)o que a média sozinha sugere.

---
**Salvar como:** `01-rocketseat-da-medidas-de-dispersao-introducao-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.

Essa aula é só a introdução motivacional do módulo — ainda não entra em nenhuma fórmula ou medida específica (amplitude, variância, desvio padrão etc.), por isso o resumo saiu enxuto por natureza, não por omissão. Manda a próxima quando tiver.