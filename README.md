# 🎓 MVP - Sprint Machine Learning & Analytics | PUC-Rio

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/release/python-380/)
[![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=flat&logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=flat&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-%23150458.svg?style=flat&logo=xgboost&logoColor=white)](https://xgboost.readthedocs.io/)

Repositório destinado ao projeto final (MVP) da Sprint de **Machine Learning & Analytics** da Pós-Graduação em Ciência de Dados e Analytics da **PUC-Rio**.

👤 **Autor:** Anderson Gonçalves Portella ([@andersonportella-collab](https://github.com/andersonportella-collab))

---

## 📑 Índice
1. [Sobre o Projeto](#-sobre-o-projeto)
2. [Objetivos](#-objetivos)
3. [Conjunto de Dados (Dataset)](#-conjunto-de-dados-dataset)
4. [Metodologia e Modelagem](#-metodologia-e-modelagem)
5. [Tecnologias Utilizadas](#-tecnologias-utilizadas)
6. [Estrutura do Repositório](#-estrutura-do-repositório)
7. [Como Executar o Projeto](#-como-executar-o-projeto)

---

## 🔍 Sobre o Projeto
O contexto deste projeto envolve a operação e o monitoramento de poços de petróleo offshore no Campo de Volve (operado pela Equinor no Mar do Norte). A antecipação precisa da vazão é fundamental para a eficiência operacional e a segurança logística no transporte de fluidos, mitigando perdas financeiras por paradas não programadas e contribuindo para a excelência na gestão da matriz energética.

O desafio é utilizar dados históricos de instrumentação (telemetria) para prever a produção diária de óleo, substituindo heurísticas puramente analíticas por modelos baseados em Machine Learning para extrair maior valor e entender o comportamento complexo e não-linear do escoamento.

---

## 🎯 Objetivos
* **Objetivo Principal:** Desenvolver um modelo preditivo de **Regressão supervisionada** capaz de prever o volume diário de óleo produzido em poços offshore a partir de medições de sensores de pressão e temperatura.
* **Avaliação:** Comparar uma abordagem baseline (como Regressão Linear simples ou Ridge) com modelos candidatos não-lineares mais complexos (como Random Forest e XGBoost).
* **Critérios de Sucesso:** Superar o modelo baseline em pelo menos 15% na métrica RMSE e atingir um $R^2$ superior a 0.75 no conjunto de teste, garantindo também a extração e interpretabilidade da Importância das Variáveis (*Feature Importance*) para os engenheiros de produção.

---

## 📊 Conjunto de Dados (Dataset)
* **Fonte:** O dataset original foi disponibilizado publicamente pela petroleira Equinor (Campo de Volve). Para garantir reprodutibilidade, o arquivo foi hospedado publicamente neste repositório.
* **Arquivo:** `Volve_production_data.xlsx` (Aba: *Daily Production Data*)
* **Dimensões:** 15.634 registros diários e 24 atributos (colunas).
* **Variável-Alvo (Target):** `BORE_OIL_VOL` (Volume Diário de Óleo Produzido).
* **Principais Variáveis Preditoras:**
  * `ON_STREAM_HRS`: Horas ativas de operação do poço no dia.
  * `AVG_DOWNHOLE_PRESSURE`: Pressão média medida no fundo do poço.
  * `AVG_DOWNHOLE_TEMPERATURE`: Temperatura média no fundo do poço.
  * `AVG_DP_TUBING`: Diferencial de pressão na tubulação.
  * `AVG_CHOKE_SIZE_P`: Percentual de abertura da válvula (choke).
  * `AVG_WHP_P`: Pressão na cabeça do poço (*Wellhead Pressure*).
* **Restrições Tratadas:** Presença massiva de valores ausentes (NaNs) devido a falhas pontuais de telemetria ou períodos de inatividade prolongados, exigindo um tratamento criterioso.

---

## 🛠 Metodologia e Modelagem
O projeto segue as melhores práticas para o ciclo de vida de ciência de dados:
1. **Carga e Limpeza:** Carregamento dos dados via URL pública no GitHub via Pandas/openpyxl. Remoção de colunas puramente descritivas (identificadores) e atributos que causariam vazamento de dados / *data leakage* (ex: produção de gás e água diários).
2. **Análise Exploratória (EDA):** Análise de distribuições, verificação de anomalias operacionais, estatísticas descritivas e análise de correlações termodinâmicas.
3. **Pré-Processamento:** Tratamento inteligente de valores nulos (ex: `ON_STREAM_HRS = 0` resultando em vazão nula), e separação dos conjuntos em treino e teste definindo uma semente fixa (`SEED = 42`).
4. **Modelagem:** 
   * *Baseline:* Regressão Linear, Ridge e Lasso.
   * *Avançados:* Modelos de *Ensemble* baseados em árvores, incluindo Random Forest, Gradient Boosting e **XGBoost**.
5. **Avaliação e Resultados:** Funções auxiliares modulares foram construídas para extração rápida das métricas **RMSE**, **MAE** e **R²** em todos os modelos criados.

---

## 💻 Tecnologias Utilizadas
* **Linguagem:** Python
* **Ambientes de Desenvolvimento:** Google Colab / Jupyter Notebook
* **Bibliotecas de Manipulação e Visualização:** `pandas`, `numpy`, `matplotlib`, `seaborn`
* **Machine Learning & Otimização:** `scikit-learn` (Pipelines, KFold, GridSearchCV), `xgboost`

---

## 📂 Estrutura do Repositório

```text
MVP_ML_PUCRio/
├── Documentação MVP - Machine Learning & Analytics (Volve Dataset).pdf  # Definição e escopo do problema
├── MVP_ML_Analytics_2026_Anderson_G_Portella.ipynb  # Notebook principal e executável
├── Volve_production_data.xlsx                       # Base de dados oficial extraída da Equinor
└── README.md                                        # Documentação deste repositório
