# MVP_P1
MVP - Ciência de Dados: Classificação de Métodos de Vazamento de Dados em Incidentes Públicos Usando Machine Learning Clássico

**Docente**: Natália Andrade Marques
**Data**: 27/10/2025

# Classificação de Métodos de Vazamento de Dados em Incidentes Públicos Usando Machine Learning Clássico

Este repositório contém uma solução completa para a MVP, utilizando técnicas supervisionadas clássicas para prever o **método de vazamento de dados** emincidentes públicos (Data Breaches).

O objetivo do modelo é apoiar atividades de **Cyber Threat Intelligence (CTI)** e **Resposta a Incidentes (SOC/CSIRT)**, realizando a classificação automática da causa do vazamento com base em texto descritivo e metadados disponíveis publicamente.

---

## Descrição do Problema

Os incidentes de vazamento de dados possuem causas variadas como:

- Ataques cibernéticos (*Hacked*)
- Perda ou roubo de dispositivos físicos (*Lost/Stolen*)
- Erros humanos (*Human Error*)
- Outras causas não categorizadas (*Other*)

Este projeto utiliza Machine Learning para **classificar automaticamente** cada incidente nessas categorias a partir do texto e atributos do dataset.

---

## Base de Dados

Dataset utilizado:

> **Biggest Data Breaches** – Data Breaches.csv  
> Fonte: GitHub (open dataset)
> CSV_URL = "https://raw.githubusercontent.com/ali-ce/datasets/master/Biggest-Data-Breaches/Data%20Breaches.csv"

Principais colunas:
- `Description`: texto descrevendo o incidente (feature principal)
- `Entity`: organização afetada
- `Year`: ano do incidente
- `OrgType`: tipo de instituição
- `Sensitivity`: tipo de dados comprometidos
- `Method`: variável-alvo (classe a ser prevista)

---

## Abordagem

Técnicas utilizadas:

> Limpeza e normalização de texto  
> Remoção de stopwords e lematização  
> TF-IDF com n-grams (1,2,3)
> Balanceamento de classes com **SMOTE + oversampling**
> **Data augmentation textual** para enriquecer classes minoritárias
> Teste de diferentes classificadores:

| Modelo | Status |
|--------|--------|
| Regressão Logística | ok |
| Random Forest | ok |
| **LinearSVC (SVM Linear)** |  Modelo final |
| Ensemble Voting | Avaliação complementar |

## Validação:
- Train/Test Split (80/20)
- 5-Fold Cross-Validation
- **GridSearchCV** para otimizar hiperparâmetros

---

## Resultados

Modelo escolhido: **LinearSVC (GridSearchCV)**

| Métrica | Resultado |
|--------|----------|
| **Acurácia** | **0.73** |
| **F1-macro** | **0.73** |
| Weighted F1 | 0.71 |

A matriz de confusão mostra melhor desempenho em **Hacked** e **Lost/Stolen**, refletindo padrões léxicos mais consistentes nessas categorias.

---


> *Todo o pipeline está completamente documentado no notebook, incluindo a análise, modelos, validação e relatório técnico final.*

---

## Tecnologias Utilizadas

- **Python 3**
- **scikit-learn**
- **imbalanced-learn**
- **NLTK**
- **NumPy / Pandas / Matplotlib**

---

## Possíveis Melhorias

- Inserção de novas fontes de dados governamentais
- Modelagem semântica contextual (BERT ou embeddings)
- Ajuste fino para classe *Human Error*
- Deploy com monitoramento contínuo (drift detection)

---

