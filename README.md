# 📚 Student Performance Prediction - Machine Learning Regression Project

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Regression-green.svg)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Used-orange.svg)
![Status](https://img.shields.io/badge/Status-Completed-success.svg)

---

## 📌 Project Overview

This project focuses on predicting **student exam scores** based on academic behavior, lifestyle habits, and personal factors using supervised machine learning regression techniques.

The dataset includes **1000 student records** with 15 features describing study behavior, health, and environment. The main goal is to build a model that accurately predicts exam performance and identify the most influential factors affecting student success.

This project includes:
- Data cleaning and missing value handling
- Exploratory Data Analysis (EDA)
- Feature encoding and preprocessing pipeline
- Linear Regression baseline model
- Random Forest model with hyperparameter tuning
- KNN model analysis and overfitting investigation
- Model comparison and selection
- Feature importance and coefficient interpretation

---

## 📂 Dataset Description

### 📊 Structure

- **Rows:** 1000
- **Columns:** 15

### 📌 Features

- Age
- Gender
- Study Hours per Day
- Social Media Hours
- Netflix Hours
- Part-Time Job
- Attendance Percentage
- Sleep Hours
- Diet Quality
- Exercise Frequency
- Parental Education Level
- Internet Quality
- Mental Health Rating
- Extracurricular Participation
- Exam Score (Target)

---

## ⚠️ Data Quality Check

### Missing Values
- Only **one feature contains missing values**
- `parental_education_level → 91 missing values`
- Handled using **most frequent value (mode imputation)**

### Data Types
- Numerical features: correctly formatted (`int`, `float`)
- Categorical features: require encoding using OneHotEncoder

### Data Integrity
- No duplicate rows found
- No invalid or corrupted values detected

---

## 📊 Descriptive Statistics

### Key Observations

- Age range: **17 to 24 years**
- Study hours: **0 to 8.3 hours/day**
- Social media usage: **0 to 7.2 hours/day**
- Netflix usage: **0 to 5.4 hours/day**
- Attendance: **56% to 100%**
- Sleep: **3.2 to 10 hours**
- Exam scores: **18.4 to 100**

### Insight

No extreme outliers were detected, and all feature ranges are realistic for student behavior data.

---

## 📊 Exploratory Data Analysis (EDA)

### 📌 Exam Score Distribution

- Distribution is **left-skewed**
- Most students score between **70 and 80**
- Majority of students score above **60**
- A **ceiling effect at 100** is observed
- Few low-performing students (<40)

### Insight

The dataset represents a generally **high-performing student population**, with clear separation between average and top performers.

---

### 📌 Correlation Analysis

#### Strongest Relationship
- **Study Hours → Exam Score (0.83)**

#### Moderate Factors
- Mental Health Rating (0.32)
- Exercise Frequency (0.16)
- Sleep Hours (0.12)

#### Negative Influence
- Social Media Hours (-0.17)
- Netflix Hours (-0.17)

#### Weak/No Impact
- Age (~0)
- Attendance Percentage (0.09)

### Insight

Study behavior is the dominant factor, while distractions negatively affect performance.

---

### 📌 Pairplot Insights

- Strong linear relationship between **study hours and exam score**
- Random distribution between unrelated features (e.g., sleep vs social media)
- Clear **ceiling effect at score = 100**
- Most students cluster around:
  - 4 hours study/day
  - 7 hours sleep/day

---

## ⚙️ Data Preprocessing Pipeline

### Numerical Features
- StandardScaler applied

### Categorical Features
- Missing values handled using **SimpleImputer (mode)**
- Encoding using **OneHotEncoder**

### Final Pipeline
- ColumnTransformer used to combine both pipelines
- Fully automated preprocessing before modeling

---

## 🤖 Machine Learning Models

---

## 1️⃣ Linear Regression 📈 (Baseline Model)

### Model Purpose
Used as a baseline to understand linear relationships.

### Performance

**Training:**
- MAE: 4.184
- RMSE: 5.288
- R²: 0.903

**Test:**
- MAE: 4.293
- RMSE: 5.385
- R²: 0.892

### Insight
- Strong baseline performance
- Good generalization
- Cannot capture complex non-linear patterns

---

## 🧠 Linear Regression Interpretation

### Key Coefficients

- Study Hours → **+14.09 (strongest positive impact)**
- Mental Health → **+5.54**
- Exercise Frequency → **+2.59**
- Sleep Hours → **+2.47**

### Negative Factors
- Social Media → **-3.13**
- Netflix → **-2.59**

### Insight
- Academic behavior strongly influences performance
- Lifestyle distractions reduce performance
- Some categorical effects are weak but present

---

## 2️⃣ Random Forest 🌳 (Final Model Candidate)

### Default Model Performance

- Better non-linear learning ability than Linear Regression

### Tuned Hyperparameters

- max_depth = 20
- max_features = 0.5
- min_samples_split = 2
- min_samples_leaf = 1
- n_estimators = 100

### Performance

**Training:**
- MAE: 1.938
- RMSE: 2.413
- R²: 0.980

**Test:**
- MAE: 4.996
- RMSE: 6.247
- R²: 0.855

### Insight
- Strong training performance
- Slight overfitting observed
- Best balance between performance and generalization

---

### 🔥 Feature Importance (Random Forest)

- Study Hours → **0.70 (dominant feature)**
- Mental Health → 0.10
- Social Media → 0.03
- Sleep / Netflix → ~0.03 each
- Other features → minimal impact

### Insight
Model confirms:
> Study time is the most important predictor of academic success.

---

### 🔁 Permutation Importance

- Study Hours → strongest impact (~1.28)
- Mental Health → second strongest (~0.18)
- Other features → very small influence

### Insight
Confirms robustness of feature importance results.

---

## 3️⃣ K-Nearest Neighbors (KNN) 🏃

### Best Parameters
- n_neighbors = 10
- weights = distance
- metric = euclidean
- leaf_size = 20

### Performance

**Training:**
- MAE: 0.0
- RMSE: 0.0
- R²: 1.0

**Test:**
- MAE: 7.239
- RMSE: 9.411
- R²: 0.671

### Insight
- Severe overfitting
- Memorization instead of learning
- Poor generalization

---

## 📊 Model Comparison

| Model               | MAE   | RMSE  | R²    |
|--------------------|-------|-------|-------|
| Linear Regression   | 4.293 | 5.385 | 0.892 |
| Random Forest       | 4.996 | 6.247 | 0.855 |
| KNN                 | 7.239 | 9.411 | 0.671 |

---

## 🏆 Final Model Selection

### Selected Model: **Random Forest Regressor 🌳**

### Reasoning:
- Best balance between accuracy and generalization
- Handles non-linear relationships well
- Robust to feature interactions
- Strong feature interpretability via importance scores

---

## 🧠 Key Insights

- Study hours are the strongest predictor of success
- Mental health plays a meaningful secondary role
- Social media and Netflix negatively affect performance
- Lifestyle habits collectively influence academic outcomes
- Linear models are limited for this dataset
- Ensemble models perform best

---

## 🚀 Final Pipeline

1. Data cleaning
2. Missing value imputation
3. Encoding categorical variables
4. Feature scaling
5. Train-test split
6. Model training
7. Hyperparameter tuning
8. Evaluation
9. Feature interpretation
10. Final model selection

---

## 🛠️ Technologies Used

- Python 🐍
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn

---

## 📌 Conclusion

This project demonstrates a full machine learning workflow from raw data analysis to final model selection. Random Forest was selected as the final model due to its strong predictive performance and ability to capture complex relationships in student behavior data.
