# Aide à la commercialisation foncière — Scoring prédictif & cartographie des parcelles

> Projet de fin d'études — Bachelor 3 Intelligence Artificielle & Big Data (KEYCE Informatique)
> Cas d'application : **WISDOM International** (promotion immobilière, Cameroun)

## 🎯 Contexte

WISDOM International commercialise des parcelles de terrain organisées en blocs et en lots,
regroupées par titre foncier (TF). Le suivi des ventes existe sous forme de fichiers Excel et
de plans cadastraux, mais n'est pas exploité analytiquement. L'entreprise ne dispose d'aucun
outil pour anticiper quelles parcelles disponibles se commercialiseront, ni pour visualiser la
dynamique commerciale à l'échelle du lotissement.

**Objectif :** construire un modèle d'apprentissage automatique prédisant le statut de
commercialisation des parcelles, et restituer les résultats sous forme de score par parcelle
et de cartographie décisionnelle.

## 🗂️ Démarche

Le projet suit la chaîne complète d'un projet de data science :

| Phase | Contenu |
|-------|---------|
| **1. Préparation des données** | Extraction et nettoyage d'un classeur Excel de 37 feuilles hétérogènes → base propre de **408 parcelles** |
| **2. Analyse exploratoire (EDA)** | Identification des variables discriminantes : la **localisation** (bloc, lotissement) prime sur la superficie |
| **3. Modélisation** | Régression logistique & Random Forest, évaluation (AUC, F1, matrice de confusion) |
| **4. Contrôle de robustesse** | Validation croisée + test anti-fuite de données |
| **5. Restitution** | Scoring des lots disponibles + cartographie Power BI sur le plan cadastral |

## 🔬 Résultats clés

- **AUC = 0,90** sur un découpage simple (Random Forest), au-dessus du seuil de 0,75 visé.
- **MAIS** : la validation croisée révèle une performance **instable** (AUC moyen ≈ 0,61),
  signe d'un **sur-apprentissage** lié à la structure des données (faible nombre de parcelles
  disponibles, commercialisation par bloc entier).

> 💡 **Le principal apprentissage du projet n'est pas le score, mais le diagnostic.**
> Un modèle qui semble excellent sur un test unique peut masquer un sur-apprentissage.
> Seul un contrôle de robustesse rigoureux permet de le révéler.

## ⚠️ Limites assumées

- Fichier de suivi daté de **2021** (plan cadastral de 2026) → statuts potentiellement obsolètes.
- **Fort déséquilibre** des classes (~88 % vendu / 12 % disponible).
- **Absence de dates** de vente → pas de modélisation du délai.
- **Prix** connus pour 3 blocs seulement → modèle de pricing écarté.

Ces limites sont documentées comme perspectives : un jeu de données enrichi (fichier 2026
complet, dates, prix) permettrait de fiabiliser le modèle et d'ouvrir vers des analyses de
série temporelle ou des modèles hédoniques.

## 🛠️ Stack technique

- **Python** — pandas, scikit-learn, matplotlib, seaborn
- **Jupyter Notebook** — pipeline reproductible
- **Power BI** — tableau de bord décisionnel (Synoptic Panel pour la cartographie)

## 📁 Structure du dépôt

```
├── notebooks/
│   ├── 01_preparation_donnees.ipynb
│   ├── 02_analyse_exploratoire.ipynb
│   └── 03_modelisation.ipynb
├── images/          # graphiques et maquette du dashboard
└── README.md
```

> **Note sur les données :** les fichiers de données réels de l'entreprise ne sont pas
> publiés (confidentialité — données clients). Seuls le code et les résultats agrégés
> sont partagés.

---

*Projet réalisé dans le cadre d'un stage de fin d'études. Les données appartiennent à
WISDOM International et sont utilisées à des fins pédagogiques.*
