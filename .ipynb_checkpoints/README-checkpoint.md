# elaraMed 🩺

Pipeline end-to-end de Machine Learning et LLM pour l'orientation et le triage des maladies rares musculo-squelettiques et neurologiques.

Projet académique de Data Science — Universiapolis, École Polytechnique d'Agadur, encadré par Pr. Doha Karaouch.

## 📋 Description

elaraMed est un pipeline complet allant du scraping de données médicales jusqu'à un système de recommandation assisté par LLM, permettant d'orienter un patient vers la spécialité médicale la plus pertinente à partir de ses symptômes (HPO).

## 🗂️ Structure du pipeline

### 1. Scraping (`scraping.ipynb`)
- **Orphadata** : parsing du fichier XML `en_product4.xml` (44 Mo) via `ET.parse()`, filtrage par mots-clés musculo-squelettiques → 1 606 maladies extraites (`data_orphanet.csv`)
- **WHO GHO API** : indicateurs liés à la douleur, aux maladies musculo-squelettiques, neurologiques, à l'arthrite, aux os et au handicap (`data_who_indicateurs.csv`, `data_who_stats.csv`)

### 2. Nettoyage (`cleaning.ipynb`)
- Dataset final : 1 606 lignes, 6 colonnes (maladie, orphacode, nb_symptomes, symptomes, source, origine)
- Suppression des doublons sur `orphacode`, normalisation des noms (title case), nettoyage des sources par regex
- Aucune valeur manquante ni doublon détecté dans les données brutes

### 3. Analyse exploratoire (`EDA.ipynb`)
- Dataset simulé de 1 580 maladies réparties sur 6 spécialités (Rhumatologie, Neurologie, Orthopédie, Neurochirurgie, Médecine générale)
- Visualisations : top maladies, répartition par catégorie, distribution de la douleur (KDE), fréquence des symptômes HPO, analyse de sévérité

### 4. Machine Learning (`ML.ipynb`)
- **Modèles** : Random Forest, Complement Naive Bayes, KNN (distance cosinus), XGBoost
- **Features** : TF-IDF sur les termes HPO (300 features, n-grammes 1-2) + one-hot encoding de la zone corporelle + 4 features numériques normalisées
- **Validation** : StratifiedKFold (k=5), métrique F1-weighted
- **Couche LLM (bonus)** : intégration de l'API Claude pour générer un résumé des symptômes, la spécialité recommandée et des conseils pratiques, en français

## 🛠️ Stack technique

- Python (pandas, scikit-learn, XGBoost)
- Web scraping : `xml.etree.ElementTree`, requêtes API REST
- NLP : TF-IDF
- LLM : Claude API (`claude-sonnet-4-20250514`)
- Visualisation : matplotlib, seaborn

## 🚀 Perspectives

- Intégration UMLS / SNOMED CT
- Fine-tuning des modèles
- Support multilingue (FR / EN / AR)
- Déploiement via FastAPI + Streamlit

## 📁 Organisation du repo

```
elaraMed/
├── scraping.ipynb
├── cleaning.ipynb
├── EDA.ipynb
├── ML.ipynb
├── data_orphanet.csv
├── data_who_indicateurs.csv
├── data_who_stats.csv
└── README.md
```

## 👤 Auteure

Kenza Amoura — Étudiante en 4ème année Génie Informatique, spécialité Big Data & IA
Universiapolis — École Polytechnique d'Agadir
s