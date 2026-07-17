# Evaluating Bias in Early Sepsis Prediction: A Fairness Analysis of a Tuned XGBoost Model

## Overview

This project investigates bias in early sepsis prediction using machine learning in a high-risk healthcare setting. The final selected model is a tuned XGBoost classifier trained on hourly ICU observations. Alongside predictive performance, the project evaluates fairness across gender using equal accuracy, demographic parity, and equal opportunity.

The work was developed as part of an AI Ethics assessment and focuses on an important question: a model may perform reasonably well overall, but does it behave fairly across different groups?

## Objectives

The main objectives of this project are to:

- build a binary classification model for early sepsis prediction
- compare a baseline Random Forest model with XGBoost
- improve the final model through hyperparameter tuning
- test an additional SMOTE-based experiment for class balancing
- evaluate fairness across gender groups
- use LIME to explain selected individual predictions

## Dataset

This project uses the **Prediction of Sepsis** dataset from Kaggle, based on the PhysioNet/Computing in Cardiology 2019 Challenge dataset.

**Dataset link:**  
`https://www.kaggle.com/datasets/salikhussaini49/prediction-of-sepsis`

> The raw dataset is not included in this repository because of file size limits.

## Why Sepsis?

Sepsis was chosen because it is a high-risk healthcare problem where delayed recognition can lead to severe complications or death. That makes it a meaningful setting for an AI ethics project. In this context, fairness matters because a model that misses genuine sepsis cases more often in one group than another may contribute to unequal clinical benefit.

## Project Workflow

The project follows this workflow:

1. load and inspect the dataset  
2. perform exploratory data analysis  
3. examine class imbalance and missingness  
4. filter highly sparse features  
5. split data by `Patient_ID` to avoid leakage  
6. build a baseline Random Forest model  
7. switch to XGBoost and tune the final model  
8. evaluate predictive performance  
9. evaluate fairness across gender groups  
10. test an additional XGBoost + SMOTE experiment  
11. apply LIME for local explainability  

## Final Selected Model

The final selected model is a **tuned XGBoost classifier**.

### Final performance on the test set

- **Accuracy:** 0.8264
- **Precision:** 0.0615
- **Recall:** 0.5722
- **F1-score:** 0.1110
- **ROC-AUC:** 0.7763
- **PR-AUC:** 0.0926

### Fairness gaps across gender

- **Equal Accuracy Gap:** 0.00033
- **Demographic Parity Gap:** 0.00113
- **Equal Opportunity Gap:** 0.03345

## Additional Experiment: XGBoost + SMOTE

An additional experiment was carried out using SMOTE to oversample the minority sepsis class before training XGBoost.

Although this version improved accuracy, precision, and F1-score, it reduced recall, ROC-AUC, and PR-AUC when compared with the final tuned XGBoost model. It also produced a mixed fairness outcome.

Because of this, the **tuned XGBoost model without SMOTE** was retained as the final model for the project.

## Fairness Evaluation

Fairness was evaluated across **Gender** using three criteria:

- **Equal Accuracy**
- **Demographic Parity**
- **Equal Opportunity**

The results showed that the final model was broadly balanced under equal accuracy and demographic parity, but a modest gap remained under equal opportunity. This means that one gender group was slightly less likely to have true sepsis cases correctly identified.

## Interpretability

To improve transparency, **LIME** was used to explain selected individual predictions from the final tuned XGBoost model. Local explanations were generated for:

- a true positive case
- a false negative case
- a false positive case

These explanations showed that features such as `ICULOS`, `Hour`, `HR`, `MAP`, and `HospAdmTime` played an important role in the model’s local decision-making.

## Repository Structure

```text
sepsis-fairness-xgboost/
│
├── README.md
├── .gitignore
├── requirements.txt
├── notebooks/
│   ├── Early_Sepsis_Prediction.ipynb
│
├── reports/
│   └── ....
└── 
