# Online Shoppers Purchasing Intention Dataset — Full Analytical Report

## 1. Introduction
This report provides a **complete, structured, and detailed analysis** of the *Online Shoppers Purchasing Intention Dataset*. It is designed to be uploaded on **GitHub** and used seamlessly in **Google Colab** for data exploration, visualization, and machine learning tasks.

The goal of this dataset is to **predict whether an online visitor will make a purchase** based on behavioral and technical browsing features.

---

## 2. Dataset Overview
- **Dataset Name:** Online Shoppers Purchasing Intention
- **Source:** UCI Machine Learning Repository
- **Donated on:** 30/08/2018
- **Total Sessions:** 12,330
  - Negative class (no purchase): **10,422** (84.5%)
  - Positive class (purchase): **1,908** (15.5%)
- **Subject Area:** Business & E-commerce
- **Dataset Type:** Multivariate
- **Associated Tasks:** Classification, Clustering
- **Feature Types:** Integer, Real, Categorical
- **Total Features:** 17
- **Missing Values:** None
- **Target Variable:** `Revenue` (True/False)

The dataset was constructed so that each session corresponds to a **unique visitor** over one year, eliminating bias from special seasonal events, campaigns, or user repetition.

---

## 3. Dataset Variables
Below is a summarized table of key variables:

| Variable Name | Type | Description |
|---------------|------|-------------|
| Administrative | Integer | Number of administrative pages visited |
| Administrative_Duration | Integer | Time spent on administrative pages |
| Informational | Integer | Informational pages visited |
| Informational_Duration | Integer | Time spent on informational pages |
| ProductRelated | Integer | Product-related pages visited |
| ProductRelated_Duration | Continuous | Time spent on product pages |
| BounceRates | Continuous | % of visitors leaving instantly |
| ExitRates | Continuous | % of sessions ending on a given page |
| PageValues | Real | Estimated value of page before purchase |
| SpecialDay | Real | Proximity to special sales days |
| OperatingSystem | Categorical | OS used |
| Browser | Categorical | Browser type |
| Region | Categorical | Visitor region |
| TrafficType | Categorical | Type of traffic source |
| VisitorType | Categorical | New or Returning visitor |
| Weekend | Boolean | Visit occurred on weekend |
| Month | Category | Month of visit |
| Revenue | Boolean (TARGET) | Indicates purchase |

---

## 4. Additional Variable Information
- `BounceRates`, `ExitRates`, and `PageValues` come from **Google Analytics** measurements.
- `SpecialDay` measures closeness to events such as **Valentine’s Day** or **Mother’s Day**.
- Example: For Valentine's Day, SpecialDay is:
  - Non-zero from **Feb 2 to Feb 12**
  - Peak = **1 on Feb 8**

---

## 5. Loading the Dataset in Google Colab
Use the **ucimlrepo** library to import the dataset:

```python
!pip install ucimlrepo

from ucimlrepo import fetch_ucirepo

# Fetch dataset
online_data = fetch_ucirepo(id=468)

# Dataframes
X = online_data.data.features
y = online_data.data.targets

df = X.copy()
df['Revenue'] = y

print(df.head())
print(online_data.metadata)
print(online_data.variables)
```

---

## 6. Exploratory Data Analysis (EDA)
Below are Python visualizations to explore key dataset characteristics.

### 6.1 Class Distribution
```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.countplot(x='Revenue', data=df)
plt.title("Purchase vs No Purchase Distribution")
plt.show()
```

### 6.2 Correlation Heatmap (Numerical Features)
```python
plt.figure(figsize=(12,7))
sns.heatmap(df.corr(numeric_only=True), annot=True, cmap='coolwarm')
plt.title("Correlation Matrix of Numerical Features")
plt.show()
```

### 6.3 Distribution of Page Interactions
```python
page_features = ['Administrative', 'Informational', 'ProductRelated']
df[page_features].hist(bins=20, figsize=(10,5))
plt.suptitle("Distribution of Page Visit Types")
plt.show()
```

### 6.4 Bounce Rate vs Exit Rate
```python
sns.scatterplot(data=df, x='BounceRates', y='ExitRates', hue='Revenue')
plt.title("Bounce vs Exit Rates by Purchase Intention")
plt.show()
```

### 6.5 Page Values by Revenue Category
```python
sns.boxplot(data=df, x='Revenue', y='PageValues')
plt.title("Page Values Distribution Depending on Purchase Outcome")
plt.show()
```

### 6.6 Monthly Purchase Trends
```python
df.groupby('Month')['Revenue'].mean().plot(kind='bar', figsize=(10,5))
plt.title("Average Purchase Probability by Month")
plt.ylabel("Purchase Rate")
plt.show()
```

---

## 7. Preparing the Dataset for Machine Learning
```python
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline

# Identify categorical and numerical columns
num_cols = X.select_dtypes(include=['int64','float64']).columns
cat_cols = X.select_dtypes(include=['object']).columns

# Preprocessing pipeline
tf = ColumnTransformer([
    ('num', StandardScaler(), num_cols),
    ('cat', OneHotEncoder(handle_unknown='ignore'), cat_cols)
])

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
```

---

## 8. Basic Machine Learning Models
### Logistic Regression
```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report

model = Pipeline([
    ('prep', tf),
    ('clf', LogisticRegression(max_iter=200))
])

model.fit(X_train, y_train)
pred = model.predict(X_test)

print(classification_report(y_test, pred))
```

### Random Forest
```python
from sklearn.ensemble import RandomForestClassifier

rf_model = Pipeline([
    ('prep', tf),
    ('clf', RandomForestClassifier(n_estimators=200))
])

rf_model.fit(X_train, y_train)
pred = rf_model.predict(X_test)

print(classification_report(y_test, pred))
```

---

## 9. Suggested Advanced Analysis
- Time-based behavior modeling
- RNN / LSTM modeling for sequence-based browsing prediction
- Traffic segmentation and clustering
- Feature importance ranking (Permutation Importance / SHAP)
- Conversion funnel analysis

---

## 10. Citation
Sakar, C. & Kastro, Y. (2018). *Online Shoppers Purchasing Intention Dataset* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5F88Q

---

## 11. Conclusion
This Markdown report delivers a **complete, ready-to-use analytical framework**.  
It includes dataset descriptions, variable documentation, Python code for loading and visualizing data, and machine learning pipelines—fully compatible with **Google Colab** and ideal for **GitHub** documentation.

If you want, I can also create:
- A **PDF version**
- A **Jupyter Notebook (.ipynb)**
- A **PowerPoint summary**

