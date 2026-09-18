# 🏎️ Formula 1 Winners Prediction (2014 - 2021)

Un projet de Data Science et Machine Learning visant à prédire les vainqueurs des Grands Prix de Formule 1 durant l'ère hybride V6 Turbo (2014-2021) à partir de données issues d'API officielles et de scraping web.

---

## 📌 Présentation du Projet

Prédire le vainqueur d'une course de F1 représente un défi complexe en raison du faible taux d'événements positifs (un seul vainqueur par course parmi 20 pilotes, soit 5 % de la grille) et de l'impact déterminant des qualifications et des performances récentes des écuries.

Ce projet couvre l'intégralité du pipeline de Data Science :
1. **Extraction de données** via l'API Ergast, la librairie `FastF1` et du scraping sur `Formula1.com`.
2. **Nettoyage et Feature Engineering** (calcul des écarts en qualifications, encodage des écuries et calcul de moyennes glissantes).
3. **Modélisation & Évaluation** à l'aide d'algorithmes de classification (Random Forest, Gradient Boosting, CatBoost, XGBoost, AdaBoost).

---

## 📊 Sources des Données

* **[Ergast F1 API](http://ergast.com/mrd/)** : Résultats des courses, classements pilotes/constructeurs et informations sur les circuits.
* **[FastF1 Python Library](https://github.com/theOdev/FastF1)** : Télémétrie et données de sessions F1.
* **Scraping Formula1.com** : Grilles de départ et temps officiels des séances de qualifications.

---

## 🛠️ Feature Engineering

Afin de nourrir les modèles avec des variables prédictives avant le départ de la course, les caractéristiques suivantes ont été construites :

* **`grid`** : Position du pilote sur la grille de départ.
* **`quali_gap`** : Écart de temps en qualifications par rapport au poleman (en secondes).
* **`Top Team`** : Indicateur binaire désignant les écuries majeures de l'ère hybride (Mercedes, Red Bull, Ferrari).
* **`driver_points` & `driver_wins`** : Points et victoires cumulés avant le GP.
* **Moyennes glissantes (`rolling_mean`)** : Moyenne sur les 3 dernières courses pour capturer la forme récente du pilote et de la voiture (`grid_rolling`, `quali_gap_rolling`, `rank_rolling`).

---

## 🚀 Modèles et Résultats

Les données ont été séparées temporellement : 
* **Train Set** : Saisons 2014 à 2020
* **Test Set** : Saison 2021

### Performances des modèles (sur le jeu de test 2021)

| Modèle | Accuracy globale | Precision (Classe Vainqueur) | F1-Score |
| :--- | :---: | :---: | :---: |
| **CatBoost (Tuned)** | **96.6%** | **0.69** | **0.63** |
| Random Forest | 96.6% | 0.52 | 0.54 |
| Gradient Boosting | 95.2% | 0.50 | 0.52 |
| XGBoost | 93.8% | 0.45 | 0.48 |

> **Note sur la métrique** : L'Accuracy globale est naturellement élevée (~95%) du fait du déséquilibre de classe (95% des lignes représentent des non-vainqueurs). Le **F1-score** et la **Précision** sur la classe `1` sont donc les métriques retenues pour évaluer la capacité réelle du modèle à désigner le gagnant.

---

## ⚙️ Installation et Utilisation

### Prerequisites
* Python 3.8+
* Jupyter Notebook / JupyterLab

### Installation
1. Cloner le dépôt :
   ```bash
   git clone [https://github.com/AlexandreBurhan/Formula-1-Winners-prediction.git](https://github.com/AlexandreBurhan/Formula-1-Winners-prediction.git)
   cd Formula-1-Winners-prediction
