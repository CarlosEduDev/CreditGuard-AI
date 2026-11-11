# 💳 CreditGuard-AI: Detecção de Fraudes em Cartões de Crédito

![Python](https://img.shields.io/badge/Python-3.13-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-157C68?style=for-the-badge)

Este projeto aborda o problema clássico de **Detecção de Fraudes em Transações Financeiras** utilizando aprendizado de máquina. O principal desafio técnico enfrentado é o **extremo desbalanceamento das classes**, visto que transações fraudulentas representam apenas **~0,17%** do total de dados.

---

## 📌 Visão Geral do Projeto

O objetivo é construir e comparar modelos preditivos capazes de identificar transações fraudulentas com alta precisão e recall, minimizando tanto falsos negativos (fraudes não detectadas) quanto falsos positivos (alarmes falsos para transações legítimas).

### 📄 Sobre o Dataset
* **Fonte:** [Credit Card Fraud Detection Dataset](https://storage.googleapis.com/download_tensorflow_org/data/creditcard.csv)
* **Total de Transações:** ~284.807 transações
* **Distribuição de Classes:**
  * **Classe 0 (Legítima):** 99,83%
  * **Classe 1 (Fraude):** 0,17%
* **Features:** 30 variáveis de entrada (`Time`, `Amount` e variáveis transformadas via PCA de `V1` a `V28`).

---

## 🛠️ Tecnologias e Bibliotecas Utilizadas

* **Linguagem:** Python 3.13
* **Manipulação de Dados:** `pandas`, `numpy`
* **Visualização:** `matplotlib`
* **Pré-processamento e Modelagem:** `scikit-learn`
* **Tratamento de Desbalanceamento:** `imbalanced-learn` (`SMOTE`, Undersampling)
* **Modelos Avançados:** XGBoost (`XGBClassifier`), Random Forest
* **Explicabilidade do Modelo:** SHAP (SHapley Additive exPlanations)

---

## 🚀 Etapas do Projeto

1. **📊 Análise Exploratória e Pré-processamento:**
   * Verificação de valores nulos e distribuição das classes.
   * Padronização e escala logarítmica da variável `Amount` (`StandardScaler`, `log1p`).
   * Divisão estratificada dos dados em treino e teste (70/30).

2. **⚖️ Tratamento de Desbalanceamento:**
   * Aplicação de **Random Undersampling** para balanceamento rápido.
   * Aplicação da técnica de sobreamostragem sintética **SMOTE** (Synthetic Minority Over-sampling Technique).
   * Ajuste do parâmetro `class_weight='balanced'` e `scale_pos_weight`.

3. **🤖 Treinamento e Avaliação de Modelos:**
   * **Regressão Logística:** Baseline com ajuste de threshold de decisão.
   * **Random Forest:** Modelo ensemble balanceado.
   * **XGBoost:** Gradient Boosting otimizado com busca de hiperparâmetros via `GridSearchCV`.

4. **🔍 Interpretabilidade com SHAP:**
   * Análise do impacto das variáveis nas previsões do modelo XGBoost utilizando valores SHAP.

---

## 📈 Resultados Alcançados

| Modelo | Precision (Classe 1) | Recall (Classe 1) | F1-Score (Classe 1) |
| :--- | :---: | :---: | :---: |
| **Regressão Logística (Baseline)** | 0.86 | 0.65 | 0.74 |
| **Random Forest (Weighted)** | 0.83 | 0.76 | 0.80 |
| **XGBoost (scale_pos_weight)** | **0.94** | **0.78** | **0.85** |

> 🏆 **Destaque:** O modelo **XGBoost** obteve o melhor desempenho geral (F1-score de **0.85** para a classe de fraudes), garantindo alta precisão (94%) sem comprometer a taxa de detecção (Recall de 78%).

---

## 🧠 Interpretabilidade do Modelo (SHAP)

Utilizando a biblioteca **SHAP**, foi possível identificar quais atributos mais influenciaram o modelo na tomada de decisão para classificar uma transação como fraudulenta:

* As variáveis transformadas por PCA (como `V14`, `V4`, `V10`, `V12`) apresentaram maior impacto na pontuação do modelo.

---

## 💻 Como Executar o Projeto

1. **Clone este repositório:**
   ```bash
   git clone [https://github.com/SEU-USUARIO/NOME-DO-REPOSITORIO.git](https://github.com/SEU-USUARIO/NOME-DO-REPOSITORIO.git)
   cd NOME-DO-REPOSITORIO
