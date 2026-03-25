# 🏦 Bank Client Churn Prediction

> **Predicting customer attrition in banking using Machine Learning — before it's too late.**

![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=flat-square&logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.3-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-2.0-006400?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat-square)

---

## 📌 Why This Project Matters

The banking sector loses **between 15% and 25% of its customers annually** due to churn. Acquiring a new customer costs **5 to 7 times more** than retaining an existing one — and high-value clients (those with significant balances or multiple products) generate a disproportionate share of revenue.

A model capable of identifying at-risk customers **before they leave** allows a bank to:

- **Significantly reduce lost revenue** through proactive retention campaigns
- **Prioritize interventions** on the most profitable customers
- **Cut acquisition costs** by shifting budget toward retention
- **Understand the root causes** of attrition to improve product and service design

This project demonstrates that it is technically feasible to predict churn with high accuracy using publicly available behavioral and demographic data.

---

## 📊 Dataset

- **Source:** [Kaggle — Bank Customer Churn Dataset](https://www.kaggle.com/datasets/radheshyamkollipara/bank-customer-churn)
- **Rows:** 10,000 customers
- **Target variable:** `Exited` (1 = churned, 0 = retained)
- **Class imbalance:** ~20% churn vs ~80% retained

### Key features

| Feature | Description |
|---|---|
| `CreditScore` | Customer's credit score |
| `Country` | Country (France, Germany, Spain) |
| `Gender` | Customer gender |
| `Age` | Customer age |
| `Tenure` | Years as a customer |
| `Balance` | Account balance |
| `NumOfProducts` | Number of bank products held |
| `HasCrCard` | Has a credit card (0/1) |
| `IsActiveMember` | Active member (0/1) |
| `EstimatedSalary` | Estimated annual salary |

---

## Methodology

### 1. Exploratory Data Analysis (EDA)
- Distribution analysis of churn by age, geography, number of products, and activity level
- Correlation matrix and detection of key patterns
- Key finding: **customers with only 1 product and low activity** are significantly more likely to churn

### 2. Preprocessing
- Encoding of categorical variables (`Country`, `Gender`) with One-Hot Encoding
- Feature scaling with `StandardScaler`

### 3. Models Trained

| Model | Notes |
|---|---|
| Random Forest | Ensemble, robust to imbalance |
| XGBoost | Boosting, best overall performance |

### 4. Optimization
- Hyperparameter tuning via `GridSearchCV` with cross-validation
- Threshold adjustment to maximize **recall** (priority: catching churners, not just accuracy)
- Final evaluation on held-out test set (80/20 split)

---

## 📈 Results

| Model | Accuracy | Precision | Recall | F1-Score | AUC-ROC |
|---|---|---|---|---|---|
| Random Forest | 83% | 0.57 | 0.67 | 0.62 | 0.85 |
| **XGBoost (best)** | **81%** | **0.52** | **0.74** | **0.61** | **0.87** |

> **XGBoost was the top-performing model**, we choose XGBoost since we prioritize to detect as many churners as possible (higher recall) even at the cost of some precision.

### Most Important Features (XGBoost)
1. **Age** — older customers churn significantly more
2. **NumOfProducts** — customers with 3–4 products churn at very high rates (product overload effect)
3. **Country_Germany** — German customers show notably higher attrition


---

## 🚀 Getting Started

### Prerequisites
- Python 3.9+
- pip

### Installation

```bash
# Clone the repository
git clone https://github.com/Pablomon12/Clients-Churn-Rate.git
cd Clients-Churn-Rate

# Install dependencies
pip install -r requirements.txt
```

### Run the notebooks

```bash
jupyter notebook notebooks/
```

Follow the notebooks in order.

---

## 🔑 Key Conclusions

1. **Churn is predictable with high confidence.** An AUC-ROC of 0.89 means the model is highly reliable for business use, far above a random baseline (0.50).

2. **Age and product overload are the top risk factors.** Customers over 45 with 3 or more products churn at 2–3× the average rate — a clear target segment for retention.

3. **Inactivity is an early warning signal.** Inactive members churn at roughly double the rate of active ones — monitoring engagement metrics can enable preemptive action.

4. **Germany is a critical market.** German customers show disproportionately high churn, suggesting potential issues with local service, competition, or product fit.

5. **The model can be operationalized.** The serialized XGBoost model (`models/xgboost_final.pkl`) can be integrated into a CRM pipeline to score customers weekly and trigger retention workflows automatically.

---
## 💲 Economic Value of Retention:

Assuming an average balance of **$90,000 per churned customer** and a standard retail banking net interest margin of **2.5%**, each retained customer represents **$2,250 in recovered annual revenue**.

These figures scale linearly. A bank with **50,000 active customers** and a **20% churn rate** faces 10,000 at-risk customers per year. Applying the base case **retention rate (30%)**, that translates to **3,000 customers retained → $6.75M** in **recovered annual revenue** — with a model that costs a fraction of that to deploy.

---

## 🛠️ Tech Stack

- **Python** — core language
- **Pandas / NumPy** — data manipulation
- **Scikit-learn** — preprocessing, modeling, evaluation
- **XGBoost** — gradient boosting
- **imbalanced-learn (SMOTE)** — class imbalance handling
- **Matplotlib / Seaborn** — visualization
- **Jupyter Notebook** — development environment

