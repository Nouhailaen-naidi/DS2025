# Online Shoppers Purchasing Intention Dataset

## Overview
- **Dataset Name:** Online Shoppers Purchasing Intention
- **Donated on:** 30/08/2018
- **Total Sessions:** 12,330
  - Negative class (no purchase): 10,422 (84.5%)
  - Positive class (purchase): 1,908 (15.5%)
- **Subject Area:** Business / E-commerce
- **Dataset Type:** Multivariate
- **Associated Tasks:** Classification, Clustering
- **Feature Types:** Integer, Real
- **Total Features:** 17
- **Missing Values:** None

---

## Dataset Description
This dataset contains feature vectors from 12,330 browsing sessions. Each session corresponds to a different user recorded over a one‑year period. This ensures no bias from specific campaigns, special days, user profiles, or time periods.

The goal is typically to **predict the purchasing intention** (Revenue = True/False) using behavioral, technical, and engagement‑based features.

---

## Introductory Paper
**Title:** *Real-time prediction of online shoppers’ purchasing intention using multilayer perceptron and LSTM recurrent neural networks*

- **Authors:** C. O. Sakar, S. Polat, Mete Katircioglu, Yomi Kastro
- **Published in:** Neural Computing & Applications (Print), 2019
- **Citation DOI:** 10.24432/C5F88Q

Dataset license: **CC BY 4.0** (free to use and adapt with attribution).

---

## Variables Table

| Variable Name              | Role       | Type       | Description | Missing |
|----------------------------|------------|------------|-------------|---------|
| Administrative             | Feature    | Integer    | Administrative pages visited | No |
| Administrative_Duration    | Feature    | Integer    | Time spent on administrative pages | No |
| Informational              | Feature    | Integer    | Informational pages visited | No |
| Informational_Duration     | Feature    | Integer    | Time spent on informational pages | No |
| ProductRelated             | Feature    | Integer    | Product-related pages visited | No |
| ProductRelated_Duration    | Feature    | Continuous | Time spent on product-related pages | No |
| BounceRates                | Feature    | Continuous | Bounce rate of entry page | No |
| ExitRates                  | Feature    | Continuous | Exit rate of last viewed page | No |
| PageValues                 | Feature    | Integer    | Estimated transaction value of the page | No |
| SpecialDay                 | Feature    | Integer    | Closeness to a special shopping day | No |
| OS, Browser, Region, ...   | Categorical| Varies     | Visitor technical & categorical data | No |
| Weekend                    | Boolean    | Categorical| Visit occurred on weekend | No |
| Month                      | Categorical| Category   | Month of the visit | No |
| Revenue                    | Target     | Boolean    | Purchase made (True/False) | No |

---

## Additional Variable Information
- The dataset includes **10 numerical** and **8 categorical** variables.
- The **Revenue** column is the target label.
- Page-related variables are derived from **URL metadata**.
- BounceRates, ExitRates, PageValues originated from **Google Analytics metrics**.
- SpecialDay is a numeric metric showing proximity to major sale days (e.g., Valentine's Day).

Example:
- SpecialDay = 1 on **February 8** (peak for Valentine's Day purchases).
- Non-zero between February 2–12.

Other variables include:
- Operating System
- Browser type
- Geographic Region
- Traffic Type
- Visitor Type (Returning / New)
- Weekend flag
- Month of the year

---

## Python Code: Loading Dataset via UCI Repository
```python
# Install the UCI ML Repo package
!pip install ucimlrepo

from ucimlrepo import fetch_ucirepo

# Fetch dataset by ID
online_data = fetch_ucirepo(id=468)

# Features and target
X = online_data.data.features
y = online_data.data.targets

# Metadata
print(online_data.metadata)

# Variable information
print(online_data.variables)
```

---

## Exploratory Data Analysis (for Google Colab)
### View dataset
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.concat([X, y], axis=1)
df.head()
```

### Class distribution
```python
sns.countplot(x='Revenue', data=df)
plt.title("Class Distribution: Purchase vs No Purchase")
plt.show()
```

### Correlation Heatmap
```python
plt.figure(figsize=(12, 7))
sns.heatmap(df.corr(numeric_only=True), annot=True, cmap='coolwarm')
plt.title("Correlation Matrix of Numerical Features")
plt.show()
```

### Distribution of Page Visit Counts
```python
features = ['Administrative', 'Informational', 'ProductRelated']
df[features].hist(bins=25, figsize=(10,5))
plt.suptitle("Distribution of Page Visit Counts")
plt.show()
```

---

## Next Steps for Analysis
- Feature engineering (scaling, encoding categorical variables)
- Model building:
  - Logistic Regression
  - Random Forest
  - Gradient Boosting
  - LSTM/RNN models for sequential behavior analysis
- Cross‑validation and evaluation (Precision, Recall, AUC)
- Visualization of model performance

---

## Citation
Sakar, C. & Kastro, Y. (2018). *Online Shoppers Purchasing Intention Dataset* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5F88Q

