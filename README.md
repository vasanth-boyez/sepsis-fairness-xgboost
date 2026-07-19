# 🩺 Evaluating Bias in Early Sepsis Prediction with XGBoost

A healthcare AI project focused on **early sepsis prediction**, **fairness evaluation**, and **model interpretability** using ICU patient data.

---

## 📌 Overview

Sepsis is a life-threatening medical condition where delayed detection can lead to severe complications or death. In a clinical setting, it is not enough for a machine learning model to perform well overall if it behaves differently across patient groups.

This project builds and evaluates a **tuned XGBoost classifier** for early sepsis prediction using hourly ICU observations. Alongside predictive performance, the project examines **fairness across gender** using key subgroup fairness criteria and applies **LIME** to explain selected predictions.

---

## 🎯 Project Objectives

- Build a binary classification model for **early sepsis prediction**
- Compare a **baseline Random Forest** model with **XGBoost**
- Improve model performance through **hyperparameter tuning**
- Test an additional **SMOTE-based oversampling** experiment
- Evaluate fairness across gender using:
  - Equal Accuracy
  - Demographic Parity
  - Equal Opportunity
- Improve transparency with **LIME-based local explanations**

---

## ❓ Why This Project Matters

In healthcare, machine learning errors are not just technical issues. They can affect patient outcomes.

A model that misses genuine sepsis cases may delay clinical recognition and treatment. A model that performs differently across groups may also create **unequal clinical benefit**. This project was built to study all three dimensions together:

- **Performance**
- **Fairness**
- **Interpretability**

---

## 🗂 Dataset

This project uses the **Prediction of Sepsis** dataset from Kaggle, based on the **PhysioNet/Computing in Cardiology 2019 Challenge** dataset.

**Dataset link:**  
[Prediction of Sepsis - Kaggle](https://www.kaggle.com/datasets/salikhussaini49/prediction-of-sepsis)

> The raw dataset is **not included** in this repository because of GitHub file size limits.

---

## 🔄 Project Workflow

```text
Dataset Loading
    ↓
Exploratory Data Analysis
    ↓
Missingness Review & Feature Filtering
    ↓
Patient-Level Train/Test Split
    ↓
Baseline Random Forest
    ↓
XGBoost Baseline
    ↓
Hyperparameter Tuning
    ↓
Final Tuned XGBoost Evaluation
    ↓
Fairness Analysis Across Gender
    ↓
Additional XGBoost + SMOTE Experiment
    ↓
LIME-Based Local Explainability
```

---

## 🤖 Final Selected Model

### Tuned XGBoost Classifier

The final selected model was a **tuned XGBoost classifier**, chosen because it produced the strongest overall balance between:

- class 1 detection
- ranking performance
- fairness analysis suitability

### Final Test Performance

| Metric | Value |
|--------|------:|
| Accuracy | 0.8264 |
| Precision | 0.0615 |
| Recall | 0.5722 |
| F1-score | 0.1110 |
| ROC-AUC | 0.7763 |
| PR-AUC | 0.0926 |

### Final Fairness Gaps Across Gender

| Fairness Metric | Gap |
|----------------|----:|
| Equal Accuracy Gap | 0.00033 |
| Demographic Parity Gap | 0.00113 |
| Equal Opportunity Gap | 0.03345 |

### Key Fairness Insight

The final model was broadly balanced under **equal accuracy** and **demographic parity**, but a modest gap remained under **equal opportunity**, meaning one gender group was slightly less likely to have true sepsis cases correctly identified.

---

## 🧪 Additional Experiment: XGBoost + SMOTE

An additional experiment was carried out using **SMOTE** to oversample the minority sepsis class before training XGBoost.

Although the SMOTE-based version improved:
- accuracy
- precision
- F1-score

it reduced:
- recall
- ROC-AUC
- PR-AUC

Because this weakened true sepsis detection, the **tuned XGBoost model without SMOTE** remained the final selected model.

---

## 🔍 Interpretability with LIME

To improve transparency, **LIME** was used to inspect selected individual predictions from the final tuned XGBoost model.

Three representative cases were analysed:
- **True Positive**
- **False Negative**
- **False Positive**

Across these local explanations, features such as:

- `ICULOS`
- `Hour`
- `HR`
- `MAP`
- `HospAdmTime`

appeared repeatedly, suggesting that the model relied strongly on **time-related ICU context** and **cardiovascular instability** when forming predictions.

---

## 📁 Repository Structure

```text
sepsis-fairness-xgboost/
│
├── README.md
├── requirements.txt
│
├── notebooks/
│   ├── Early_Sepsis_Prediction.ipynb
│
├── reports/
└── 
```

---

## 🛠 Tech Stack

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Scikit-learn**
- **XGBoost**
- **imbalanced-learn**
- **LIME**
- **Jupyter Notebook**

---

## 🚀 How to Run

### 1. Clone the repository

```bash
git clone https://github.com/vasanth-boyez/sepsis-fairness-xgboost.git
cd sepsis-fairness-xgboost
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Download the dataset

Download the dataset from Kaggle:

[Prediction of Sepsis - Kaggle](https://www.kaggle.com/datasets/salikhussaini49/prediction-of-sepsis)

### 4. Place the dataset in the expected folder

```text
data/raw/Dataset.csv
```

### 5. Run the notebook

Open:

```text
notebooks/01_final_pipeline.ipynb
```

---

## 📎 Notes on Data Availability

The dataset is not uploaded to this repository because of GitHub size limits and distribution practicality. Please download it manually from Kaggle and place it in the `data/raw/` directory before running the notebooks.

---

## 📄 Report

The full academic report for this project is included in:

```text
reports/AI_Report_Vasanth.pdf
```

---

## 💡 Key Takeaway

This project shows that in healthcare AI, **performance alone is not enough**. A model can look strong overall while still creating unequal benefit across groups. For that reason, sepsis prediction was evaluated here through **performance**, **fairness**, and **interpretability** together.

---

## 👨‍💻 Author

**Vasanth Boyez**  
AI Ethics Project  
Teesside University
