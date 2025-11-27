# Bank Marketing Dataset — Rapport analytique prêt pour GitHub & Google Colab

## 1. Introduction
Ce document Markdown synthétise l'ensemble de données **Bank Marketing** afin d'être importé sur **GitHub** et exécuté sur **Google Colab**. Il contient : description du jeu de données, tableau des variables, code Python pour charger les données (depuis UCI via `ucimlrepo` ou depuis un fichier local), visualisations EDA, prétraitement et modèles de base.

**But principal :** prédire si un client souscrira un dépôt à terme (variable `y`) après une campagne de télémarketing.

---

## 2. Aperçu du dataset
- **Nom :** Bank Marketing
- **Donated on :** 13/02/2012
- **Instances :** 45 211 (varie selon la version: full / subset)
- **Features :** 16 (jusqu'à 20 dans les versions étendues)
- **Type :** Multivarié
- **Tâches associées :** Classification
- **Types de variables :** Catégoriel, Entier, Numérique
- **Valeur cible :** `y` (yes / no)
- **Missing values :** Non

Versions disponibles :
1. `bank-additional-full.csv` — 41 188 exemples, 20 inputs (mai 2008 — nov 2010)
2. `bank-additional.csv` — 4 119 exemples (10 % aléatoires)
3. `bank-full.csv` — version plus ancienne, 17 inputs
4. `bank.csv` — 10 % exemples de la version 3

---

## 3. Variables clés (résumé)

| Variable | Type | Description |
|----------|------|-------------|
| age | Integer | Âge du client |
| job | Categorical | Type d'emploi |
| marital | Categorical | État civil |
| education | Categorical | Niveau d'éducation |
| default | Binary | A un crédit en défaut ? |
| balance | Numeric | Solde moyen annuel (euros) |
| housing | Binary | Prêt logement ? |
| loan | Binary | Prêt personnel ? |
| contact | Categorical | Type de contact (cellular/telephone) |
| day | Integer | Jour du dernier contact |
| month | Categorical | Mois du dernier contact |
| duration | Numeric | Durée du dernier appel (secondes) |
| campaign | Numeric | Nombre d'appels durant la campagne |
| pdays | Numeric | Jours depuis dernier contact (-1 = pas contacté) |
| previous | Numeric | Nombre de contacts précédents |
| poutcome | Categorical | Résultat campagne précédente |
| y | Binary (Target) | Souscription au dépôt ? (yes/no) |

---

## 4. Charger le dataset

### Option A — Depuis UCI via `ucimlrepo`
```python
!pip install ucimlrepo
from ucimlrepo import fetch_ucirepo

# ID UCI pour Bank Marketing
bank_marketing = fetch_ucirepo(id=222)

# Dataframes pandas
X = bank_marketing.data.features
y = bank_marketing.data.targets

df = X.copy()
df['y'] = y

print(bank_marketing.metadata)
print(bank_marketing.variables)
```

### Option B — Depuis le fichier local uploadé
Tu as fourni le fichier ZIP localement ; utilise le chemin suivant dans Colab/Notebook :

```
/mnt/data/bank+marketing.zip
```

Le code ci‑dessous liste les fichiers contenus dans le ZIP, détecte automatiquement le CSV le plus complet (`bank-additional-full.csv` ou `bank-full.csv`) et le charge avec le bon séparateur (souvent `;` pour ces fichiers).

```python
import pandas as pd
from zipfile import ZipFile
from pathlib import Path

zip_path = Path('/mnt/data/bank+marketing.zip')

with ZipFile(zip_path, 'r') as z:
    print('Fichiers dans le zip:')
    for name in z.namelist():
        print('-', name)
    # Choisir le fichier le plus complet s'il existe
    preferred = None
    for candidate in ['bank-additional-full.csv', 'bank-additional.csv', 'bank-full.csv', 'bank.csv']:
        if candidate in z.namelist():
            preferred = candidate
            break
    if preferred is None:
        # Si les noms ont des dossiers, cherche par suffixe
        for name in z.namelist():
            if name.endswith('bank-additional-full.csv'):
                preferred = name
                break
            if name.endswith('bank-full.csv') and preferred is None:
                preferred = name
    print('\nChargement du fichier choisi:', preferred)
    with z.open(preferred) as f:
        # Ces fichiers utilisent souvent ";" comme séparateur
        df_local = pd.read_csv(f, sep=';')

print(df_local.shape)
print(df_local.head())
```

> **Remarque :** j'ai détecté que tu as uploadé le ZIP sur le chemin **`/mnt/data/bank+marketing.zip`**. Utilise ce chemin dans Colab (ou adapte si tu l'as installé ailleurs).

---

## 5. Exploration et visualisations (Exemples)

### 5.1 Distribution de la cible
```python
import seaborn as sns
import matplotlib.pyplot as plt
sns.countplot(x='y', data=df)
plt.title('Distribution: Souscription oui/non')
plt.show()
```

### 5.2 Répartition de l'âge
```python
sns.histplot(df['age'], bins=30)
plt.title('Répartition des âges')
plt.show()
```

### 5.3 Solde moyen vs Souscription
```python
sns.boxplot(x='y', y='balance', data=df)
plt.ylim(-2000, 20000)
plt.title('Balance par outcome')
plt.show()
```

### 5.4 Durée de l'appel vs Souscription
```python
sns.boxplot(x='y', y='duration', data=df)
plt.title('Durée du dernier appel par outcome')
plt.show()
```

### 5.5 Heatmap : corrélations numériques
```python
plt.figure(figsize=(10,8))
num_cols = df.select_dtypes(include=['int64','float64']).columns
sns.heatmap(df[num_cols].corr(), annot=True, fmt='.2f')
plt.title('Matrice de corrélation')
plt.show()
```

---

## 6. Prétraitement (exemple rapide)
```python
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import OneHotEncoder, StandardScaler
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline

# Séparer X/y si tu as le df complet
X = df.drop(columns=['y'])
y = df['y'].map({'yes':1,'no':0})

cat_cols = X.select_dtypes(include=['object']).columns.tolist()
num_cols = X.select_dtypes(include=['int64','float64']).columns.tolist()

preproc = ColumnTransformer([
    ('num', StandardScaler(), num_cols),
    ('cat', OneHotEncoder(handle_unknown='ignore', sparse=False), cat_cols)
])

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42, stratify=y)
```

---

## 7. Modélisation (exemples)
### 7.1 Logistic Regression
```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report, roc_auc_score

pipe = Pipeline([('pre', preproc), ('clf', LogisticRegression(max_iter=200))])
pipe.fit(X_train, y_train)
pred = pipe.predict(X_test)
print(classification_report(y_test, pred))
print('AUC:', roc_auc_score(y_test, pipe.predict_proba(X_test)[:,1]))
```

### 7.2 Random Forest
```python
from sklearn.ensemble import RandomForestClassifier

rf = Pipeline([('pre', preproc), ('clf', RandomForestClassifier(n_estimators=200))])
rf.fit(X_train, y_train)
print(classification_report(y_test, rf.predict(X_test)))
```

---

## 8. Analyses avancées recommandées
- Traitement des déséquilibres de classes (SMOTE, class weights)
- Sélection de variables & importance (Permutation Importance, SHAP)
- Validation temporelle (si les données ordonnées par date)
- Analyse de coût-bénéfice (ROI) pour différentes stratégies de contact

---

## 9. Références
- Sérgio Moro, P. Cortez, P. Rita. (2014). *A data-driven approach to predict the success of bank telemarketing*. Decision Support Systems.
- Dataset UCI : Bank Marketing

---

## 10. Remarques finales
- Ce Markdown est prêt à être déposé sur GitHub comme `README.md` pour un projet d'analyse.
- Si tu veux que j'ajoute un Notebook `.ipynb` ou une version PDF, je peux générer le code et te fournir le contenu prêt à télécharger.

