# 🛡️ Ethereum Fraud Detection: End-to-End ML Pipeline

![Python](https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python)
![LightGBM](https://img.shields.io/badge/LightGBM-Ensemble-green?style=for-the-badge)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Machine%20Learning-orange?style=for-the-badge&logo=scikitlearn)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter)

## 📖 Project Overview
Fraud in cryptocurrency (such as phishing, Ponzi schemes, and money laundering) is a major problem. This project presents a comprehensive machine learning pipeline designed to detect fraudulent activities within the Ethereum blockchain. 

The primary objective is to build a robust classifier that prioritizes catching fraudsters (**high Recall**) without sacrificing the experience of legitimate users. By analyzing behavioral patterns in transaction timing, volume, and smart contract interactions, the model automatically flags suspicious wallet addresses.

## 📊 Dataset
* **Source:** Ethereum Fraud Detection Dataset.
* **Size:** 9,841 unique wallet addresses.
* **Class Imbalance:** Highly imbalanced (~78% Non-Fraud vs. ~22% Fraud).
* **Features:** Transaction counts, Ether values, ERC20 token metrics, and temporal behaviors.

## ⚙️ Methodology & Pipeline
1. **Data Cleaning:** Removed identifiers (Address, Index) and near-constant features. Applied Median Imputation for missing ERC20 values to prevent zero-inflation bias.
2. **Feature Selection:** Dropped highly multicollinear features (e.g., perfect 1.0 correlation among ERC20 min/max values) to prevent overfitting.
3. **Handling Imbalance:** Applied **SMOTE** (Synthetic Minority Over-sampling Technique) *strictly* on the training data to prevent data leakage.
4. **Model Benchmarking:** Evaluated multiple tree-based ensembles (LightGBM, XGBoost, CatBoost, Random Forest) using PyCaret.
5. **Hyperparameter Tuning:** Utilized `RandomizedSearchCV` (5-fold CV) optimized specifically for **Recall**, as missing a fraudster (False Negative) is far more costly than a false alarm.

## 🏆 Results
The optimized LightGBM model successfully captured complex, non-linear behavioral patterns, significantly reducing false negatives.

| Model | Accuracy | F1-Score | Fraud Recall | False Negatives |
| :--- | :--- | :--- | :--- | :--- |
| Baseline LightGBM | 99.4% | 0.987 | 97.8% | 13 |
| **Tuned LightGBM (Winner)** | **99.3%** | **0.970** | **98.2%** | **9** |

*The tuned model successfully intercepted all but 9 out of 436 fraudulent cases in the test set.*

## 💡 Key Insights (Feature Importance)
* **The "Hit and Run" Behavior:** The time difference between the first and last transaction is the strongest predictor of fraud. Fraudulent wallets are typically short-lived, created to execute a scam, and abandoned immediately.
* **Network Diversity:** The number of unique addresses a wallet receives funds from is a critical signal. Fraudsters often receive funds from a wide network of victims.
* **Token Activity:** Fraudsters tend to avoid heavy ERC20 token trading, likely to evade detection algorithms or liquidate stolen funds rapidly.

## 📂 Repository Structure
```text
├── notebooks/
│   └── ethereum-fraud-detection.ipynb    # Main Jupyter Notebook (EDA, Modeling, Tuning)
├── requirements.txt                      # Python dependencies
└── README.md                             # Project documentation
```

## 🚀 How to Run

1. Clone the repository:
   git clone https://github.com/AliPakzad/Ethereum-Fraud-Detection.git

2. Install the required packages:
   pip install -r requirements.txt

3. Open the Jupyter Notebook and run the cells:
   jupyter notebook notebooks/ethereum-fraud-detection.ipynb

## 🔗 Links
* **Kaggle Notebook:** https://www.kaggle.com/code/alipakzad/ethereum-fraud-detection-eda-to-lightgbm-97-f1
* **Personal Portfolio:** https://www.linkedin.com/in/ali-pakzad-b145a3b4

---
**Author:** Ali Pakzad (Data Scientist & ML Engineer)
