# 📊 Analyse du Dataset : Global EV Sales (2010-2024)

## Rapport Complet d'Analyse Exploratoire des Données

---

## 📑 Table des Matières

1. [Introduction](#-1-introduction)
2. [Le Dataset](#-2-le-dataset)
3. [Chargement et Exploration](#-3-chargement-et-exploration-initiale)
4. [Nettoyage des Données](#-4-nettoyage-des-données)
5. [Analyse Exploratoire (EDA)](#-5-analyse-exploratoire-des-données)
6. [Modélisation](#-6-préparation-pour-la-modélisation)
7. [Conclusions](#-7-conclusions-et-recommandations)

---

## 🎯 1. Introduction

### Contexte du Projet

Ce projet analyse l'évolution mondiale des **ventes de véhicules électriques (EV)** de 2010 à 2024. L'objectif principal est de comprendre :

- 🌍 La croissance du marché EV mondial
- 📈 Les tendances par région et par pays
- 🔋 L'évolution des types de motorisation (BEV vs PHEV)
- 🎯 Les facteurs influençant l'adoption des véhicules électriques

### Objectifs de l'Analyse

✅ **Analyse descriptive** : Comprendre la structure et l'évolution du marché  
✅ **Analyse comparative** : Identifier les leaders et les tendances régionales  
✅ **Préparation des données** : Nettoyer et structurer pour la modélisation  
✅ **Insights business** : Fournir des recommandations stratégiques  

---

## 📁 2. Le Dataset

### 2.1 Source et Provenance

| Élément | Détail |
|---------|--------|
| **Plateforme** | Kaggle |
| **Nom du dataset** | Global EV Sales 2010-2024 |
| **Auteur** | Patrick L. Ford |
| **Lien** | [Kaggle Dataset](https://www.kaggle.com/datasets/patricklford/global-ev-sales-2010-2024) |
| **Période couverte** | 2010 → 2024 (15 ans) |
| **Thématique** | Mobilité électrique, transition énergétique |
| **Licence** | Open Data |

### 2.2 Définition de la Problématique

Ce dataset permet de répondre à **plusieurs types de problèmes en Machine Learning** :

#### 🔵 **Problème 1 : Régression**
- **Type** : Régression supervisée
- **Variable cible** : `EV_Sales` (nombre de véhicules électriques vendus)
- **Variables explicatives** : Year, Country, Type, Market_Share, etc.
- **Objectif** : Prédire les ventes futures selon différents facteurs
- **Algorithmes applicables** : 
  - Régression Linéaire Multiple
  - Random Forest Regressor
  - XGBoost
  - Gradient Boosting

#### 🟢 **Problème 2 : Séries Temporelles (Time Series Forecasting)**
- **Type** : Prévision temporelle
- **Variable cible** : `EV_Sales` dans le temps
- **Objectif** : Forecasting des ventes pour 2025-2030
- **Algorithmes applicables** :
  - ARIMA / SARIMA
  - Prophet (Facebook)
  - LSTM (Deep Learning)
  - Exponential Smoothing

#### 🟡 **Problème 3 : Clustering (Non-supervisé)**
- **Type** : Segmentation
- **Objectif** : Regrouper les pays selon leurs patterns d'adoption EV
- **Variables** : Taux de croissance, Market Share, EV Stock
- **Algorithmes applicables** :
  - K-Means
  - DBSCAN
  - Clustering Hiérarchique

### 2.3 Métadonnées du Dataset

#### Structure Générale

| Élément | Valeur Estimée |
|---------|----------------|
| **Nombre de lignes** | ~200-500 (selon version) |
| **Nombre de colonnes** | 6-8 variables |
| **Taille mémoire** | < 1 MB |
| **Période** | 2010 → 2024 |
| **Fréquence** | Annuelle |
| **Granularité** | Pays/Région × Année × Type |
| **Unité de mesure** | Nombre de véhicules vendus |

### 2.4 Dictionnaire des Variables

| Variable | Rôle | Type | Description | Exemples | Valeurs Manquantes |
|----------|------|------|-------------|----------|-------------------|
| **year** | Feature | Numérique (int) | Année de référence | 2010, 2015, 2024 | ❌ Non |
| **country** | Feature | Catégorielle | Pays ou région géographique | China, USA, Europe, India | ❌ Non |
| **region** | Feature | Catégorielle | Zone géographique agrégée | Asia, North America, Europe | ⚠️ Possibles |
| **ev_sales** | **Target** | Numérique (int) | Nombre de VE vendus dans l'année | 50000, 1500000 | ⚠️ Possibles |
| **type** | Feature | Catégorielle | Type de motorisation | BEV, PHEV, Total | ❌ Non |
| **market_share** | Feature | Numérique (float) | Part de marché (% du total auto) | 0.05 (5%), 0.18 (18%) | ⚠️ Possibles |
| **ev_stock** | Feature | Numérique (int) | Parc total de VE en circulation | 500000, 10000000 | ⚠️ Possibles |

#### 📖 Glossaire des Types de Véhicules

- **BEV** (Battery Electric Vehicle) : Véhicule 100% électrique à batterie
- **PHEV** (Plug-in Hybrid Electric Vehicle) : Véhicule hybride rechargeable
- **Total** : Somme des BEV + PHEV

---

## 💻 3. Chargement et Exploration Initiale

### 3.1 Installation des Dépendances
```python
