# 📊 **Bank Marketing – Rapport d’Analyse Complet & Détaillé**

## 🏦 1. Introduction Générale

Le dataset **Bank Marketing** provient d’une institution bancaire portugaise et documente les **campagnes de marketing direct basées sur des appels téléphoniques**. L’objectif principal est de déterminer si un client va **souscrire à un dépôt à terme** (`y = yes/no`).

Ce jeu de données est très utilisé dans la recherche, notamment pour :

* les modèles prédictifs,
* le marketing data-driven,
* l’analyse du comportement client,
* les problématiques de déséquilibre de classes.

Ce rapport inclut :

* une **description détaillée des variables**,
* un **chargement automatisé du dataset**,
* une **analyse exploratoire (EDA)** riche en interprétations,
* plusieurs **visualisations**,
* des **insights marketing exploitables**.

---

## 📁 2. Description du Dataset

* **Instances :** 45 211
* **Variables :** 16
* **Type :** Multivariate
* **Tâche :** Classification
* **Sujet :** Marketing & Comportement client
* **Valeurs manquantes :** Aucune

### Structure des données

Les variables couvrent :

* caractéristiques sociodémographiques,
* informations sur les prêts,
* données liées à la dernière campagne d’appel,
* historique des interactions avec la banque.

### Objectif

> **Prédire si un client va souscrire un dépôt à terme (`y`).**

---

## 🧩 3. Dictionnaire des Variables

Voici les variables principales :

| Variable  | Type        | Description                            |
| --------- | ----------- | -------------------------------------- |
| age       | Integer     | Âge du client                          |
| job       | Categorical | Profession                             |
| marital   | Categorical | Situation matrimoniale                 |
| education | Categorical | Niveau d’éducation                     |
| default   | Binary      | Crédit en défaut ?                     |
| balance   | Integer     | Solde moyen annuel                     |
| housing   | Binary      | Crédit immobilier ?                    |
| loan      | Binary      | Crédit personnel ?                     |
| contact   | Categorical | Type de contact (téléphone/cellulaire) |
| day       | Integer     | Jour du dernier appel                  |
| month     | Categorical | Mois du dernier appel                  |
| duration  | Integer     | Durée du dernier appel                 |
| campaign  | Integer     | Nombre d’appels effectués              |
| pdays     | Integer     | Jours depuis le dernier contact        |
| previous  | Integer     | Nombre de contacts antérieurs          |
| poutcome  | Categorical | Résultat de la campagne précédente     |
| y         | Target      | Souscription au dépôt terme            |

---

## 🧪 4. Importation des Données & Préparation

```python
# ============================================================
# BANK MARKETING — Import via ucimlrepo + Graphiques + Analyse
# ============================================================

!pip install ucimlrepo >/dev/null 2>&1

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from ucimlrepo import fetch_ucirepo

sns.set_theme()

# ============================================================
# 1) Importation du dataset
# ============================================================
bank_marketing = fetch_ucirepo(id=222)

X = bank_marketing.data.features
y = bank_marketing.data.targets

df = pd.concat([X, y], axis=1)
```

---

## 🔧 5. Nettoyage & Transformation

```python
# Convertir la cible en binaire
df["y"] = df["y"].map({"yes": 1, "no": 0})

# Séparer numérique / catégorique
num_cols = df.select_dtypes(include=["int64", "float64"]).columns
cat_cols = df.select_dtypes(include=["object"]).columns
```

---

## 📊 6. Analyse Exploratoire (EDA) + Interprétations

### 🔹 A. Distribution de la variable cible

```python
plt.figure(figsize=(6,4))
df["y"].value_counts().plot(kind="bar")
plt.title("Distribution de la variable cible (y)")
plt.xlabel("Souscription (0 = non, 1 = oui)")
plt.ylabel("Nombre de clients")
plt.show()
```

**Interprétation :**
La classe est très déséquilibrée : ~88% de **non-souscription**, ~12% de **souscription**.
➡️ Cela nécessite des techniques comme **SMOTE**, **class_weight='balanced'**, etc.

---

### 🔹 B. Distribution de l'âge

```python
plt.figure(figsize=(7,5))
plt.hist(df["age"], bins=30)
plt.title("Distribution de l'âge des clients")
plt.xlabel("Âge")
plt.ylabel("Fréquence")
plt.show()
```

**Interprétation :**
La majorité des clients ont entre **30 et 55 ans**, avec une légère présence de seniors.
➡️ Le marketing peut adapter ses messages par tranche d’âge.

---

### 🔹 C. Boxplot de l’âge selon la souscription

```python
sns.boxplot(x=df["y"], y=df["age"])
```

**Interprétation :**
Les clients plus âgés montrent une tendance légèrement plus élevée à souscrire.

---

### 🔹 D. Heatmap des corrélations

```python
corr = df[num_cols].corr()
sns.heatmap(corr, cmap="coolwarm", center=0)
```

**Interprétation :**
Le dataset présente de **faibles corrélations linéaires**, ce qui est favorable pour des modèles non linéaires.

---

### 🔹 E. Analyse de la variable clé : durée d’appel

```python
plt.hist(df["duration"], bins=40)
```

**Interprétation essentielle :**

> **Plus l’appel est long, plus il y a de chances que le client souscrive.**
> Cependant, la variable n’est connue *qu’après* l’appel → non utilisable en prédiction en amont.

---

### 🔹 F. Types de professions & Taux de souscription

```python
df["job"].value_counts().plot(kind="bar")
df.groupby("job")["y"].mean().plot(kind="bar")
```

**Interprétation :**

* Les professions les plus représentées : **blue-collar**, **technician**, **management**.
* Les professions avec le meilleur taux de souscription : **student**, **retired**, **management**.

---

## 🧠 7. Insights Business

Voici les conclusions marketing :

### ✔ 1. La durée de l'appel est le meilleur prédicteur

Plus un conseiller reste en ligne, plus le client finit par dire oui.

### ✔ 2. Certains groupes sont plus sensibles

* retraités,
* étudiants,
* professions stables.

### ✔ 3. Les campagnes doivent être ciblées

Segmentation recommandée :

* âge 40–60,
* solde bancaire positif,
* clients déjà contactés auparavant.

### ✔ 4. Les mois influencent les résultats

Les analyses habituelles montrent que **mai**, **août**, **novembre** donnent de meilleurs résultats.

---

## 🏁 8. Conclusion

Ce dataset est un excellent support pour :

* l’analyse comportementale,
* l’apprentissage automatique supervisé,
* l’optimisation des campagnes marketing téléphoniques.

Il démontre que l’interaction humaine (**durée de l’appel**) est un levier clé dans la conversion.

---

## 📚 Références

* Moro, S., Rita, P., & Cortez, P. (2014). *A data-driven approach to predict the success of bank telemarketing*. Decision Support Systems.
* UCI Machine Learning Repository — Bank Marketing Dataset.

---

Souhaites-tu que j’ajoute :
➡️ une partie **modélisation (Logistic Regression, Random Forest, XGBoost)** ?
➡️ une **ACP (PCA)** ?
➡️ une **mise en page plus académique** ?

