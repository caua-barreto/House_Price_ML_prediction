# 🏡 House Price Prediction - Machine Learning

![Kaggle](https://img.shields.io/badge/Kaggle-Competition-blue?style=for-the-badge&logo=kaggle)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Random%20Forest-green?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python)

## 📌 Sobre o Projeto
Este repositório contém uma proposta desenvolvida para a competição do Kaggle: **[House Prices - Advanced Regression Techniques](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques)**. 

O objetivo principal é prever o preço de venda de imóveis residenciais em Ames, Iowa, utilizando técnicas avançadas de regressão, Ciência de Dados e Machine Learning. O algoritmo final escolhido e otimizado para este projeto foi o **Random Forest Regressor**.

Esse projeto tem contexto com meu aprendizado de Machine Leaning, sendo um dos meus primeiros projetos que integram Análise de Dados, Estatística Descritiva e Machine Learning aplicada.

## 📁 Estrutura do Repositório
O projeto está organizado da seguinte forma:

- 📂 **`arquivos`**: Pasta contendo os arquivos originais fornecidos pela competição (ex: `train.csv`, `test.csv`, `data_description.txt`).
- 📂 **`csv_gerados`**: Pasta com os arquivos CSV gerados durante o processo de limpeza, feature engineering e as predições finais.
- 📄 **3 Arquivos Principais (Notebooks)**: Os arquivos centrais que detalham a jornada de ponta a ponta da nossa análise (Análise Exploratória, Pré-processamento/Limpeza e Treinamento do Modelo).

## 🧠 Metodologia Aplicada
O fluxo de trabalho foi dividido nas seguintes etapas estratégicas:

1. **Análise Exploratória de Dados (EDA):** Entendimento profundo das variáveis, identificação das melhores métricas de correlação com o preço e mapeamento do comportamento dos dados.
2. **Pré-Processamento & Limpeza (Etapa 3.1):**
   - Remoção de Outliers extremos (imóveis gigantescos e baratos).
   - Remoção de colunas irrelevantes (baixa variância ou alta multicolinearidade).
3. **Feature Engineering:**
   - Transformação de datas em idades reais (Idade do Imóvel, Idade da Reforma, com base no ano de venda).
   - Agrupamento de variáveis fragmentadas e esparsas (Criação de `TotalArea`, `TotalBaths`, `TotalPorch`).
4. **Tratamento de Dados (Etapas 3.2 e 3.3):**
   - Label Encoding para variáveis ordinais.
   - Tratamento de nulos (imputação pela mediana ou categorias neutras) e One-Hot Encoding para variáveis nominais.
5. **Modelagem de Machine Learning:**
   - Treinamento do modelo Base de Random Forest.
   - Otimização de Hiperparâmetros para alcançar a melhor precisão e estancar falhas em previsões atípicas.

## 🏆 Resultados Finais (Modelo Otimizado)
Após o ajuste de hiperparâmetros, o modelo obteve um ganho expressivo de performance, consolidando-se como uma ferramenta robusta:

- **R² (Poder de Explicação):** `0.9105` (91,05%)
- **MAE (Erro Médio Absoluto):** `US$ 15.685,95`
- **RMSE (Raiz do Erro Quadrático Médio):** `US$ 22.237,59`
- **MAPE (Erro Percentual Médio):** `10.15%`

O modelo consegue explicar **mais de 91%** da variação dos preços. Além disso, a otimização reduziu o erro nas casas atípicas (RMSE) em quase 2.500 dólares e diminuiu o erro médio em mais de 1.100 dólares por imóvel!

## 🚀 Como Executar Localmente
1. Clone este repositório: 
   ```bash
   git clone https://github.com/caua-barreto/House_Price_ML_prediction.git
   ```
2. Certifique-se de ter as bibliotecas necessárias instaladas, como `pandas`, `numpy`, `scikit-learn`, `matplotlib` e `seaborn`.
3. Navegue pelos 3 arquivos principais na ordem lógica (Exploração -> Limpeza/Feature Engineering -> Modelagem) para replicar os resultados.

---
*Desenvolvido por [Cauã Barreto](https://github.com/caua-barreto)*
