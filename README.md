# 📊 Students Performance — EDA & Data Preprocessing

An **Exploratory Data Analysis (EDA)** and preprocessing project on the **Students Performance dataset**. The project covers feature selection, missing value handling, and outlier removal to prepare clean data for machine learning.


---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset](#-dataset)
- [Preprocessing Steps](#️-preprocessing-steps)
- [Libraries Used](#️-libraries-used)
- [How to Run](#-how-to-run)
- [Project Structure](#-project-structure)

---

## 📌 Project Overview

This project performs end-to-end **data cleaning and preprocessing** on a Students Performance dataset. The goal is to:

- Remove low-variance (non-informative) features
- Handle missing values in both numeric and categorical columns
- Remove outliers using the **IQR method**
- Prepare the dataset for downstream ML models

---

## 📂 Dataset

- **File:** `StudentsPerformance.csv`
- **Rows:** 1000 students
- **Columns:** 8 features

| Column | Type | Description |
|---|---|---|
| `gender` | Categorical | Male / Female |
| `race/ethnicity` | Categorical | Group A to E |
| `parental level of education` | Categorical | Education level of parents |
| `lunch` | Categorical | Standard / Free-Reduced |
| `test preparation course` | Categorical | Completed / None |
| `math score` | Numeric | Score in Math (0–100) |
| `reading score` | Numeric | Score in Reading (0–100) |
| `writing score` | Numeric | Score in Writing (0–100) |

### Sample Data:

| gender | race | parental edu | lunch | test prep | math | reading | writing |
|---|---|---|---|---|---|---|---|
| female | group B | bachelor's | standard | none | 72 | 72 | 74 |
| female | group C | some college | standard | completed | 69 | 90 | 88 |
| male | group A | associate's | free/reduced | none | 47 | 57 | 44 |

---

## ⚙️ Preprocessing Steps

### Step 1 — Variance Threshold Feature Selection
```
VarianceThreshold(threshold=0.5)
```
- Separated numeric columns from categorical
- Removed any numeric feature with variance below **0.5**
- Kept all categorical columns as-is
- Only informative numeric features retained

---

### Step 2 — Handle Missing Values

**Numeric columns:**
- Filled missing values with **column mean**

**Categorical columns:**
- Filled missing values with **column mode** (most frequent value)

```python
df[numeric_cols] = df[numeric_cols].fillna(df.mean(numeric_only=True))
df[cat_col] = df[cat_col].fillna(df[cat_col].mode()[0])
```

✅ After this step: `df.isnull().sum()` = 0 for all columns

---

### Step 3 — Outlier Removal (IQR Method)

Applied **IQR-based outlier removal** on:
- `math score`
- `reading score`

**Formula:**
```
Q1 = 25th percentile
Q3 = 75th percentile
IQR = Q3 - Q1
Lower Bound = Q1 - 1.5 × IQR
Upper Bound = Q3 + 1.5 × IQR
```

Rows outside the bounds are dropped — keeping only clean, valid data.

---

## 🛠️ Libraries Used

```
pandas
numpy
seaborn
matplotlib
scikit-learn (VarianceThreshold)
```

---

## 🚀 How to Run

1. Clone the repository:
```bash
git clone https://github.com/hamza93-ai/Students-Performance-EDA.git
```

2. Open the notebook:
```bash
jupyter notebook students_performance_eda_preprocessing.ipynb
```

3. Place `StudentsPerformance.csv` in the same directory and run all cells.

---

## 📁 Project Structure

```
Students-Performance-EDA/
│
├── students_performance_eda_preprocessing.ipynb   # Main notebook
├── StudentsPerformance.csv                        # Dataset
└── README.md                                      # Project documentation
```

---

## 👤 Author

**Hamza Asif**
