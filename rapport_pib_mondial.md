# Rapport d'Analyse Approfondie du PIB Mondial
## Étude Comparative de 12 Économies Majeures (2015-2024)


![Ma photo](images/WIN_20250616_21_00_40_Pro.jpg)

NOUHAILA EN-NAIDI
---

**Auteur:** Service d'Analyse Économique Internationale  
**Date:** 30 octobre 2025  
**Version:** 1.0  
**Classification:** Document Public

---

## Table des Matières

1. [Introduction et Contexte](#1-introduction-et-contexte)
2. [Description du Jeu de Données](#2-description-du-jeu-de-données)
3. [Code Python Commenté](#3-code-python-commenté)
4. [Résultats de l'Analyse](#4-résultats-de-lanalyse)
5. [Visualisations et Graphiques](#5-visualisations-et-graphiques)
6. [Conclusions et Recommandations](#6-conclusions-et-recommandations)

---

## 1. Introduction et Contexte

### 1.1 Objectif de l'Analyse

Cette étude vise à réaliser une analyse comparative approfondie du Produit Intérieur Brut (PIB) de douze économies majeures représentant différentes régions du monde. Les objectifs spécifiques sont:

- **Identifier les tendances économiques** sur une décennie (2015-2024)
- **Comparer les performances** des économies développées et émergentes
- **Évaluer la résilience économique** face aux chocs externes (COVID-19, crises géopolitiques)
- **Analyser les dynamiques de croissance** et leur évolution
- **Fournir des insights** pour la compréhension des déséquilibres économiques mondiaux

### 1.2 Méthodologie Générale Employée

L'analyse s'appuie sur une approche quantitative rigoureuse comprenant:

**Phase 1 : Collecte et Préparation**
- Extraction de données macroéconomiques de sources fiables
- Nettoyage et standardisation des données
- Validation de la cohérence temporelle

**Phase 2 : Analyse Exploratoire**
- Calcul de statistiques descriptives (moyenne, médiane, écart-type)
- Identification de valeurs aberrantes
- Analyse de distribution

**Phase 3 : Analyse Comparative**
- Comparaisons inter-pays et inter-périodes
- Calcul des taux de croissance annuels et cumulés
- Analyse de corrélations et classements

**Phase 4 : Visualisation**
- Création de 6+ graphiques professionnels
- Représentation des tendances temporelles
- Cartographie thermique des performances

**Phase 5 : Interprétation**
- Contextualisation économique
- Identification des facteurs explicatifs
- Formulation de conclusions et recommandations

### 1.3 Pays Sélectionnés et Période d'Analyse

**Pays analysés (12 économies):**

| Pays | Région | Catégorie | Justification |
|------|--------|-----------|---------------|
| États-Unis | Amérique du Nord | Développée | 1ère économie mondiale |
| Chine | Asie-Pacifique | Émergente | 2ème économie mondiale |
| Japon | Asie-Pacifique | Développée | 3ème économie mondiale |
| Allemagne | Europe | Développée | Leader européen |
| Inde | Asie du Sud | Émergente | Croissance rapide |
| Royaume-Uni | Europe | Développée | Post-Brexit |
| France | Europe | Développée | G7 membre |
| Brésil | Amérique du Sud | Émergente | Leader régional |
| Italie | Europe | Développée | G7 membre |
| Canada | Amérique du Nord | Développée | Économie diversifiée |
| Corée du Sud | Asie-Pacifique | Développée | Tigre asiatique |
| Mexique | Amérique du Nord | Émergente | USMCA membre |

**Période d'analyse:** 2015-2024 (10 ans)

### 1.4 Questions de Recherche Principales

1. Quelle est l'évolution du PIB des principales économies mondiales sur la décennie 2015-2024?
2. Quels pays ont connu la croissance la plus rapide et la plus lente?
3. Quel a été l'impact de la pandémie COVID-19 sur les différentes économies?
4. Comment les économies émergentes se comparent-elles aux économies développées?
5. Quelles sont les disparités en termes de PIB par habitant?
6. Existe-t-il des corrélations entre les performances économiques de différentes régions?

---

## 2. Description du Jeu de Données

### 2.1 Source des Données

**Sources primaires:**
- **Fonds Monétaire International (FMI)** - World Economic Outlook Database
- **Banque Mondiale** - World Development Indicators
- **OCDE** - Economic Outlook Statistics

**Fiabilité:** Organismes internationaux reconnus avec méthodologie standardisée
**Date d'extraction:** Octobre 2025

### 2.2 Variables Analysées

| Variable | Unité | Description | Usage |
|----------|-------|-------------|-------|
| PIB Nominal | Milliards USD | Valeur totale de production | Comparaison taille économique |
| PIB par Habitant | USD | PIB / population | Niveau de vie |
| Taux de Croissance | % | Variation annuelle du PIB | Dynamique économique |
| Population | Millions | Nombre d'habitants | Calculs per capita |

### 2.3 Période Couverte

**Années:** 2015-2024 (10 ans)

**Événements marquants:**
- 2015-2019: Croissance stable post-crise 2008
- 2020: Pandémie COVID-19
- 2021: Rebond économique
- 2022-2024: Inflation et stabilisation

### 2.4 Qualité et Limitations des Données

**Points forts:**
- ✓ Couverture de 10 ans
- ✓ Données standardisées
- ✓ 12 pays = 70% du PIB mondial

**Limitations:**
- ⚠ PIB nominal (non ajusté inflation)
- ⚠ Taux de change USD crée distorsions
- ⚠ Économie informelle non captée

### 2.5 Tableau Récapitulatif des Données

**Structure:**
- 12 pays × 10 années
- 0 valeur manquante
- PIB en milliards USD

---

## 3. Code Python Commenté

### 3.1 Importation et Configuration

**Explication:** Nous importons toutes les bibliothèques nécessaires et configurons l'environnement pour des visualisations professionnelles.

```python
# ============================================================================
# SECTION 1: IMPORTATION DES BIBLIOTHÈQUES
# ============================================================================

# Manipulation de données tabulaires
import pandas as pd

# Calculs mathématiques et arrays
import numpy as np

# Visualisations
import matplotlib.pyplot as plt
import seaborn as sns

# Suppression des avertissements
import warnings
warnings.filterwarnings('ignore')

# Configuration de l'affichage pandas
pd.options.display.float_format = '{:,.2f}'.format
pd.set_option('display.max_columns', None)
pd.set_option('display.width', 1000)

print("✓ Bibliothèques importées avec succès")
print(f"✓ Pandas version: {pd.__version__}")
print(f"✓ NumPy version: {np.__version__}")
```

```python
# ============================================================================
# SECTION 2: CONFIGURATION GRAPHIQUE
# ============================================================================

# Style professionnel
plt.style.use('seaborn-v0_8-whitegrid')
sns.set_palette("Set2")

# Paramètres matplotlib pour graphiques de haute qualité
plt.rcParams.update({
    'figure.figsize': (16, 9),      # Format 16:9
    'figure.dpi': 100,              # Résolution affichage
    'savefig.dpi': 300,             # Résolution sauvegarde
    'font.size': 11,
    'axes.labelsize': 12,
    'axes.titlesize': 14,
    'xtick.labelsize': 10,
    'ytick.labelsize': 10,
    'legend.fontsize': 10,
    'figure.titlesize': 16,
    'axes.grid': True,
    'grid.alpha': 0.3,
    'axes.facecolor': '#f8f9fa',
    'figure.facecolor': 'white'
})

print("✓ Configuration graphique appliquée")
```

**Résultat:** Environnement prêt avec style professionnel pour tous les graphiques.

---

### 3.2 Création du Dataset

**Explication:** Nous créons le dataset principal avec les données PIB de 12 pays sur 10 ans.

```python
# ============================================================================
# SECTION 3: CRÉATION DU JEU DE DONNÉES
# ============================================================================

# Dictionnaire contenant PIB nominal en milliards USD
# Source: FMI, Banque Mondiale
pib_donnees = {
    'Pays': [
        'États-Unis', 'Chine', 'Japon', 'Allemagne', 'Inde', 'Royaume-Uni',
        'France', 'Brésil', 'Italie', 'Canada', 'Corée du Sud', 'Mexique'
    ],
    '2015': [18220, 11060, 4390, 3370, 2100, 2930, 2440, 1800, 1820, 1550, 1470, 1170],
    '2016': [18710, 11220, 4950, 3470, 2290, 2700, 2470, 1790, 1860, 1530, 1500, 1080],
    '2017': [19540, 12310, 4870, 3690, 2650, 2690, 2590, 2050, 1960, 1650, 1620, 1150],
    '2018': [20580, 13890, 4971, 3947, 2713, 2855, 2780, 1885, 2073, 1713, 1730, 1220],
    '2019': [21380, 14280, 5082, 3861, 2875, 2830, 2716, 1840, 2004, 1736, 1650, 1260],
    '2020': [20936, 14720, 5048, 3846, 2671, 2710, 2603, 1445, 1886, 1643, 1640, 1076],
    '2021': [23315, 17730, 4937, 4260, 3173, 3108, 2938, 1609, 2107, 1990, 1810, 1290],
    '2022': [25464, 17960, 4231, 4072, 3385, 3070, 2783, 1920, 2010, 2139, 1670, 1410],
    '2023': [27360, 17890, 4210, 4120, 3730, 3330, 2920, 2130, 2190, 2240, 1710, 1570],
    '2024': [28780, 18560, 4350, 4280, 4050, 3520, 3100, 2280, 2310, 2380, 1790, 1680]
}

# Création du DataFrame
df_pib = pd.DataFrame(pib_donnees)

# Affichage du DataFrame
print("\n" + "="*100)
print("DONNÉES DU PIB NOMINAL (en milliards USD)")
print("="*100)
print(df_pib.to_string(index=False))
print("\n")

# Informations sur le dataset
print("Informations sur le dataset:")
print(f"  - Nombre de pays: {len(df_pib)}")
print(f"  - Nombre d'années: {len(df_pib.columns) - 1}")
print(f"  - Valeurs manquantes: {df_pib.isnull().sum().sum()}")
print(f"  - Type de données: {df_pib.iloc[:, 1:].dtypes.unique()[0]}")
```

**Résultat:** DataFrame structuré avec 12 pays et 10 années de données PIB.

---

### 3.3 Ajout des Données Démographiques

**Explication:** Nous ajoutons les populations pour calculer le PIB par habitant.

```python
# ============================================================================
# SECTION 4: AJOUT DES DONNÉES DÉMOGRAPHIQUES
# ============================================================================

# Population en millions d'habitants (2024)
# Source: Banque Mondiale, Nations Unies
population_2024 = {
    'États-Unis': 340,
    'Chine': 1425,
    'Japon': 123,
    'Allemagne': 84,
    'Inde': 1428,
    'Royaume-Uni': 68,
    'France': 68,
    'Brésil': 216,
    'Italie': 59,
    'Canada': 39,
    'Corée du Sud': 52,
    'Mexique': 128
}

# Ajout de la colonne population au DataFrame
df_pib['Population_2024'] = df_pib['Pays'].map(population_2024)

# Calcul du PIB par habitant pour 2024
# Formule: (PIB en milliards × 1000) / Population en millions
df_pib['PIB_par_habitant_2024'] = (df_pib['2024'] * 1000) / df_pib['Population_2024']

# Arrondir à 2 décimales
df_pib['PIB_par_habitant_2024'] = df_pib['PIB_par_habitant_2024'].round(2)

print("\n" + "="*100)
print("PIB PAR HABITANT EN 2024")
print("="*100)
print(df_pib[['Pays', 'Population_2024', '2024', 'PIB_par_habitant_2024']].to_string(index=False))
print("\n")
```

**Résultat:** Nouveau DataFrame enrichi avec population et PIB par habitant.

---

### 3.4 Transformation des Données

**Explication:** Nous transformons le DataFrame du format large au format long pour faciliter l'analyse et la visualisation.

```python
# ============================================================================
# SECTION 5: TRANSFORMATION DES DONNÉES (FORMAT LONG)
# ============================================================================

# Conversion du format large (années en colonnes) au format long (années en lignes)
# Cela facilite les opérations de groupby et les visualisations temporelles
colonnes_annees = [str(annee) for annee in range(2015, 2025)]

df_long = df_pib.melt(
    id_vars=['Pays', 'Population_2024', 'PIB_par_habitant_2024'],
    value_vars=colonnes_annees,
    var_name='Année',
    value_name='PIB'
)

# Conversion de la colonne Année en entier
df_long['Année'] = df_long['Année'].astype(int)

# Tri par pays et année
df_long = df_long.sort_values(['Pays', 'Année']).reset_index(drop=True)

print("\n" + "="*100)
print("DONNÉES AU FORMAT LONG (aperçu des 20 premières lignes)")
print("="*100)
print(df_long.head(20).to_string(index=False))
print(f"\nDimensions: {df_long.shape[0]} lignes × {df_long.shape[1]} colonnes")
print("\n")
```

**Résultat:** DataFrame transformé avec 120 lignes (12 pays × 10 années).

---

### 3.5 Calcul des Taux de Croissance

**Explication:** Nous calculons les taux de croissance annuels et cumulés pour chaque pays.

```python
# ============================================================================
# SECTION 6: CALCUL DES TAUX DE CROISSANCE
# ============================================================================

# Calcul du taux de croissance annuel pour chaque pays
# Formule: ((PIB_année_n - PIB_année_n-1) / PIB_année_n-1) × 100
df_long['Taux_croissance'] = df_long.groupby('Pays')['PIB'].pct_change() * 100

# Calcul de la croissance cumulée 2015-2024
croissance_cumulee = []

for pays in df_pib['Pays']:
    pib_2015 = df_pib[df_pib['Pays'] == pays]['2015'].values[0]
    pib_2024 = df_pib[df_pib['Pays'] == pays]['2024'].values[0]
    
    # Formule: ((PIB_2024 - PIB_2015) / PIB_2015) × 100
    taux = ((pib_2024 - pib_2015) / pib_2015) * 100
    
    croissance_cumulee.append({
        'Pays': pays,
        'PIB_2015': pib_2015,
        'PIB_2024': pib_2024,
        'Croissance_2015_2024': round(taux, 2)
    })

# Création du DataFrame de croissance
df_croissance = pd.DataFrame(croissance_cumulee)
df_croissance = df_croissance.sort_values('Croissance_2015_2024', ascending=False)

print("\n" + "="*100)
print("TAUX DE CROISSANCE CUMULÉE (2015-2024)")
print("="*100)
print(df_croissance.to_string(index=False))
print("\n")

# Calcul de la croissance annuelle moyenne
df_croissance['Croissance_annuelle_moyenne'] = (
    ((df_croissance['PIB_2024'] / df_croissance['PIB_2015']) ** (1/9) - 1) * 100
).round(2)

print("CROISSANCE ANNUELLE MOYENNE (TCAM):")
print(df_croissance[['Pays', 'Croissance_annuelle_moyenne']].to_string(index=False))
print("\n")
```

**Résultat:** Taux de croissance calculés et classement des pays par performance.

---

## 4. Résultats de l'Analyse

### 4.1 Statistiques Descriptives

**Code pour les statistiques:**

```python
# ============================================================================
# SECTION 7: STATISTIQUES DESCRIPTIVES
# ============================================================================

print("\n" + "="*100)
print("STATISTIQUES DESCRIPTIVES - PIB PAR PAYS (2015-2024)")
print("="*100)

# Calcul des statistiques pour chaque pays
stats_pays = df_long.groupby('Pays')['PIB'].agg([
    ('Moyenne', 'mean'),
    ('Médiane', 'median'),
    ('Minimum', 'min'),
    ('Maximum', 'max'),
    ('Écart-type', 'std'),
    ('Coefficient_variation', lambda x: (x.std() / x.mean()) * 100)
]).round(2)

stats_pays = stats_pays.sort_values('Moyenne', ascending=False)
print(stats_pays)
print("\n")

# Statistiques globales par année
print("="*100)
print("STATISTIQUES GLOBALES PAR ANNÉE")
print("="*100)

stats_annuelles = df_long.groupby('Année')['PIB'].agg([
    ('PIB_total', 'sum'),
    ('PIB_moyen', 'mean'),
    ('PIB_médian', 'median'),
    ('Écart-type', 'std')
]).round(2)

print(stats_annuelles)
print("\n")
```

### 4.2 Classement des Pays

**Classement par PIB 2024:**

| Rang | Pays | PIB 2024 (Mds USD) | Part du Total |
|------|------|-------------------|---------------|
| 1 | États-Unis | 28,780 | 26.9% |
| 2 | Chine | 18,560 | 17.4% |
| 3 | Japon | 4,350 | 4.1% |
| 4 | Allemagne | 4,280 | 4.0% |
| 5 | Inde | 4,050 | 3.8% |
| 6 | Royaume-Uni | 3,520 | 3.3% |
| 7 | France | 3,100 | 2.9% |
| 8 | Canada | 2,380 | 2.2% |
| 9 | Italie | 2,310 | 2.2% |
| 10 | Brésil | 2,280 | 2.1% |
| 11 | Corée du Sud | 1,790 | 1.7% |
| 12 | Mexique | 1,680 | 1.6% |

**Classement par Croissance 2015-2024:**

1. **Inde**: +92.86% (champion de la croissance)
2. **Chine**: +67.83%
3. **États-Unis**: +57.96%
4. **Canada**: +53.55%
5. **Mexique**: +43.59%

**Classement par PIB par Habitant 2024:**

1. **États-Unis**: 84,647 USD
2. **Canada**: 61,026 USD
3. **Allemagne**: 50,952 USD
4. **Royaume-Uni**: 51,765 USD
5. **France**: 45,588 USD

### 4.3 Impact COVID-19 (2020)

**Contractions du PIB en 2020:**

| Pays | Contraction 2020 | Récupération 2021 |
|------|------------------|-------------------|
| Brésil | -21.5% | +11.3% |
| Mexique | -14.6% | +19.9% |
| Royaume-Uni | -4.2% | +14.7% |
| Italie | -5.9% | +11.7% |
| États-Unis | -2.1% | +11.4% |

### 4.4 Corrélations Identifiées

**Observations clés:**
- Corrélation forte entre PIB 2015 et PIB 2024 (r=0.98)
- Les économies développées montrent moins de volatilité
- Les économies émergentes ont une croissance plus rapide mais plus volatile

---

## 5. Visualisations et Graphiques

### 5.1 Graphique 1: Évolution Temporelle du PIB

**Code de génération:**

```python
# ============================================================================
# GRAPHIQUE 1: ÉVOLUTION DU PIB PAR PAYS (2015-2024)
# ============================================================================

plt.figure(figsize=(18, 10))

# Création de couleurs distinctes pour chaque pays
couleurs = plt.cm.tab20(np.linspace(0, 1, 12))

# Tracer une ligne pour chaque pays
for idx, pays in enumerate(df_pib['Pays']):
    # Extraire les valeurs PIB pour ce pays
    valeurs = df_pib[df_pib['Pays'] == pays][colonnes_annees].values[0]
    
    # Tracer la ligne avec marqueurs
    plt.plot(colonnes_annees, valeurs, 
             marker='o',              # Forme des marqueurs
             linewidth=2.5,           # Épaisseur de la ligne
             markersize=8,            # Taille des marqueurs
             label=pays,              # Nom pour la légende
             color=couleurs[idx],     # Couleur unique
             alpha=0.85)              # Transparence

# Configuration du graphique
plt.title('Évolution du PIB par Pays (2015-2024)', 
          fontsize=20, fontweight='bold', pad=20)
plt.xlabel('Année', fontsize=14, fontweight='bold')
plt.ylabel('PIB (milliards USD)', fontsize=14, fontweight='bold')

# Légende optimisée
plt.legend(loc='upper left', 
           fontsize=11, 
           framealpha=0.95,
           ncol=2)          # 2 colonnes pour économiser l'espace

# Grille pour faciliter la lecture
plt.grid(True, alpha=0.3, linestyle='--')

# Rotation des labels de l'axe X
plt.xticks(rotation=45, ha='right')

# Ajustement automatique
plt.tight_layout()

# Sauvegarde en haute résolution
plt.savefig('graphique_1_evolution_pib.png', dpi=300, bbox_inches='tight')

plt.show()

print("✓ Graphique 1 généré: Évolution temporelle du PIB")
```

**Description du graphique:**
Ce graphique en lignes montre l'évolution du PIB de chaque pays sur 10 ans. Les lignes permettent d'identifier facilement les tendances de croissance, les périodes de récession (notamment 2020) et les trajectoires distinctes des économies développées vs émergentes.

---

### 5.2 Graphique 2: Comparaison PIB 2024

**Code de génération:**

```python
# ============================================================================
# GRAPHIQUE 2: COMPARAISON DU PIB EN 2024 (BARRES HORIZONTALES)
# ============================================================================

plt.figure(figsize=(14, 10))

# Tri des données par PIB décroissant
df_2024_sorted = df_pib[['Pays', '2024']].sort_values('2024', ascending=True)

# Création d'un gradient de couleurs
couleurs = plt.cm.viridis(np.linspace(0.2, 0.9, len(df_2024_sorted)))

# Création du graphique en barres horizontales
bars = plt.barh(df_2024_sorted['Pays'], 
                df_2024_sorted['2024'],
                color=couleurs,
                edgecolor='black',
                linewidth=1.5,
                alpha=0.85)

# Ajout des valeurs sur les barres
for bar in bars:
    width = bar.get_width()
    plt.text(width + 500,                    # Position X (légèrement à droite)
             bar.get_y() + bar.get_height()/2,  # Position Y (centre)
             f'{int(width):,}',              # Texte formaté
             ha='left',                      # Alignement horizontal
             va='center',                    # Alignement vertical
             fontsize=11,
             fontweight='bold')

# Configuration
plt.title('Comparaison du PIB des Pays en 2024', 
          fontsize=20, fontweight='bold', pad=20)
plt.xlabel('PIB (milliards USD)', fontsize=14, fontweight='bold')
plt.ylabel('Pays', fontsize=14, fontweight='bold')

# Grille verticale
plt.grid(True, axis='x', alpha=0.3, linestyle='--')

plt.tight_layout()
plt.savefig('graphique_2_comparaison_pib_2024.png', dpi=300, bbox_inches='tight')
plt.show()

print("✓ Graphique 2 généré: Comparaison PIB 2024")
```

**Description du graphique:**
Graphique en barres horizontales montrant le classement des pays par PIB en 2024. La longueur des barres permet une comparaison visuelle immédiate des tailles économiques.

---

### 5.3 Graphique 3: PIB par Habitant

**Code de génération:**

```python
# ============================================================================
# GRAPHIQUE 3: PIB PAR HABITANT 2024 (BARRES VERTICALES)
# ============================================================================

plt.figure(figsize=(16, 10))

# Tri par PIB par habitant décroissant
df_pib_habitant = df_pib[['Pays', 'PIB_par_habitant_2024']].sort_values(
    'PIB_par_habitant_2024', ascending=False
)

# Palette de couleurs selon le niveau (vert = élevé, orange = moyen, rouge = faible)
seuils = [50000, 30000]
couleurs_barres = []

for valeur in df_pib_habitant['PIB_par_habitant_2024']:
    if valeur >= seuils[0]:
        couleurs_barres.append('#2ecc71')  # Vert
    elif valeur >= seuils[1]:
        couleurs_barres.append('#f39c12')  # Orange
    else:
        couleurs_barres.append('#e74c3c')  # Rouge

# Création des barres
bars = plt.bar(df_pib_habitant['Pays'],
               df_pib_habitant['PIB_par_habitant_2024'],
               color=couleurs_barres,
               edgecolor='black',
               linewidth=1.5,
               alpha=0.85,
               width=0.7)

# Ajout des valeurs au-dessus des barres
for bar in bars:
    height = bar.get_height()
    plt.text(bar.get_x() + bar.get_width()/2,
             height + 1000,
             f'${int(height):,}',
             ha='center',
             va='bottom',
             fontsize=10,
             fontweight='bold')

# Ligne de référence (moyenne mondiale)
moyenne = df_pib_habitant['PIB_par_habitant_2024'].mean()
plt.axhline(y=moyenne, color='red', linestyle='--', linewidth=2, 
            label=f'Moyenne: ${int(moyenne):,}', alpha=0.7)

# Configuration
plt.title('PIB par Habitant par Pays en 2024', 
          fontsize=20, fontweight='bold', pad=20)
plt.xlabel('Pays', fontsize=14, fontweight='bold')
plt.ylabel('PIB par Habitant (USD)', fontsize=14, fontweight='bold')

# Rotation des labels
plt.xticks(rotation=45, ha='right', fontsize=11)

# Légende
plt.legend(fontsize=12, loc='upper right')

# Grille horizontale
plt.grid(True, axis='y', alpha=0.3, linestyle='--')

plt.tight_layout()
plt.savefig('graphique_3_pib_par_habitant.png', dpi=300, bbox_
