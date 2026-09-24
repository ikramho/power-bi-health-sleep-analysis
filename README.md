## Power BI Dashboards for Health and Sleep Analysis

Projet de Data Analyse explorant les liens entre le stress, la qualité du sommeil et divers facteurs de santé et de mode de vie, réalisé avec Power BI et des visuels Python intégrés (analyse de corrélation et clustering).

Réalisé par : MOUSSAOUI Ikram

## Contexte et objectifs

Le stress chronique et le manque de sommeil ont des conséquences importantes sur la santé à long terme. Ce projet vise à :

Identifier les principaux facteurs de stress
Évaluer l'impact du stress sur la qualité du sommeil
Comprendre les conséquences à long terme sur la santé
Proposer, à partir des données, des pistes pour réduire le stress et améliorer le sommeil

**Solution proposée** : utiliser Power BI pour analyser les données de sommeil et de stress, identifier les tendances et corrélations clés, et restituer ces insights via des dashboards interactifs.


## Sources de données

Le projet combine **deux jeux de données** :

| Dataset | Lignes | Colonnes principales |
|---|---:|---|
| **Health and Sleep Statistics** | 100 | User ID, Age, Sleep Quality, Bedtime, Wake-up Time, Daily Steps, Calories Burned, Physical Activity Level, Dietary Habits, Sleep Disorders, Medication Usage |
| **Sleep Health and Lifestyle Dataset** | 400 | Gender, Age, Occupation, Sleep Duration, Quality of Sleep, Physical Activity Level, Stress Level, BMI Category, Blood Pressure, Heart Rate, Daily Steps, Sleep Disorder |

## Préparation des données (Data Preprocessing)

### Suppression des colonnes inutiles

- **Sleep Health and Lifestyle Dataset** : `Blood Pressure`
- **Health and Sleep Statistics** : `Bedtime`, `Wake-up Time`, `Calories Burned`, `Dietary Habits`, `Medication Usage`

### Standardisation des noms de colonnes

Harmonisation des noms de colonnes entre les deux datasets :

- `User ID` → `Person ID`
- `Quality of Sleep` → `Sleep Quality`
- `Sleep Disorders` → `Sleep Disorder`

### Normalisation des valeurs textuelles

- **BMI Category** : `Normal Weight` → `Normal`
- **Sleep Disorder** : `Sleep Apnea`, `Insomnia` → `Yes / No`
- **Physical Activity Level** (min/jour) → `Low / Medium / High`
- **Gender** : `F / M` → `Female / Male`

### Regroupement en catégories — tranches d'âge

- `20-29` : < 30 ans
- `30-39` : < 40 ans
- `40-49` : < 50 ans
- `50-59` : < 60 ans
- `60+` : ≥ 60 ans

### Conversion des types de données

- **Sleep Duration** : texte → nombre flottant
- Cette conversion permet d'effectuer des analyses numériques.
## Modèle de données (Star Schema)

Les deux datasets ont été fusionnés et structurés en **schéma en étoile** : une table de faits centrale (Fact) reliée à des tables de dimensions pour les attributs catégoriels.

### Table de faits (Fact)

La table de faits contient :

- `Person ID`
- `Heart Rate`
- `Sleep Duration`
- `Sleep Quality`
- `Stress Level`
- Les clés étrangères vers les tables de dimensions

###  Tables de dimensions

- `Gender_DIM`
- `Age_Category_DIM`
- `Occupation_DIM`
- `BMI_Category_DIM`
- `Physical_Activity_DIM`
- `Sleep_Disorder_DIM`
## Contenu du rapport Power BI (4 pages)
### 1. Dataset Description

Vue d'ensemble de la population étudiée à travers :

- la répartition par genre ;
- la profession ;
- la catégorie d'IMC ;
- la présence de troubles du sommeil ;
- la tranche d'âge.

Les données sont présentées à l'aide de graphiques en donut et de graphiques en colonnes.

### 2. Correlations

- **Matrice de corrélation** sous forme de heatmap réalisée avec Python / Seaborn, entre :
  - Stress Level
  - Sleep Quality
  - Sleep Duration
  - Heart Rate
  - Daily Steps
- **Nuage de points** : Stress Level vs Sleep Quality
- **Nuage de points** : Sleep Quality vs Daily Steps

**Principaux constats :**

- forte corrélation négative entre le **stress et la qualité du sommeil** : `-0.87`
- forte corrélation négative entre le **stress et la durée du sommeil** : `-0.83`
- forte corrélation positive entre la **qualité et la durée du sommeil** : `0.88`

### 3. Stress and Categories

Analyse du niveau de stress moyen selon différentes catégories :

- genre ;
- profession ;
- niveau d'activité physique ;
- tranche d'âge ;
- présence ou absence de trouble du sommeil.

### 4. Clustering

Segmentation des individus en 3 profils via K-Means (Stress Level, Sleep Duration, Sleep Quality, Heart Rate, Daily Steps, BMI, Activity Level, Sleep Disorder) :

| Cluster | Profil | IMC dominant | Activité dominante |
|---|---|---|---|
| 1 | À risque | Overweight | Medium |
| 2 | Stable | Normal | High |
| 3 | Intermédiaire | Normal | Low |
## Outils et bibliothèques
- **Power BI Desktop** — modélisation et création de dashboards
- **Python (visuels intégrés)** :
  - **pandas** — manipulation et analyse des données
  - **seaborn / matplotlib** — visualisation des données (heatmaps, graphiques)
  - **scikit-learn** — `LabelEncoder`, `StandardScaler` et `KMeans` pour le clustering
## Structure du dépôt
```text
Projet_DS53/
├── projet_ds53.pbix
│   └── Fichier Power BI complet (rapport + modèle de données)
├── Presentation_DS53.pdf
│   └── Support de présentation du projet
└── README.md
    └── Documentation du projet
```
## Utilisation
Cloner ce dépôt
Ouvrir le fichier .pbix avec Power BI Desktop
Activer l'exécution des scripts Python dans Power BI (Fichier > Options > Options du script Python) pour afficher les visuels Python (heatmap, clustering)
## Prérequis
Power BI Desktop
Python installé localement avec : pandas, seaborn, matplotlib, scikit-learn
## Solutions proposées

À partir des analyses menées (corrélations, comparaisons par catégorie, clustering), voici les principales pistes d'action qui se dégagent des données :

**1. Agir sur l'activité physique** Le cluster "Stable" (faible stress, bon sommeil) est associé à un niveau d'activité physique "High", alors que le cluster "À risque" n'a qu'une activité "Medium". → Encourager une activité physique régulière et plus intense est le levier le plus directement soutenu par les données.

**2. Prioriser la qualité et la durée du sommeil** La corrélation très forte entre stress et qualité de sommeil (-0.87) et entre stress et durée de sommeil (-0.83) montre que toute amélioration du sommeil (routine de coucher régulière, réduction des écrans le soir, environnement propice) devrait avoir un effet direct sur la baisse du stress.

**3. Cibler les professions et tranches d'âge les plus exposées** Le dashboard "Stress and Categories" identifie les professions (ex. Sales Representative, Salesperson, Scientist) et la tranche d'âge (20-29 ans) avec le stress moyen le plus élevé. → Des actions de prévention (sensibilisation, aménagement du temps de travail, accès à des ressources de gestion du stress) pourraient être priorisées pour ces groupes.

**4. Surveiller le poids/IMC comme indicateur associé** Le cluster "À risque" est associé à un IMC "Overweight", contrairement aux clusters plus stables (IMC "Normal"). → Le suivi du poids peut servir d'indicateur complémentaire dans une démarche de prévention du stress chronique.

**5. Utiliser le clustering comme outil de segmentation préventive** Le modèle K-Means permet de classer un individu dans un profil ("À risque", "Stable", "Intermédiaire") à partir de quelques mesures simples (stress, sommeil, fréquence cardiaque, activité, IMC). → Ce modèle pourrait être réutilisé comme outil de dépistage rapide pour orienter les personnes vers des recommandations personnalisées.

## Conclusion

L'analyse confirme un lien fort entre stress et qualité/durée du sommeil, avec des variations notables selon la profession, le niveau d'activité physique et la tranche d'âge. Le clustering permet d'identifier des profils types utiles pour cibler des actions de prévention (ex. population "à risque" avec stress élevé et activité physique modérée).

## Auteurs
MOUSSAOUI Ikram

