# 🏥 Medical Insurance Charges Analysis & Prediction

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![Excel](https://img.shields.io/badge/Microsoft%20Excel-Analysis-217346?logo=microsoft-excel)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Regression-orange?logo=scikit-learn)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

> **Uncovering the true drivers of medical insurance costs through exploratory data analysis and linear regression — with smoking status emerging as the single most powerful predictor of healthcare charges.**

---

## 📌 Problem Statement

Insurance companies manage risk by pricing policies according to individual characteristics. But which factors most meaningfully predict medical charges — and by how much?

This project performs a complete data analysis workflow on an insurance dataset covering **1,337 individuals**, aiming to:
- Identify the key drivers of medical insurance charges through EDA
- Quantify the impact of age, BMI, and smoking status on costs
- Build and evaluate a **linear regression model** that predicts charges based on individual attributes
- Deliver insights relevant to healthcare policy, actuarial modeling, and risk management

---

## 🎯 Objectives

| # | Objective |
|---|-----------|
| 1 | Perform thorough EDA to reveal patterns, distributions, and outliers |
| 2 | Analyze the influence of smoking status, age, and BMI on insurance charges |
| 3 | Build a linear regression model using Age, BMI, and Smoker status as predictors |
| 4 | Evaluate model performance and interpret residuals |
| 5 | Deliver actionable insights for insurers and healthcare policy makers |

---

## 🏗️ System Architecture

```
┌────────────────────────────────────────────────────────────────┐
│                    ANALYSIS PIPELINE                           │
│                                                                │
│  Raw Insurance Dataset (CSV, 1338 records)                     │
│         │                                                      │
│         ▼                                                      │
│  Data Cleaning (Python)                                        │
│  ├── Missing value check                                       │
│  ├── Duplicate removal (1 removed → 1337 records)             │
│  ├── Outlier detection (Z-score method on BMI & Charges)       │
│  └── Statistical summary                                       │
│         │                                                      │
│         ▼                                                      │
│  EDA & Visualization (Python + Excel)                          │
│  ├── Correlation matrix                                        │
│  ├── Distribution plots (KDE)                                  │
│  ├── Scatter plots (Age/BMI vs Charges, coloured by Smoker)    │
│  └── Smoker vs Non-smoker charge comparison                    │
│         │                                                      │
│         ▼                                                      │
│  Linear Regression Model                                       │
│  ├── Independent variables: Age, BMI, Smoker (binary)         │
│  ├── Dependent variable: Insurance Charges                     │
│  └── Implemented & validated in both Python and Excel         │
│         │                                                      │
│         ▼                                                      │
│  Model Evaluation                                              │
│  ├── R² = 0.749 (74.9% variance explained)                    │
│  ├── Actual vs Predicted scatter plot                          │
│  └── Residual analysis                                         │
└────────────────────────────────────────────────────────────────┘
```

---

## 💡 Solution Approach

### 1. Data Cleaning
- **Dataset size**: 1,338 records → 1,337 after removing 1 duplicate
- Verified no null values in critical columns
- Detected and handled outliers in **BMI** and **Charges** using the **Z-score method** to prevent skewed regression results
- Generated statistical summaries (mean, median, std dev) for all numerical columns

### 2. Correlation Analysis

| Feature | Correlation with Charges |
|---------|--------------------------|
| Age | 0.30 (moderate positive) |
| BMI | 0.20 (moderate positive) |
| Children | 0.07 (minimal impact) |
| **Smoker** | **Strongest predictor** (binary) |

### 3. Exploratory Data Analysis (EDA)

**Charges Distribution:**
- Right-skewed — majority of charges fall between **$0–$15,000**
- A smaller high-risk group drives charges above **$30,000**
- Peak density around **$10,000** — most individuals are low-risk

**Smoking Status Impact:**
- Smokers: Average charges between **$30,000–$40,000**
- Non-smokers: Average charges between **$10,000–$15,000**
- This 3x cost difference is the most significant pattern in the dataset

**Age vs Charges:**
- Positive correlation (equation: `y = 253.9x + 3125.8`)
- R² = 0.1238 — age alone explains only 12.4% of charge variation
- Two distinct clusters visible — driven by smoker vs non-smoker separation

**BMI vs Charges:**
- Positive correlation (equation: `y = 376.1x + 1595.7`)
- R² = 0.049 — BMI alone explains only 4.9% of charges
- High-charge cluster (>$25,000) driven by unaccounted variables, primarily smoking

### 4. Linear Regression Model

**Model Equation:**
```
Predicted Charges = β₀ + β₁(Age) + β₂(BMI) + β₃(Smoker)
```
Where `Smoker` is encoded as: 1 = Smoker, 0 = Non-Smoker

**Model Performance:**

| Metric | Value |
|--------|-------|
| R² | **0.749** |
| Variance Explained | **74.9%** |
| Model Fit | Reasonably strong |
| Slope (Actual vs Predicted) | 0.749 |
| Intercept | 3,288.3 |

### 5. Residual Analysis
- Residuals are **randomly scattered** across age groups — no systematic bias
- Slight tendency to **underpredict** charges for certain age groups
- Outlier residuals visible at ages ~20 and ~60 — individuals with extreme cost profiles

---

## 📊 Results & Key Findings

### Predicted Charges — Smokers vs Non-Smokers

| Group | Count | Total Predicted Charges | Average per Person |
|-------|-------|-------------------------|--------------------|
| **Smokers** | 265 | $8,314,362.30 | **$31,374.95** |
| **Non-Smokers** | 1,043 | $8,818,313.69 | **$8,454.76** |

> 💡 **Smokers cost insurers ~3.7x more on average than non-smokers.**

### Feature Importance Summary

| Predictor | Significance | Impact Direction |
|-----------|-------------|-----------------|
| Smoking Status | ⭐⭐⭐⭐⭐ Highest | Strong positive |
| Age | ⭐⭐⭐ Moderate | Positive |
| BMI | ⭐⭐ Low-Moderate | Positive |
| Children | ⭐ Minimal | Negligible |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **Python 3.x** | Core analysis and modeling |
| **Pandas** | Data loading, cleaning, manipulation |
| **NumPy** | Numerical computations, Z-score outlier detection |
| **Scikit-learn** | Linear regression modeling |
| **Matplotlib / Seaborn** | KDE plots, scatter plots, residual charts |
| **Microsoft Excel** | Regression output validation, visual reporting |

---

## 📁 Project Structure

```
medical-insurance-analysis/
│
├── data/
│   └── insurance.csv                   # Raw insurance dataset (1338 records)
│
├── notebooks/
│   └── insurance_analysis.ipynb        # Full EDA + regression pipeline
│
├── excel/
│   └── regression_analysis.xlsx        # Excel-based regression output & charts
│
├── visuals/
│   ├── charge_distribution_kde.png     # KDE plot of insurance charges
│   ├── age_vs_charges_smoker.png       # Scatter plot coloured by smoker status
│   ├── bmi_vs_charges.png              # BMI regression scatter
│   ├── actual_vs_predicted.png         # Model performance chart
│   └── residual_plot.png              # Residual analysis
│
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
```bash
pip install pandas numpy scikit-learn matplotlib seaborn openpyxl
```

### Run the Analysis
```bash
# Clone the repo
git clone https://github.com/yourusername/medical-insurance-analysis.git
cd medical-insurance-analysis

# Open notebook
jupyter notebook notebooks/insurance_analysis.ipynb
```

### Core Code Snippet
```python
from sklearn.linear_model import LinearRegression
import pandas as pd

df = pd.read_csv('data/insurance.csv')
df = df.drop_duplicates()

# Encode smoker as binary
df['smoker_binary'] = df['smoker'].map({'yes': 1, 'no': 0})

X = df[['age', 'bmi', 'smoker_binary']]
y = df['charges']

model = LinearRegression()
model.fit(X, y)

print(f"R² Score: {model.score(X, y):.3f}")
print(f"Coefficients: {dict(zip(X.columns, model.coef_))}")
```

---

## ⚠️ Limitations

- Linear regression assumes a **linear relationship** between features and charges — non-linear models (e.g., Random Forest, XGBoost) may yield better accuracy
- **25.1% of variance remains unexplained** — additional variables like pre-existing conditions, lifestyle, and regional healthcare costs could improve the model
- Interaction terms (e.g., Age × Smoker) were not modeled — combining these may reveal non-additive effects
- Dataset is cross-sectional — no longitudinal tracking of charge changes over time

---

## 🌍 Project Impact

| Stakeholder | Benefit |
|-------------|---------|
| **Insurance Companies** | Smoking status should carry heavy weight in risk-based pricing models |
| **Healthcare Policy Makers** | Data-driven evidence for smoking cessation program investment |
| **Actuaries** | Baseline regression framework to build more complex pricing models upon |
| **Individuals** | Awareness of how lifestyle choices (especially smoking) dramatically impact insurance costs |

---

## 🔮 Future Enhancements

- Incorporate additional features: **region, pre-existing conditions, exercise habits**
- Experiment with non-linear models: **Random Forest, Gradient Boosting, Neural Networks**
- Add interaction terms: `age × smoker`, `bmi × smoker`
- Deploy a simple **Streamlit web app** for real-time charge prediction

---

## 📚 References

- Scikit-learn Linear Regression: https://scikit-learn.org/stable/modules/linear_model.html
- Dataset: Medical Cost Personal Dataset — [Kaggle](https://www.kaggle.com/mirichoi0218/insurance)
- WHO Report on Tobacco and Health Expenditure: https://www.who.int/tobacco

---

## 👤 Author

**[Mahima Srinivasan]**
- 📧 [mahima.s3994@gmail.com.com]
- 💼 [linkedin.com/in/mahimasrinivasan3994]

> *This project demonstrates end-to-end data analysis skills — from cleaning and EDA through regression modeling and business interpretation.*

---

*⭐ If you found this project useful, please consider starring the repository!*
