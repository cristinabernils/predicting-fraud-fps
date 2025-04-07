# 🕵️‍♀️ Fraud Detection in Financial Services – PaySim Dataset

This project applies **Data Science techniques** to detect fraudulent financial transactions using the synthetic **PaySim** dataset, which simulates a real mobile payment system.

---

## 📁 Project Structure

This repository contains a complete fraud detection pipeline, divided into the following stages:

---

## 1. 🔍 Exploratory Data Analysis (EDA)

In this phase, we explore the structure and distribution of the data:

- Review of available columns and variable types.
- Distribution of the target variable (`isFraud`) with class imbalance visualization.
- Study of numeric variables (`amount`, `oldbalanceOrg`, etc.) and categorical ones (`type`).
- Temporal pattern analysis (`step`) and amount distribution by class.

---

## 2. 🧱 Data Preparation & Feature Engineering

After exploration, we prepare the dataset and create features that reflect behavioral fraud patterns:

### 🔍 Transaction Filtering

Fraud only occurs in the following transaction types:
- `TRANSFER`
- `CASH_OUT`

Other types (`PAYMENT`, `DEBIT`, `CASH_IN`) are filtered out to reduce noise and focus on high-risk patterns.

### 🛠️ Feature Engineering Highlights

- **Balance errors**  
  `errorBalanceOrig`, `errorBalanceDest` → Detect inconsistencies in transaction math.
  
- **Binary balance flags**  
  e.g., `orig_balance_zero_before`, `is_orig_emptied` → Indicators of suspicious states.

- **Amount-to-balance ratio**  
  e.g., `amount_to_balance_ratio` → Spot transactions disproportionately large.

- **Outlier detection**  
  Using `z-score` to flag anomalous transfers.

These variables aim to simulate the behavior fraudsters attempt to hide — such as draining an account or sending money without sufficient balance.

---

## 3. ⚖️ Class Balancing with SMOTETomek

Given the extreme imbalance (fraud < 1%):

- The **SMOTETomek** technique is used to generate synthetic fraud samples and clean ambiguous examples.
- It is applied **after the train/test split** to avoid data leakage.

---

## 4. 🤖 Model Training

We train multiple models to compare approaches:

- **Logistic Regression** (baseline)
- **Random Forest** (ensemble, `class_weight='balanced'`)
- **XGBoost** (with `scale_pos_weight`)

Each model is trained using the engineered features and evaluated on real-world class imbalance scenarios.

---

## 5. 📊 Results Analysis

### 🧪 Model Evaluation

- **Confusion Matrix**
- **Classification Report** (`Precision`, `Recall`, `F1`)
- **ROC AUC Score**

### 📈 ROC Curve

The ROC curve is plotted to analyze the trade-off between **TPR (True Positive Rate)** and **FPR (False Positive Rate)**.

### 📌 Feature Importance

The most important features are visualized, including:

- `amount_to_balance_ratio`
- `errorBalanceOrig`
- `is_orig_emptied`, etc.

These insights help interpret how the model detects fraud based on behavioral signals.

---

## 💼 Dataset

**Synthetic Financial Datasets For Fraud Detection (PaySim)**  
📎 Source: [Kaggle](https://www.kaggle.com/datasets/ealaxi/paysim1)

---

## 🧠 Next Steps (optional)

- Implement fraud detection using **XGBoost + SHAP**
- Deploy the pipeline with **Streamlit** or **FastAPI**
- Real-time data monitoring and model serving