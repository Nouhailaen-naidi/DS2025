# Analyse Complète - ZZAlpha Stock Recommendations Dataset (2012-2014)

[![DOI](https://img.shields.io/badge/DOI-10.24432%2FC59W3S-blue)](https://doi.org/10.24432/C59W3S)
[![Dataset](https://img.shields.io/badge/Source-UCI%20ML%20Repository-orange)](https://archive.ics.uci.edu/dataset/449/machine+learning+based+zzalpha+ltd+stock+recommendations+2012+2014)
[![Python](https://img.shields.io/badge/Python-3.8+-green)](https://www.python.org/)

---

## 📋 Table des matières

1. [Vue d'ensemble du dataset](#vue-densemble-du-dataset)
2. [Métadonnées techniques](#métadonnées-techniques)
3. [Structure et format des données](#structure-et-format-des-données)
4. [Méthodologie ZZAlpha](#méthodologie-zzalpha)
5. [Portefeuilles et critères](#portefeuilles-et-critères)
6. [Code Python pour l'analyse](#code-python-pour-lanalyse)
7. [Analyses statistiques](#analyses-statistiques)
8. [Visualisations](#visualisations)
9. [Résultats attendus](#résultats-attendus)
10. [Limitations et considérations](#limitations-et-considérations)
11. [Références et citations](#références-et-citations)

---

## 📊 Vue d'ensemble du dataset

### Description générale

Le dataset **ZZAlpha Stock Recommendations** contient les recommandations boursières générées par des algorithmes d'apprentissage automatique pour des actions américaines pendant une période de 3 ans (2012-2014). Ces recommandations ont été émises quotidiennement avant l'ouverture des marchés et certifiées numériquement pour garantir leur traçabilité.

### Informations essentielles

| Attribut | Valeur |
|----------|--------|
| **Nom complet** | Machine Learning based ZZAlpha Ltd. Stock Recommendations 2012-2014 |
| **Créateur** | ZZAlpha Ltd. (Tucson, Arizona, USA) |
| **Donateur** | Kevin Pratt (Directeur Scientifique) |
| **Date de donation** | 06 mai 2015 |
| **Période couverte** | 1er janvier 2012 - 31 décembre 2014 |
| **Jours de bourse** | 755 jours |
| **Total d'instances** | 314,080 recommandations |
| **Type de données** | Séries chronologiques séquentielles |
| **Domaine** | Finance quantitative / Trading algorithmique |
| **Tâche ML** | Classification binaire (hausse/baisse) |
| **Format** | Fichiers texte (.txt) compressés (.zip) |

### Contexte scientifique

Ce dataset a été créé dans le cadre d'une recherche publiée à la conférence **ACM KDD 2015** (Knowledge Discovery and Data Mining), l'une des conférences les plus prestigieuses en data science :

> **Pratt, Kevin** (2015). *"Proof Protocol for a Machine Learning Technique Making Longitudinal Predictions in Dynamic Contexts"*

L'objectif était de démontrer la validité d'un protocole de preuve pour les techniques de ML effectuant des prédictions longitudinales dans des contextes dynamiques (marchés financiers).

---

## 🔧 Métadonnées techniques

### Caractéristiques du dataset

| Caractéristique | Détail |
|-----------------|--------|
| **Type de tâche** | Classification (prédiction de variation de prix) |
| **Type de features** | Réel (numériques continues) |
| **Nombre de portefeuilles** | 41 portefeuilles distincts |
| **Tailles de portefeuilles** | 5 tailles : 1, 2, 5, 10, 20 actions |
| **Types de positions** | LONG (achat) et SHORT (vente) |
| **Valeurs manquantes** | Oui (signalées comme "missing") |
| **Horizon de prédiction** | 5 jours de bourse |

### Fichiers disponibles

| Fichier | Taille | Année | Observations |
|---------|--------|-------|--------------|
| `sNewsListWResults2012.zip` | 6.3 MB | 2012 | ~105,000 recommandations |
| `sNewsListWResults2013.zip` | 6.3 MB | 2013 | ~105,000 recommandations |
| `sNewsListWResults2014.zip` | 6.1 MB | 2014 | ~104,000 recommandations |

### Certification et traçabilité

- **Fichiers originaux** : PDF certifiés quotidiennement via **Digistamp** (.p7s)
- **Horodatage** : Certification effectuée au moment de la génération des recommandations
- **Disponibilité** : Fichiers .pdf et .p7s originaux disponibles sur demande (contact : info@zzalpha.com)
- **Modification** : Les résultats (performances) ont été ajoutés **a posteriori** pour faciliter l'analyse

---

## 📁 Structure et format des données

### Format de ligne standard

Chaque ligne du fichier texte suit cette structure :

```
[DATE]_[ID] [PORTFOLIO]_[SIZE]_LONG_SHORT_F.pdf, [POSITION], [STOCK1] [PERF1] = [SELL_PRICE]/[BUY_PRICE], [STOCK2] [PERF2] = [SELL_PRICE]/[BUY_PRICE], ..., Moyenne de [N] = [AVG_PERF]
```

### Exemple réel détaillé

```
4 janvier 2005_006 Big_100_5_LONG_SHORT_F.pdf, L, AA 0,959 = 25,97/27,09, AMAT 0,950 = 14,70/15,46, EBAY 0,930 = 53,33/57,31, PFE 0,995 = 19,84/19,95, UPS 0,980 = 71,72/73,16, Moyenne de 5 = 0,963
```

### Décomposition ligne par ligne

| Élément | Valeur | Signification |
|---------|--------|---------------|
| **Date** | `4 janvier 2005` | Date d'émission de la recommandation |
| **ID** | `006` | Identifiant unique de la recommandation |
| **Portefeuille** | `Big_100` | Portefeuille limité aux 100 plus grandes capitalisations |
| **Taille** | `5` | Nombre d'actions dans cette recommandation |
| **Type** | `LONG_SHORT_F` | Type de stratégie |
| **Position** | `L` | Long (achat) ou S (short/vente) |
| **Actions** | `AA`, `AMAT`, `EBAY`, `PFE`, `UPS` | Symboles boursiers recommandés |
| **Performance** | `0.959`, `0.950`, etc. | Ratio = Prix d'ouverture J+5 / Prix d'ouverture J0 |
| **Prix** | `25.97/27.09` | Prix de vente (J+5) / Prix d'achat (J0) |
| **Moyenne** | `0.963` | Performance moyenne des 5 actions |

### Interprétation des performances

- **Performance > 1.0** : Gain (pour LONG) ou perte (pour SHORT)
- **Performance = 1.0** : Neutre (pas de variation)
- **Performance < 1.0** : Perte (pour LONG) ou gain (pour SHORT)

**Exemple** :
- Action AA : Performance = 0.959 = 25.97 / 27.09
- Perte de **4.1%** sur 5 jours de bourse pour une position LONG
- Gain de **4.1%** si c'était une position SHORT

---

## 🎯 Méthodologie ZZAlpha

### Principe de l'algorithme

L'algorithme ZZAlpha utilise des techniques d'**apprentissage automatique** pour :

1. **Analyser** les données historiques de marché (prix, volumes, etc.)
2. **Identifier** des patterns prédictifs de variations de prix
3. **Générer** des recommandations d'achat (LONG) ou de vente (SHORT)
4. **Évaluer** les performances 5 jours de bourse après l'émission

### Protocole d'évaluation

```
┌─────────────────────────────────────────────────────────────┐
│                    Timeline d'évaluation                     │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  J0 (Jour 0)          J1    J2    J3    J4    J5 (Jour +5) │
│     ▼                                           ▼            │
│  Recommandation                              Évaluation      │
│  émise avant                                 du résultat     │
│  ouverture marché                                            │
│                                                              │
│  Prix d'ouverture J0 ──────────────────► Prix d'ouverture J5│
│                                                              │
│  Performance = Prix J5 / Prix J0                            │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Ajustements nécessaires

⚠️ **Important** : L'évaluation brute doit être ajustée pour :
- **Coûts de transaction** (commissions de courtage)
- **Slippage** (écart entre prix théorique et prix d'exécution)
- **Spread bid-ask** (écart achat-vente)
- **Impact de marché** (pour les gros volumes)
- **Impossibilité d'exécution** (liquidité insuffisante)

### Calcul des prix ajustés

Les prix utilisés dans le dataset sont **ajustés rétroactivement** pour :
- **Splits d'actions** (divisions)
- **Dividendes** versés
- **Fusions/acquisitions**

> 📝 **Note** : Un recalcul avec des données plus récentes peut donner des prix différents, mais les **ratios de performance restent identiques** (à quelques erreurs d'arrondi près).

---

## 💼 Portefeuilles et critères

### Critères de sélection des actions

Toutes les actions recommandées doivent satisfaire ces critères :

| Critère | Seuil | Raison |
|---------|-------|--------|
| **Prix récent** | > 3 USD | Exclure les penny stocks |
| **Volume quotidien moyen** | > 80,000 actions | Assurer la liquidité |
| **Places boursières** | NYSE, NASDAQ, AMEX | Marchés principaux américains |

### Actions exclues

❌ **Penny stocks** : Actions < 3 USD (trop volatiles, manipulation facile)  
❌ **Micro-capitalisations** : Volume insuffisant (< 80k actions/jour)  
❌ **Actions à très bas prix** : Même si grande capitalisation  
❌ **ETF incomplets** : Problèmes de données sur certains portefeuilles

### Types de portefeuilles (41 au total)

Le dataset contient des portefeuilles segmentés par :

1. **Capitalisation boursière** :
   - `Big_100` : 100 plus grandes capitalisations
   - `Big_50` : 50 plus grandes capitalisations
   - Autres segments de capitalisation

2. **Secteurs** :
   - Technologie
   - Santé
   - Finance
   - Industrie
   - Consommation
   - Énergie
   - etc.

3. **Indices** :
   - S&P 500
   - NASDAQ 100
   - Dow Jones
   - Russell 2000

4. **Stratégies spécifiques** :
   - Momentum
   - Value
   - Growth
   - Volatilité

### Tailles de portefeuilles

| Taille | Description | Usage typique |
|--------|-------------|---------------|
| **1 action** | Recommandation unique | Pick individuel haute conviction |
| **2 actions** | Paire | Trading pairs, arbitrage |
| **5 actions** | Mini-portefeuille | Diversification minimale |
| **10 actions** | Portefeuille moyen | Équilibre risque/diversification |
| **20 actions** | Large portefeuille | Diversification maximale |

### Positions

- **LONG (L)** : Recommandation d'achat
  - Pari sur la **hausse** du prix
  - Profit si prix J+5 > prix J0
  - Performance > 1.0 = succès

- **SHORT (S)** : Recommandation de vente à découvert
  - Pari sur la **baisse** du prix
  - Profit si prix J+5 < prix J0
  - Performance < 1.0 = succès

---

## 💻 Code Python pour l'analyse

### 1. Installation des dépendances

```python
# Installation (exécuter une seule fois)
!pip install pandas numpy matplotlib seaborn scipy scikit-learn

# Imports
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime, timedelta
import zipfile
import re
from collections import Counter, defaultdict
from scipy import stats
import warnings
warnings.filterwarnings('ignore')

# Configuration globale
plt.style.use('seaborn-v0_8-darkgrid')
sns.set_palette("husl")
sns.set_context("notebook", font_scale=1.2)
%matplotlib inline

# Configuration des graphiques
plt.rcParams['figure.figsize'] = (16, 10)
plt.rcParams['figure.dpi'] = 100
plt.rcParams['savefig.dpi'] = 300
plt.rcParams['font.size'] = 11
plt.rcParams['axes.titlesize'] = 14
plt.rcParams['axes.labelsize'] = 12
plt.rcParams['xtick.labelsize'] = 10
plt.rcParams['ytick.labelsize'] = 10
plt.rcParams['legend.fontsize'] = 10

print("✓ Environnement configuré avec succès")
```

### 2. Parsing des fichiers ZZAlpha

```python
def parse_zzalpha_line(line):
    """
    Parse une ligne du format ZZAlpha
    
    Format attendu:
    DATE_ID PORTFOLIO_SIZE_TYPE.pdf, POSITION, STOCK1 PERF1 = SELL/BUY, ...
    
    Returns:
        dict avec date, portfolio, size, position, stocks
    """
    try:
        # Nettoyage de la ligne
        line = line.strip()
        if not line or line.startswith('#'):
            return None
        
        # Séparation par virgules
        parts = [p.strip() for p in line.split(',')]
        
        if len(parts) < 3:
            return None
        
        # Extraction date et portfolio
        header = parts[0].split()
        if len(header) < 2:
            return None
            
        date_str = header[0]
        portfolio_info = header[1] if len(header) > 1 else "Unknown"
        
        # Extraction de la taille du portefeuille
        portfolio_parts = portfolio_info.split('_')
        portfolio_name = portfolio_parts[0] if portfolio_parts else "Unknown"
        portfolio_size = int(portfolio_parts[1]) if len(portfolio_parts) > 1 and portfolio_parts[1].isdigit() else 0
        
        # Position (L ou S)
        position = parts[1].strip()
        
        # Extraction des actions et performances
        stocks = []
        for i in range(2, len(parts)):
            part = parts[i].strip()
            
            # Ignorer la ligne de moyenne
            if 'Moyenne' in part or 'Average' in part:
                continue
            
            # Extraction symbol, performance, et prix
            tokens = part.split()
            if len(tokens) >= 2:
                symbol = tokens[0]
                
                try:
                    # Performance
                    perf_str = tokens[1]
                    performance = float(perf_str.replace(',', '.'))
                    
                    # Prix (si disponibles)
                    prices = None
                    if '=' in part and '/' in part:
                        price_part = part.split('=')[1].strip()
                        price_tokens = price_part.split('/')
                        if len(price_tokens) == 2:
                            sell_price = float(price_tokens[0].replace(',', '.'))
                            buy_price = float(price_tokens[1].replace(',', '.'))
                            prices = {'sell': sell_price, 'buy': buy_price}
                    
                    stocks.append({
                        'symbol': symbol,
                        'performance': performance,
                        'prices': prices
                    })
                except (ValueError, IndexError):
                    continue
        
        if not stocks:
            return None
        
        return {
            'date': date_str,
            'portfolio_name': portfolio_name,
            'portfolio_size': portfolio_size,
            'position': position,
            'num_stocks': len(stocks),
            'stocks': stocks
        }
    
    except Exception as e:
        print(f"Erreur de parsing: {e}")
        return None


def load_zzalpha_data(file_path):
    """
    Charge et parse un fichier ZIP ZZAlpha
    
    Args:
        file_path: chemin vers le fichier .zip
    
    Returns:
        DataFrame pandas avec toutes les recommandations
    """
    data = []
    
    try:
        with zipfile.ZipFile(file_path, 'r') as z:
            print(f"Lecture de {file_path}...")
            
            for filename in z.namelist():
                if filename.endswith('.txt'):
                    print(f"  - Fichier: {filename}")
                    
                    with z.open(filename) as f:
                        for line_num, line in enumerate(f, 1):
                            try:
                                decoded_line = line.decode('utf-8', errors='ignore')
                                parsed = parse_zzalpha_line(decoded_line)
                                
                                if parsed:
                                    data.append(parsed)
                                    
                            except Exception as e:
                                if line_num % 1000 == 0:
                                    print(f"    Erreur ligne {line_num}: {e}")
                                continue
        
        print(f"✓ {len(data)} recommandations chargées depuis {file_path}")
        
    except Exception as e:
        print(f"✗ Erreur lors du chargement de {file_path}: {e}")
        return pd.DataFrame()
    
    return pd.DataFrame(data)


# Chargement des 3 années
print("=" * 70)
print("CHARGEMENT DES DONNÉES ZZALPHA")
print("=" * 70)

df_2012 = load_zzalpha_data('sNewsListWResults2012.zip')
df_2013 = load_zzalpha_data('sNewsListWResults2013.zip')
df_2014 = load_zzalpha_data('sNewsListWResults2014.zip')

# Ajout de la colonne année
df_2012['year'] = 2012
df_2013['year'] = 2013
df_2014['year'] = 2014

# Concaténation
df_all = pd.concat([df_2012, df_2013, df_2014], ignore_index=True)

print("\n" + "=" * 70)
print(f"TOTAL: {len(df_all):,} recommandations chargées (2012-2014)")
print("=" * 70)
```

### 3. Préparation des données pour l'analyse

```python
def extract_performances(df):
    """
    Extrait toutes les performances individuelles des actions
    
    Returns:
        DataFrame avec symbol, performance, position, date, year
    """
    records = []
    
    for idx, row in df.iterrows():
        for stock in row['stocks']:
            records.append({
                'date': row['date'],
                'year': row['year'],
                'portfolio_name': row['portfolio_name'],
                'portfolio_size': row['portfolio_size'],
                'position': row['position'],
                'symbol': stock['symbol'],
                'performance': stock['performance'],
                'prices': stock['prices']
            })
    
    return pd.DataFrame(records)


# Extraction des performances
print("Extraction des performances individuelles...")
df_performances = extract_performances(df_all)

print(f"✓ {len(df_performances):,} performances individuelles extraites")
print(f"\nAperçu des données:")
print(df_performances.head(10))

# Conversion de la date
try:
    df_performances['date_parsed'] = pd.to_datetime(df_performances['date'], format='%d %B %Y', errors='coerce')
except:
    print("⚠ Avertissement: Problème de parsing des dates")
    df_performances['date_parsed'] = pd.NaT

# Statistiques rapides
print("\n" + "=" * 70)
print("STATISTIQUES RAPIDES")
print("=" * 70)
print(f"Nombre de symboles uniques: {df_performances['symbol'].nunique():,}")
print(f"Nombre de portefeuilles: {df_performances['portfolio_name'].nunique()}")
print(f"Positions LONG: {(df_performances['position'] == 'L').sum():,}")
print(f"Positions SHORT: {(df_performances['position'] == 'S').sum():,}")
```

---

## 📊 Analyses statistiques

### 4. Statistiques descriptives globales

```python
def compute_global_statistics(df_perf):
    """Calcule les statistiques descriptives globales"""
    
    perfs = df_perf['performance'].values
    
    stats = {
        'Nombre total': len(perfs),
        'Moyenne': np.mean(perfs),
        'Médiane': np.median(perfs),
        'Écart-type': np.std(perfs),
        'Variance': np.var(perfs),
        'Min': np.min(perfs),
        'Max': np.max(perfs),
        'Q1 (25%)': np.percentile(perfs, 25),
        'Q3 (75%)': np.percentile(perfs, 75),
        'IQR': np.percentile(perfs, 75) - np.percentile(perfs, 25),
        'Skewness': stats.skew(perfs),
        'Kurtosis': stats.kurtosis(perfs)
    }
    
    # Taux de réussite
    success_long = (perfs > 1.0).sum()
    success_short = (perfs < 1.0).sum()
    neutral = (perfs == 1.0).sum()
    
    stats['Réussites (>1.0)'] = success_long
    stats['Réussites (<1.0)'] = success_short
    stats['Neutres (=1.0)'] = neutral
    stats['Taux réussite LONG (%)'] = (success_long / len(perfs)) * 100
    stats['Taux réussite SHORT (%)'] = (success_short / len(perfs)) * 100
    
    return stats


# Calcul
global_stats = compute_global_statistics(df_performances)

# Affichage
print("\n" + "=" * 70)
print("STATISTIQUES DESCRIPTIVES GLOBALES")
print("=" * 70)
for key, value in global_stats.items():
    if isinstance(value, float):
        print(f"{key:.<50} {value:>15.6f}")
    else:
        print(f"{key:.<50} {value:>15,}")

print("=" * 70)
```

### 5. Analyse par position (LONG vs SHORT)

```python
def analyze_by_position(df_perf):
    """Analyse comparative LONG vs SHORT"""
    
    long_perfs = df_perf[df_perf['position'] == 'L']['performance'].values
    short_perfs = df_perf[df_perf['position'] == 'S']['performance'].values
    
    results = {
        'LONG': {
            'Nombre': len(long_perfs),
            'Moyenne': np.mean(long_perfs),
            'Médiane': np.median(long_perfs),
            'Écart-type': np.std(long_perfs),
            'Réussites (>1.0)': (long_perfs > 1.0).sum(),
            'Taux de réussite (%)': ((long_perfs > 1.0).sum() / len(long_perfs)) * 100,
            'Gain moyen (%)': (np.mean(long_perfs) - 1.0) * 100,
            'Meilleure perf': np.max(long_perfs),
            'Pire perf': np.min(long_perfs)
        },
        'SHORT': {
            'Nombre': len(short_perfs),
            'Moyenne': np.mean(short_perfs),
            'Médiane': np.median(short_perfs),
            'Écart-type': np.std(short_perfs),
            'Réussites (<1.0)': (short_perfs < 1.0).sum(),
            'Taux de réussite (%)': ((short_perfs < 1.0).sum() / len(short_perfs)) * 100,
            'Gain moyen (%)': (1.0 - np.mean(short_perfs)) * 100,
            'Meilleure perf': np.min(short_perfs),
            'Pire perf': np.max(short_perfs)
        }
    }
    
    # Test statistique (t-test)
    t_stat, p_value = stats.ttest_ind(long_perfs, short_perfs)
    results['t_test'] = {'t_statistic': t_stat, 'p_value': p_value}
    
    return results, long_perfs, short_perfs


# Analyse
position_results, long_perfs, short_perfs = analyze_by_position(df_performances)

print("\n" + "=" * 70)
print("ANALYSE COMPARATIVE: LONG vs SHORT")
print("=" * 70)

for position in ['LONG', 'SHORT']:
    print(f"\n{position}:")
    print("-" * 70)
    for key, value in position_results[position].items():
        if isinstance(value, float):
            print(f"  {key:.<45} {value:>20.6f}")
        else:
            print(f"  {key:.<45} {value:>20,}")

print("\n" + "=" * 70)
print("TEST STATISTIQUE (t-test)")
print("=" * 70)
print(f"t-statistic: {position_results['t_test']['t_statistic']:.6f}")
print(f"p-value: {position_results['t_test']['p_value']:.6e}")
if position_results['t_test']['p_value'] < 0.05:
    print("✓ Différence statistiquement significative (p < 0.05)")
else:
    print("✗ Pas de différence significative (p >= 0.05)")
```

### 6. Analyse temporelle (par année)

```python
def analyze_by_year(df_perf):
    """Analyse des performances par année"""
    
    yearly_stats = {}
    
    for year in [2012, 2013, 2014]:
        year_data = df_perf[df_perf['year'] == year]
        perfs = year_data['performance'].values
        
        yearly_stats[year] = {
            'Nombre': len(perfs),
            'Moyenne': np.mean(perfs),
            'Médiane': np.median(perfs),
            'Écart-type': np.std(perfs),
            'Min': np.min(perfs),
            'Max': np.max(perfs),
            'Réussites (>1.0)': (perfs > 1.0).sum(),
            'Taux réussite (%)': ((perfs > 1.0).sum() / len(perfs)) * 100,
            'Gain moyen (%)': (np.mean(perfs) - 1.0) * 100,
            'Volatilité': np.std(perfs) / np.mean(perfs)  # Coefficient de variation
        }
    
    return yearly_stats


# Analyse
yearly_analysis = analyze_by_year(df_performances)

print("\n" + "=" * 70)
print("ANALYSE TEMPORELLE PAR ANNÉE")
print("=" * 70)

for year in [2012, 2013, 2014]:
    print(f"\n{year}:")
    print("-" * 70)
    for key, value in yearly_analysis[year].items():
        if isinstance(value, float):
            print(f"  {key:.<45} {value:>20.6f}")
        else:
            print(f"  {key:.<45} {value:>20,}")

# Calcul de la tendance
means = [yearly_analysis[y]['Moyenne'] for y in [2012, 2013, 2014]]
years_num = [2012, 2013, 2014]
slope, intercept, r_value, p_value, std_err = stats.linregress(years_num, means)

print("\n" + "=" * 70)
print("TENDANCE TEMPORELLE (Régression linéaire)")
print("=" * 70)
print(f"Pente: {slope:.6f} (variation annuelle moyenne)")
print(f"R²: {r_value**2:.6f}")
print(f"p-value: {p_value:.6e}")
if p_value < 0.05:
    if slope > 0:
        print("✓ Tendance à la hausse statistiquement significative")
    else:
        print("✓ Tendance à la baisse statistiquement significative")
else:
    print("✗ Pas de tendance significative")
```

### 7. Top actions recommandées

```python
def analyze_top_stocks(df_perf, top_n=30):
    """Analyse des actions les plus recommandées"""
    
    # Comptage par symbole
    symbol_counts = df_perf['symbol'].value_counts()
    top_symbols = symbol_counts.head(top_n).index.tolist()
    
    # Statistiques par symbole
    top_stocks_stats = []
    
    for symbol in top_symbols:
        symbol_