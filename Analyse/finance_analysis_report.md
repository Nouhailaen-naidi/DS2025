# 📊 **Rapport d'Analyse – Comportement d'Investissement des Particuliers**

> 🔗 **Source des données** : [Kaggle – Finance Data (nitindatta/finance-data)](https://www.kaggle.com/datasets/nitindatta/finance-data)  

---

## 📑 **Sommaire**

1. [Introduction](#introduction)
2. [Description du Dataset](#description-du-dataset)
3. [Objectifs de l'Analyse](#objectifs-de-lanalyse)
4. [Chargement & Préparation des Données](#chargement--préparation-des-données)
5. [Analyse Exploratoire (EDA)](#analyse-exploratoire-eda)
   - 5.1 Répartition par genre et âge
   - 5.2 Avenues d'investissement préférées
   - 5.3 Facteurs influençant les décisions
   - 5.4 Objectifs et durées d'investissement
   - 5.5 Sources d'information
6. [Interprétations & Insights](#interprétations--insights)
7. [Conclusion](#conclusion)

---

## 📘 **Introduction**

Ce rapport analyse un **jeu de données sur les comportements d'investissement de particuliers**, collecté via un questionnaire structuré. Il explore :

- les **préférences d'investissement** (fonds communs, actions, PPF, dépôts fixes, or, etc.),
- les **facteurs clés de décision** (rendement vs risque),
- les **objectifs financiers** (retraite, santé, éducation…),
- les **sources d'information** utilisées (consultants, internet, TV…).

L'objectif est de **comprendre les profils types d'investisseurs**, identifier les leviers de motivation, et proposer des **recommandations marketing ou éducatives** dans le domaine de la finance personnelle.

---

## 📁 **Description du Dataset**

Le fichier `Finance_data (2).csv` contient **40 observations** avec les colonnes suivantes :

| Variable | Description |
|----------|-------------|
| `gender` | Genre du répondant |
| `age` | Âge en années |
| `Investment_Avenues` | Investit-il ou non ? (Yes/No) |
| `Mutual_Funds`, `Equity_Market`, …, `Gold` | Classement (1 = préféré) parmi 8 options d'investissement |
| `Factor` | Facteur principal : *Returns* ou *Risk* |
| `Objective` | Objectif : *Growth*, *Income*, *Capital Appreciation* |
| `Purpose` | But général : *Wealth Creation*, *Savings for Future*, etc. |
| `Duration` | Horizon d'investissement (ex: *1-3 years*) |
| `Invest_Monitor` | Fréquence de suivi du portefeuille |
| `Expect` | Rendement attendu (tranches : *10%-20%*, *20%-30%*, etc.) |
| `Avenue` | Produit ou canal préféré |
| `What are your savings objectives?` | Objectif spécifique (Retraite, Santé, Éducation…) |
| `Reason_Equity`, `Reason_Mutual`, … | Motivations par type d'actif |
| `Source` | Source d'information financière |

> 💡 Ce dataset est **qualitatif + ordinal** : idéal pour l'analyse comportementale, **pas pour la prédiction de prix boursiers**.

---

## 🎯 **Objectifs de l'Analyse**

- Identifier les **profils d'investisseurs dominants**.
- Comprendre les **motivations derrière les choix d'actifs**.
- Évaluer l'**influence du genre, de l'âge et de la source d'info**.
- Proposer des **recommandations personnalisées** (marketing, conseil financier).

---

## 🔧 **Chargement & Préparation des Données**

```python
# ============================================================
# ANALYSE FINANCIÈRE – COMPORTEMENT D'INVESTISSEMENT
# Source : https://www.kaggle.com/datasets/nitindatta/finance-data
# ============================================================

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

sns.set(style="whitegrid")
plt.rcParams['figure.figsize'] = (10, 6)

# Charger le dataset local
df = pd.read_csv("Finance_data (2).csv")

print(f"✅ Données chargées – {df.shape[0]} lignes, {df.shape[1]} colonnes")
df.head()
```

---

## 📊 **Analyse Exploratoire (EDA)**

### 🔹 1. Répartition par genre et âge

```python
fig, ax = plt.subplots(1, 2, figsize=(14, 5))

df['gender'].value_counts().plot(kind='bar', ax=ax[0], color=['#1f77b4', '#ff7f0e'])
ax[0].set_title("Répartition par genre")
ax[0].set_ylabel("Nombre")

df['age'].hist(bins=10, ax=ax[1], color='green', alpha=0.7)
ax[1].set_title("Distribution de l'âge")
ax[1].set_xlabel("Âge")

plt.tight_layout()
plt.show()
```

---

### 🔹 2. Avenues d'investissement les plus populaires

> Classement inversé : 1 → score 8, 2 → 7, …, 8 → 1

```python
avenues = ['Mutual_Funds', 'Equity_Market', 'Debentures', 'Government_Bonds',
           'Fixed_Deposits', 'PPF', 'Gold', 'Stock_Marktet']

scores = {col: (9 - df[col]).sum() for col in avenues}
pd.Series(scores).sort_values(ascending=False).plot(kind='bar', color='steelblue')
plt.title("Popularité des avenues d'investissement")
plt.ylabel("Score total (plus = plus populaire)")
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```

---

### 🔹 3. Facteur principal : Rendement vs Risque

```python
df['Factor'].value_counts().plot(kind='pie', autopct='%1.1f%%', 
                                 colors=['#2ca02c', '#d62728'])
plt.title("Facteur principal dans la décision")
plt.ylabel("")
plt.show()
```

---

### 🔹 4. Objectifs & Durées d'investissement

```python
fig, ax = plt.subplots(1, 2, figsize=(14, 5))

df['Objective'].value_counts().plot(kind='bar', ax=ax[0], color='purple')
ax[0].set_title("Objectifs financiers")
ax[0].tick_params(axis='x', rotation=45)

df['Duration'].value_counts().plot(kind='bar', ax=ax[1], color='orange')
ax[1].set_title("Horizon d'investissement")
ax[1].tick_params(axis='x', rotation=45)

plt.tight_layout()
plt.show()
```

---

### 🔹 5. Sources d'information

```python
df['Source'].value_counts().plot(kind='barh', color='teal')
plt.title("Sources d'information financière")
plt.xlabel("Nombre de répondants")
plt.tight_layout()
plt.show()
```

---

## 💡 **Interprétations & Insights**

### ✅ Profil type
- **Âge** : majoritairement **22–30 ans** → jeunes actifs.
- **Genre** : équilibre presque parfait.
- **Objectif** : *Retirement Plan* (retraite) domine.
- **Horizon** : **1 à 3 ans** pour 60 % → court/moyen terme.

### ✅ Produits préférés
- **PPF** (Public Provident Fund) et **Fixed Deposits** très populaires → **sécurité + avantages fiscaux**.
- **Mutual Funds** et **Equity** suivent → pour la **croissance**.
- **Or** et **Debentures** moins demandés.

### ✅ Facteur clé : **Rendement** (≈75 % des répondants)
- Malgré un horizon court, les investisseurs visent **20–30 % de rendement** → **optimisme ou manque de réalisme**.

### ✅ Sources d'info
- **Financial Consultants** et **Internet** en tête → combinaison **humain + digital**.
- **TV** et **presse** restent présentes, surtout chez les 30+.

> 📌 **Recommandation** : Proposer des **formations sur la gestion du risque** et des **simulateurs de rendement réalistes**.

---

## 🏁 **Conclusion**

Ce dataset révèle un **public jeune, orienté rendement, mais prudent sur le choix des produits**.  
Il cherche **sécurité, fiscalité avantageuse, et diversification**, tout en étant influencé par des **conseillers et le web**.

Ce type d'analyse est précieux pour :
- ✅ Adapter l'**offre de produits financiers**,
- ✅ Cibler les **campagnes de sensibilisation**,
- ✅ Développer des **outils pédagogiques en finance personnelle**.

---

> 📚 **Source officielle citée** :  
> [Kaggle – Finance Data (nitindatta)](https://www.kaggle.com/datasets/nitindatta/finance-data)
