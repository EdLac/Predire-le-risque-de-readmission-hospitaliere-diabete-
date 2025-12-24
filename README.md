# Prédiction du risque de réadmission hospitalière (Diabète)

## 📌 Contexte
Les réadmissions hospitalières précoces représentent un enjeu majeur de santé publique. Elles sont associées à une augmentation des coûts, à une surcharge des établissements de soins et à des risques accrus pour les patients sortis trop tôt.

Dans ce contexte, l’analyse des données hospitalières peut aider à identifier les patients les plus à risque de réadmission afin d’adapter le suivi post-hospitalisation.

---

## 🎯 Objectif du projet
L’objectif de ce projet est de **prédire la probabilité de réadmission hospitalière dans les 30 jours** suivant une hospitalisation pour diabète, à partir de données d’archives hospitalières.

Le projet adopte une **approche orientée prévention**, en privilégiant la détection des patients à risque plutôt que l’optimisation de la précision globale.

---

## 🧠 Problématique data
- Données fortement **déséquilibrées** (les réadmissions précoces sont minoritaires)
- Grand nombre de **variables catégorielles**
- Risque de **faux négatifs** critique dans un contexte médical

---

## 📊 Données
- **Source** : Diabetes 130-US hospitals (1999–2008)
- **Unité d’observation** : une hospitalisation
- **Taille** : plus de 100 000 observations
- Données anonymisées issues de plusieurs hôpitaux américains

### Variable cible
La variable `readmitted` est transformée en variable binaire :
- `1` : réadmission dans les 30 jours
- `0` : sinon

---

## 🛠️ Méthodologie

### 1. Exploration des données (EDA)
- Analyse de la structure du dataset
- Étude de la distribution de la variable cible
- Identification du déséquilibre de classes
- Visualisations exploratoires ciblées

### 2. Nettoyage des données
- Suppression des identifiants non informatifs
- Gestion des valeurs manquantes (`?` → `NaN`)
- Création de la variable cible binaire

### 3. Feature engineering
- Séparation des variables numériques et catégorielles
- Encodage des variables catégorielles via **One-Hot Encoding**
- Utilisation d’un **ColumnTransformer** pour éviter toute fuite de données

### 4. Modélisation
- Modèle baseline : **Régression logistique**
- Pipeline combinant préprocessing et modèle
- Pondération des classes pour gérer le déséquilibre

### 5. Évaluation
- Matrice de confusion
- Precision, Recall, F1-score
- Analyse spécifique de la classe "patients à risque"

### 6. Ajustement du seuil de décision
- Abaissement du seuil de classification à **0.3**
- Objectif : **maximiser le recall** et réduire les faux négatifs
- Approche cohérente avec une logique de prévention médicale

---

## 📈 Résultats clés

- **Recall ≈ 0.92** pour les patients réadmis à moins de 30 jours
- Forte augmentation de la détection des patients à risque
- Compromis assumé : augmentation des faux positifs
- Le modèle privilégie la **sécurité des patients** plutôt que la précision

---

## 🏥 Interprétation métier
Dans un contexte de santé publique, le coût d’un faux négatif (patient à risque non détecté) est bien plus élevé que celui d’un faux positif.  
L’ajustement du seuil de décision permet donc de mieux répondre aux enjeux médicaux et organisationnels.

---

## ⚠️ Limites
- Données anciennes et spécifiques à un contexte hospitalier américain
- Absence de données cliniques détaillées
- Modèle simple servant de baseline
- Le modèle ne constitue **en aucun cas un outil de diagnostic médical**

---

## 🚀 Pistes d’amélioration
- Optimisation du seuil via courbe ROC
- Utilisation de modèles plus complexes (Random Forest, XGBoost)
- Analyse approfondie de l’importance des variables
- Intégration dans un outil d’aide à la décision (dashboard)

---

## 🧪 Technologies utilisées
- Python
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

---

## ▶️ Reproduire le projet
```bash
pip install -r requirements.txt
```
Ouvrir ensuite le notebook principal dans le dossier notebooks/.

👤 Auteur

Édouard LACROIX
