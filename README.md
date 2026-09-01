# NLSY79 Intelligence and Income Prediction

## Overview

This project examines the relationship between cognitive ability, education, demographic characteristics, and later-life income using data from the **National Longitudinal Survey of Youth 1979 (NLSY79)**.

The analysis combines statistical modeling and machine learning to address three main questions:

1. Are ASVAB-derived measures of cognitive ability associated with future income?
2. Is there evidence of a gender income gap after controlling for measured ability and education?
3. Which predictive modeling approach performs best for forecasting later-life income?

The project was completed for **QTM 347 at Emory University: Machine Learning**.

---

## Data

The dataset includes individuals from the NLSY79 with:

- Demographic characteristics
- Family background information
- Years of education
- Ten ASVAB subtest scores
- Annual wage and salary income measured in 2005

The ASVAB measures were collected earlier in life and used to examine whether cognitive and technical abilities were associated with future economic outcomes. 

The processed dataset used in the analysis is available in the [`data/`](data/) folder.

---

## Methods

The analysis combines dimensionality reduction, regression, and tree-based machine learning methods.

### Principal Component Analysis

The ten ASVAB subtests were standardized and summarized using PCA.

- **ASVAB_PC1** captured broad overall test performance and explained approximately **61% of total ASVAB variance**.
- **ASVAB_PC2** captured differences between numerical/coding/verbal skills and more technical or mechanical skills. 

### Linear Regression

An OLS regression model predicted log-transformed income using:

- ASVAB_PC1
- ASVAB_PC2
- Gender
- Years of education

Both principal components, gender, and education were statistically significant predictors in the fitted model. The overall model had an **R² of approximately 0.217**. 

### Predictive Modeling

Several tree-based models were compared:

- Unpruned decision tree
- Pruned decision tree
- Two-tree bootstrap ensemble
- Random forest
- Four-model ensemble

The random forest was tuned using out-of-bag error and test performance.

---

## Key Findings

### 1. Cognitive ability was associated with later income

The first ASVAB principal component represented broad cognitive performance, while the second captured skill specialization.

Both components were positively associated with log income after controlling for gender and education.

---

### 2. Education was positively associated with income

Years of education showed a statistically significant positive relationship with later-life income in the regression model. 

---

### 3. A substantial gender-income association remained after controlling for ability and education

Gender was one of the strongest predictors in the regression model.

The model identified a large difference in income between male and female respondents even after controlling for ASVAB performance and education. Because the dataset is observational, this result should be interpreted as an association within the sample rather than a causal estimate.

---

### 4. Ensemble modeling produced the best test performance

The five predictive approaches achieved the following test MSE values:

| Model | Test MSE |
|---|---:|
| Unpruned Decision Tree | 0.6336 |
| Pruned Decision Tree | 0.6271 |
| Two-Tree Bagging | 0.6354 |
| Random Forest | 0.6326 |
| Four-Model Ensemble | **0.6093** |

The final ensemble achieved the lowest test error among the models evaluated. 

---

## Repository Structure

```text
nlsy79-income-prediction/
│
├── README.md
│
├── requirements.txt
│
├── data/
│   ├── README.md
│   └── IQ.Full.csv
│
├── notebooks/
│   └── nlsy79_income_prediction.ipynb
│
├── figures/
│   ├── README.md
│   ├── eda_distributions.png
│   ├── asvab_pca_loadings.png
│   ├── pruned_decision_tree.png
│   ├── random_forest_n_estimators.png
│   ├── random_forest_max_features.png
│   └── model_comparison.png
│
└── report/
    └── nlsy79_income_prediction_report.pdf
```

---

## Limitations

The NLSY79 data are observational, so the relationships identified in this project should be interpreted as **associations rather than causal effects**.

Income is influenced by many factors that are not included in the available dataset, including occupation, industry, labor-market conditions, career choices, social networks, and other personal circumstances.

The final ensemble also performed worse on the independent validation set than on the test set, demonstrating the uncertainty involved in predicting future income from a limited set of demographic and cognitive variables.

---

## Full Report

The full project report including methodology, results, model comparisons, appendices, and additional interpretation, is available in the [report](report/) folder.
