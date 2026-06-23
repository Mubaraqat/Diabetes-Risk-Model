# 🩺 Diabetes Risk Prediction Using Machine Learning

👨🏽‍💻 **Author**

**Onifade Yemi Mubaraqat**  
**Role:** Data Scientist

---

# 📌 Project Overview

This project develops a machine learning solution for predicting diabetes risk using patient health records. The objective is to assist healthcare providers with early identification of high-risk individuals, enabling timely intervention and preventive care.

The project follows a complete end-to-end data science workflow:

- 🧹 Data Cleaning & Preprocessing
- 📊 Exploratory Data Analysis (EDA)
- 🤖 Baseline Model Development
- 🚀 Model Optimization
- 📈 Model Evaluation
- 🏥 Clinical Interpretation of Results

---

# 🎯 Business Problem

Diabetes is a chronic disease that can lead to severe health complications if not detected early.

Healthcare organizations require predictive systems capable of:

- Identifying patients at risk
- Supporting preventive healthcare strategies
- Reducing delayed diagnosis
- Assisting clinicians during screening

This project builds a predictive model that classifies patients as:

- **0 → No Diabetes**
- **1 → Has Diabetes**

---

# 📊 Dataset Information

## Dataset Summary

| Attribute | Value |
|:----------|:------|
| Total Records | 768 |
| Total Features | 8 |
| Target Column | 1 |
| Total Columns | 9 |

---

## Features

| Feature |
|:---------|
| Pregnancies |
| Glucose |
| BloodPressure |
| SkinThickness |
| Insulin |
| BMI |
| DiabetesPedigreeFunction |
| Age |

---

## Target Variable

| Value | Meaning |
|:------|:--------|
| 0 | No Diabetes |
| 1 | Has Diabetes |

---

# 📈 Target Distribution

| Class | Count | Percentage |
|:------|------:|-----------:|
| No Diabetes (0) | 500 | 65.10% |
| Diabetes (1) | 268 | 34.90% |

### 🔍 Observation

The dataset is moderately imbalanced.

This means machine learning models may naturally favor predicting the majority class (healthy patients) unless corrective techniques are applied.

---

# 🧹 Data Cleaning & Preprocessing

## Missing Value Analysis

| Feature | Missing Values |
|:---------|---------------:|
| Glucose | 5 |
| BloodPressure | 35 |
| SkinThickness | 227 |
| Insulin | 374 |
| BMI | 11 |

---

## Missing Value Strategy

Median Imputation was applied to all columns containing missing values.

### Why Median?

- ✅ Robust against outliers
- ✅ Suitable for skewed medical variables
- ✅ Preserves dataset size
- ✅ Prevents loss of valuable patient records

### Result

✅ All missing values were successfully removed.

---

# 📊 Exploratory Data Analysis (EDA)

## 📌 Figure 1 — Diabetes Distribution

### Findings

- 500 healthy patients
- 268 diabetic patients

### Insight

The dataset contains more healthy individuals than diabetic individuals. This imbalance can negatively affect model performance if not addressed.

---

## 📌 Figure 2 — Glucose Distribution by Outcome

### Findings

| Group | Median Glucose |
|:------|:---------------|
| Non-Diabetic | 107.5 mg/dL |
| Diabetic | 140.0 mg/dL |

### Insight

Glucose levels show strong separation between diabetic and non-diabetic patients, making it one of the strongest predictors of diabetes.

---

## 📌 Figure 3 — Correlation Heatmap

### Strongest Relationships with Diabetes

| Feature | Correlation |
|:---------|------------:|
| Glucose | 0.49 |
| BMI | 0.31 |
| Age | 0.24 |

### Insight

Higher glucose levels, elevated BMI, and increasing age are associated with greater diabetes risk.

---

# 🤖 Machine Learning Development

## Data Splitting

| Dataset | Size |
|:---------|-----:|
| Training Set | 80% (614 patients) |
| Testing Set | 20% (154 patients) |

---

## Stratification

Stratified sampling was applied to preserve the original class distribution in both training and testing datasets.

---

# 📍 Baseline Model

## Algorithm

**Logistic Regression**

---

## Performance

| Metric | Score |
|:--------|------:|
| Accuracy | **0.7727** |
| Precision | **0.7100** |
| Recall | **0.6900** |
| F1 Score | **0.7000** |

---

## Baseline Confusion Matrix

| | Predicted Healthy | Predicted Diabetic |
|:-------------------|------------------:|-------------------:|
| **Actual Healthy** | 85 | 15 |
| **Actual Diabetic** | 17 | 37 |

---

## Clinical Interpretation

- **True Negatives:** 85
- **False Positives:** 15
- **False Negatives:** 17
- **True Positives:** 37

### 🏥 Medical Assessment

The baseline model correctly identified **77.27%** of cases overall. However, it leaves a significant gap in catching all positive instances, missing **17 diabetic individuals** and incorrectly classifying them as healthy.

Since healthcare screening prioritizes minimizing missed diagnoses, hyperparameter tuning via cross-validation was performed to determine whether predictive performance could be further improved.

---

# 🚀 Model Optimization

To thoroughly test the predictive boundaries of the model, the following improvements were implemented.

---

## Feature Scaling

```python
StandardScaler()
```

### Benefits

- Normalizes feature ranges
- Prevents dimensional bias
- Improves coefficient learning
- Enhances model stability

---

## Hyperparameter Tuning

```python
GridSearchCV()
```

### Parameters Tuned

**Regularization Strength**

```python
C = [0.01, 0.1, 1, 10, 100]
```

**Solver**

```python
[
    "liblinear",
    "lbfgs"
]
```

**Optimization Metric**

- Recall

---

## Best Hyperparameters

```python
{
    "model__C": 1.0,
    "model__penalty": "l2",
    "model__solver": "lbfgs"
}
```

---

# 🏆 Optimized Model Results

When evaluated on the untouched testing dataset (**n = 154**), the optimized model achieved the following performance.

| Metric | Score |
|:--------|------:|
| Accuracy | **0.7922** |
| Precision | **0.7100** |
| Recall | **0.6900** |
| F1 Score | **0.7000** |

---

# 📊 Optimized Confusion Matrix

| | Predicted Healthy | Predicted Diabetic |
|:-------------------|------------------:|-------------------:|
| **Actual Healthy** | 85 | 15 |
| **Actual Diabetic** | 17 | 37 |

---

## Breakdown

| Metric | Value |
|:--------|------:|
| True Negative (TN) | 85 |
| False Positive (FP) | 15 |
| False Negative (FN) | 17 |
| True Positive (TP) | 37 |

---

# 🏥 Medical Context Interpretation

### The Finalized Model Shows

### ✅ Robust Accuracy

The model correctly classified **79.22%** of all patients, providing a reliable diagnostic triage baseline.

### ✅ Balanced False Alarms

A precision score of **71%** means that when the system flags a patient as high risk, approximately **7 out of every 10** predictions are correct, keeping false alarms manageable.

### ✅ Stable Sensitivity

The model captures **69%** of true diabetic cases, making it a useful screening tool before confirmatory laboratory testing.

---

## 📌 Verdict

Hyperparameter optimization confirmed that the baseline Logistic Regression model had essentially reached the performance ceiling achievable for a linear classifier on this dataset.

The model is therefore suitable as a **clinical decision-support tool**, but **must never replace professional medical diagnosis**.

---

# 🔍 Feature Importance

## Top Predictors of Diabetes

| Rank | Feature | Importance |
|:----:|:---------|:-----------|
| 1 | Glucose | Highest Positive |
| 2 | BMI | High Positive |
| 3 | Age | Moderate Positive |

### Key Finding

Plasma glucose concentration, BMI, and age emerged as the strongest predictors of diabetes, aligning with established clinical and epidemiological evidence.

---

# 📌 Model Comparison

| Metric | Baseline | Optimized |
|:--------|---------:|----------:|
| Accuracy | 0.7727 | **0.7922** |
| Precision | 0.7100 | 0.7100 |
| Recall | 0.6900 | 0.6900 |
| F1 Score | 0.7000 | 0.7000 |

---

## ✅ Improvement Summary

- ✔ Data standardization improved numerical stability.
- ✔ Cross-validation confirmed optimal hyperparameters.
- ✔ The model achieved a peak validation accuracy of **79.22%**.
- ✔ Logistic Regression reached the practical performance ceiling for this dataset.

---

# 🏁 Conclusion

This project successfully developed an end-to-end machine learning pipeline capable of predicting diabetes risk using patient clinical indicators.

Through careful preprocessing, median imputation, feature scaling, and hyperparameter optimization, the final Logistic Regression model achieved:

- **79.22% Accuracy**
- **71% Precision**
- **69% Recall**
- **70% F1 Score**

Although linear models appear to have reached their performance limit on this dataset, the project establishes a strong and interpretable baseline for future machine learning enhancements.

---

# 🚀 Future Improvements

- 🌳 Random Forest
- ⚡ XGBoost
- 🎯 Probability Threshold Optimization
- 🧬 Integration of HbA1c and Family History
- 🔍 Explainable AI using SHAP
- ⚖️ SMOTE for Class Imbalance
- 🌐 Streamlit Deployment

---

# 🛠️ Technologies Used

- 🐍 Python
- 📊 Pandas
- 🔢 NumPy
- 📉 Matplotlib
- 🎨 Seaborn
- 🤖 Scikit-Learn
- 📓 Jupyter Notebook
- 💻 VS Code

---

# 📜 License

This project is intended for **educational**, **research**, and **portfolio** purposes.

---

## ⭐ If you found this project helpful, consider giving it a Star!
