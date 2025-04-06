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

## 2. ✂️ Filtering Relevant Transactions

From the analysis, we observe that fraud only occurs in the following transaction types:

- `TRANSFER`
- `CASH_OUT`

Thus, the other types (`PAYMENT`, `DEBIT`, `CASH_IN`) are filtered out to reduce noise and improve model precision.

---

## 3. 🛠️ Feature Engineering

Additional features are created to enhance the model’s learning capacity:

- **Balance errors**: `errorBalanceOrig`, `errorBalanceDest`  
  → Detect accounting inconsistencies.

- **Binary balance flags**:  
  → e.g., `orig_balance_zero_before`, `is_orig_emptied`.

- **Amount-to-balance ratio**:  
  → `amount_to_balance_ratio`

- **Outlier detection** using `z-score` on transaction amount.

These features help capture hidden patterns that fraudsters may try to mask.

---

## 4. ⚖️ Class Balancing with SMOTETomek

Given the extreme imbalance (fraud < 1%):

- The **SMOTETomek** technique is used to generate synthetic fraud samples and clean ambiguous examples.
- It is applied **after the train/test split** to avoid data leakage.

---

## 5. 🤖 Model Training (Random Forest)

A **RandomForestClassifier** is trained using:

- Balanced class weights (`class_weight='balanced'`)
- Balanced dataset via SMOTETomek
- Evaluation metrics: Precision, Recall, F1-Score, ROC AUC

---

## 6. 📊 Results Analysis

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

These insights help interpret how the model detects fraud.

---

## 💼 Dataset

**Synthetic Financial Datasets For Fraud Detection (PaySim)**  
📎 Source: [Kaggle](https://www.kaggle.com/datasets/ealaxi/paysim1)

---

## 🧠 Next Steps (optional)

- Implement fraud detection using **XGBoost + SHAP**
- Deploy the pipeline with **Streamlit** or **FastAPI**
- Real-time data monitoring and model serving

---

## 🚀 Project Execution

```bash
# Clone the repository
git clone https://github.com/your_user/your_repo.git
cd your_repo

# Install dependencies
pip install -r requirements.txt

# Run the notebook
jupyter notebook