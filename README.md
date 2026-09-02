# 🏡 House Price Prediction - Machine Learning Relatório FINAL

![Kaggle](https://img.shields.io/badge/Kaggle-Competition-blue?style=for-the-badge&logo=kaggle)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Ensemble%20%26%20Linear-green?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

---

## 📌 Sobre o Projeto

Este repositório apresenta o estudo e a solução para o desafio de Machine Learning do Kaggle: **[House Prices - Advanced Regression Techniques](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques)**.

O projeto está dividido em duas abordagens:

- **Versão 1 (Prediction_V1)** (Finalizada em 27/08/2026): Análise simples e direta utilizando Unicamente o algoritmo **Random Forest** [cite: 5].
- **Versão 2 (Prediction_V2)** (Finalizada em 02/09/2026: evolução significativa com reestruturação inteligente do código, tratamentos estatísticos aprofundados, divisão estratégica de datasets para diferentes famílias de algoritmos e avaliação de múltiplos modelos preditivos de alta performance.

O projeto foi totalmente desenvolvido em um ambiente virtual isolado (`.venv`) para garantir a reprodutibilidade das análises.

---

## 🔄 Diferenciais e Evolução (V1 vs V2)

A Versão 2 traz diversas inovações analíticas e metodológicas em relação à V1:

### 📊 Transformação Estatística do Target
Durante a Análise Exploratória (EDA), identificou-se que o KDE da  distribuição de preços (`SalePrice`) possuía forte assimetria a direita, e apresenta comportamento lognormal . Nesse sentido, aplicou-se a transformação logarítmica `log1p` nas features distorcidas e no *target* para aproximar os dados de uma distribuição normal teórica.

(KDE tradicional do SalesPrice)
<img width="981" height="584" alt="image" src="https://github.com/user-attachments/assets/de2f217d-1296-48b9-9178-32044aef7556" />

(KDE para log1p de SalesPrice)
<img width="984" height="584" alt="image" src="https://github.com/user-attachments/assets/6e37c277-1f94-4eda-acfd-2b6f8c3063df" />

### 🔀 Bifurcação do Dataset
Os dados foram estrategicamente separados em dois DataFrames distintos após o pré-processamento :

| Dataset | Características | Aplicação |
|---------|-----------------|-----------|
| **Dataset Linear** | Conjunto enxuto contendo apenas `SalePrice` transformado em log1p e as **10 features de maior importância** | Ideal para algoritmos lineares que sofrem com multicolinearidade |
| **Dataset em Árvore** | Conjunto completo com One-Hot Encoding (OHE) e Label Enconding aplicados, gerando **190 features totais** | Ideal para algoritmos não-lineares que lidam bem com alta dimensionalidade |

### 🛡️ Controle Rigoroso de Overfitting
Diferente da primeira versão, foi implementada **Cross-Validation**, **K-Fold** (K=5) aliada à otimização de hiperparâmetros (usando `RandomizedSearchCV`) focada em regularização. O antigo modelo Random Forest da V1 foi melhor otimizado na V2, controlando ativamente a "memorização" de dados e reduzindo o gap entre treino e validação.

### 🔍 Interpretabilidade com SHAP
A dificuldade de interpretar modelos não lineares foi superada com o uso da biblioteca *SHAP*, permitindo avaliar a **importância e o impacto de cada feature** e convertendo o impacto logarítmico diretamente para **dólares (US$)** de acordo com o preço mediano dos imóveis.

---

## 🧠 Modelagem e Algoritmos Avaliados

Para garantir a melhor precisão possível, foram desenvolvidos e comparados **9 algoritmos** diferentes:

- **Modelos Lineares:** Regressão Linear Tradicional, Ridge (L2), Lasso (L1) e ElasticNet.
- **Modelos Não Lineares (Árvores e Ensembles):** Decision Tree, Random Forest, Gradient Boosting, XGBoost e LightGBM.

---

## 📊 Resultados Comparativos

### Modelos Lineares (treinados com 10 features essenciais)

| Modelo | MAE Treino | MAE Validação | Gap (MAE) | RMSE Validação | R² Validação |
|--------|------------|---------------|-----------|----------------|--------------|
| Regressão Linear | $18.319,11 | $19.327,22 | $1.008,11 | $26.097,57 | 0.8767 |
| Ridge | $18.315,62 | $19.335,98 | $1.020,36 | $26.123,49 | 0.8765 |
| Lasso | $18.295,63 | $19.325,06 | $1.029,43 | $26.168,02 | 0.8760 |
| ElasticNet | $18.302,52 | $19.325,00 | $1.022,48 | $26.139,40 | 0.8763 |

<img width="984" height="784" alt="image" src="https://github.com/user-attachments/assets/948eae14-b331-4f96-9181-fdbb17e01bd3" />


### Modelos Não Lineares (otimizados, treinados com dataset completo OHE)

| Modelo | MAE Treino | MAE Validação | Gap (MAE) | RMSE Validação | R² Validação | Gap (R²) |
|--------|------------|---------------|-----------|----------------|--------------|----------|
| Decision Tree | $18.858,03 | $20.849,99 | $1.991,96 | $28.790,73 | 0.8499 | 3.25% |
| Random Forest | $10.340,09 | $15.812,01 | $5.471,91 | $21.971,15 | 0.9126 | 3.90% |
| Gradient Boosting | $9.590,53 | $13.645,93 | $4.055,40 | $18.621,69 | 0.9372 | 3.11% |
| **XGBoost** ⭐ | $10.841,88 | **$13.645,57** | $2.803,69 | $19.019,11 | **0.9345** | **1.80%** |
| LightGBM | $10.568,00 | $14.243,04 | $3.675,04 | $20.005,30 | 0.9275 | 1.74% |

<img width="1783" height="1022" alt="image" src="https://github.com/user-attachments/assets/28a9ed08-06a0-4819-80f8-729e5c5ec16b" />

---

## 🔬 Diagnósticos Visuais e Interpretabilidade

### 1. Análise de Dispersão e Resíduos
- Gráficos de **Previsto vs. Real** mostraram que as arquiteturas de Boosting (XGBoost e Gradient Boosting) apresentam agrupamentos extremamente coesos em torno da linha ideal de previsão.
- A distribuição dos resíduos assumiu um comportamento **leptocúrtico** (alta concentração de acertos na média zero), confirmando ausência de viés sistêmico.

<img width="1795" height="1022" alt="image" src="https://github.com/user-attachments/assets/dad92b0b-fe0f-4ef0-ac6c-e455f90fd537" />

- Para os modelos lineares, que são todos consistentes entre si, observamos uma análise de dispersão bem mais equilibrada e próxima da curva normal:

<img width="984" height="584" alt="image" src="https://github.com/user-attachments/assets/ef592f25-2918-4e53-bd1e-11900689f7bb" />

### 2. Dificuldade nas Caudas
- Todos os modelos apresentaram **subestimação leve** para imóveis de altíssimo padrão (acima de US$ 350.000).
- O **Q-Q Plot** confirmou que o erro residual comporta-se de forma normal no centro, com desvios característicos apenas nas pontas extremas (caudas pesadas).

-Para os modelos lineares:

<img width="984" height="684" alt="image" src="https://github.com/user-attachments/assets/ff0fe9f2-1662-47b6-b37b-c9210367988f" />

- Para os modelos não lineares:

<img width="1784" height="1022" alt="image" src="https://github.com/user-attachments/assets/96a6e766-02e1-4df8-8e24-1dad77e9c4b5" />

### 3. Impacto Financeiro (SHAP)
A aplicação do SHAP revelou o real impacto em dólares (US$) das features nos modelos otimizados:

| Feature | Impacto Financeiro (US$) |
|---------|--------------------------|
| **Luxury_Score** | + $24.000+ |
| **TotalArea** | + $17.200 |
| **OverallQual** | ~ $15.000 |
| **Idade da Reforma** | ~ $12.000 |

---

### 4. Curva de aprendizado 

Ao analisar modelos não lineares, o tamanho da base de dados pode interferir no modelo. Geralmente modelos mais avançados ( principalmente os de Boosting ) tendem a performar melhores resultados com bases maiores. Desse modo, segue os gráficos para cada um dos modelos de árvore analisados na base de dados desse case, que possui na faixa de 1500 linhas de dados.

<img width="1782" height="1022" alt="image" src="https://github.com/user-attachments/assets/0702b013-eab9-4268-bd18-57744b07c3c6" />

Veja que os modelos de boosting possui, comparativamente, grande consistência em comparação aos modelos de Bagging e tendência de redução do erro para grandes bases de dados.

## 🏆 O Veredito: Melhor Modelo

O **XGBoost Regressor** consolidou-se como o modelo mais maduro e confiável para este projeto, alcançando o melhor equilíbrio entre alta capacidade preditiva e robustez contra overfitting.

- Entregou um **MAE de US$ 13.645,57** em dados inéditos [cite: 3].
- Atingiu um **R² de 0.9345** (explicando 93,45% da variação dos preços) [cite: 3].
- Apresentou o **menor gap de variação** entre o desempenho de treino e validação (R² gap de 1,80%), garantindo estabilidade e prontidão para produção [cite: 3].

---

## 📁 Estrutura do Repositório

A organização final da pasta do projeto reflete uma esteira clara de processamento de dados e modelagem:
___________________________________________________________________________________________________________________________________________________________


 ## 🚀 Como Executar Localmente
Este projeto foi construído utilizando boas práticas de isolamento de ambiente. Para reproduzir os resultados perfeitamente, siga as instruções:

### (1) Clone este repositório:

``
git clone [https://github.com/caua-barreto/House_Price_ML_prediction.git](https://github.com/caua-barreto/House_Price_ML_prediction.git)
cd House_Price_ML_prediction/Prediction_V2
``

### (2) Crie um ambiente virtual .venv

### (3) Instale as dependências a partir do arquivo requirements.txt

#### (4) Execute os notebooks:


Com o ambiente ativado, abra o Jupyter Notebook ou o VS Code e execute os arquivos na ordem lógica da esteira:

1. Análise_Exploratoria.ipynb
2. Tratamento_Processamento.ipynb
3. Modelos_Lineares.ipynb
4. Modelos_nao_Lineares.ipynb


---
*Desenvolvido por [Cauã Barreto](https://github.com/caua-barreto)*
Desenvolvido por Cauã Barreto - Junior Data Scientist 

