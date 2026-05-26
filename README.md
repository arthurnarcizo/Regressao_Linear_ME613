# Análise Preditiva do Mercado Imobiliário de Seattle por Meio de Modelos de Regressão

Este repositório contém o desenvolvimento do projeto prático final para a disciplina **ME613 - Análise de Regressão** do Instituto de Matemática, Estatística e Computação Científica (IMECC) da **UNICAMP**, realizado no segundo semestre de 2025.

O objetivo principal deste trabalho é modelar estatisticamente e prever o valor de mercado de imóveis na região de Seattle (Condado de King, EUA) a partir de suas características estruturais, qualitativas e geográficas, aplicando e contrastando diferentes abordagens de regressão linear múltipla.

---

## 👥 Autores
* **Amanda Nogueira Pereira** — RA 257134
* **Arthur Lourenço Narcizo da Silva** — RA 236043
* **Gabriel Campovilla da Silva** — RA 193625
* **Docente:** Profª. Drª. Tatiana Benaglia

---

## 📊 Estrutura do Conjunto de Dados
O estudo utiliza um ecossistema de dados composto por **21.613 observações** e 22 variáveis originais. Como tratamento inicial e refinamento metodológico, realizou-se o **ajuste inflacionário** dos preços coletados entre 2014 e 2015 para garantir consistência temporal nas modelagens estatísticas.

As principais variáveis analisadas incluem:
* `price`: Valor de venda do imóvel (variável resposta).
* `sqft_living` / `sqft_lot`: Área útil interna e do terreno (em pés quadrados).
* `grade`: Índice de qualidade da construção e design do imóvel.
* `condition`: Condição geral de conservação da propriedade.
* `waterfront`: Variável binária indicando se há vista para a água.
* `lat` / `long`: Coordenadas geográficas de localização.

---

## 🛠️ Metodologia e Modelos Implementados
A modelagem foi conduzida integralmente utilizando a linguagem **R**. Para contornar problemas clássicos de modelagem de dados reais (como assimetria severa, *outliers* e heterocedasticidade), foram construídas e validadas quatro abordagens analíticas:

1. **Mínimos Quadrados Ordinários (OLS Baseline):** Modelo de partida global para identificar as variáveis com maior significância estatística. Obtendo um $R^2$ ajustado de `0.6985`.
2. **Regressão com Penalização LASSO:** Utilizado para seleção automatizada de atributos (*feature selection*) e regularização de variância. O modelo removeu com sucesso coeficientes redundantes (`sqft_basement`, por exemplo) mantendo o mesmo poder preditivo.
3. **Modelo Log-Log (Transformação Logarítmica):** Aplicação do logaritmo natural na variável resposta e nos preditores contínuos de área. **Foi o modelo de melhor desempenho prático**, alcançando um $R^2$ ajustado de `0.7508` e reduzindo o RMSE para `249.745,2`. Essa técnica corrigiu de forma eficiente as violações de homocedasticidade e normalidade dos resíduos.
4. **Mínimos Quadrados Ponderados (WLS):** Tentativa de correção analítica da heterocedasticidade. Embora tenha inflado o $R^2$ para `0.8867`, o modelo violou drasticamente as premissas de diagnóstico visual nos resíduos, apresentando um erro de previsão superior (RMSE de `318.614,5`).

---

## 🏆 Principais Conclusões
* **Direcionadores de Valor:** A qualidade construtiva (`grade`), a área construída (`sqft_living`), a proximidade da água (`waterfront`) e a latitude (localização norte/sul em Seattle) são os componentes de maior peso na precificação imobiliária.
* **Modelo Recomendado:** O **Modelo Logarítmico** provou ser a melhor escolha para propósitos de *valuation* imobiliário e inferência preditiva robusta, combinando maior aderência matemática às premissas de Gauss-Markov e menor margem de erro.

