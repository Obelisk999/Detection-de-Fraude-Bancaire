# 🔐 Application Streamlit - Détection de Fraude Bancaire

Application interactive pour détecter les transactions frauduleuses en utilisant des modèles de détection d'anomalies non supervisés.

## 📋 Prérequis

- Python 3.8+
- pip (gestionnaire de paquets Python)

## 🚀 Installation et Démarrage

### 1. Installer les dépendances

```bash
pip install -r requirements.txt
```

### 2. Entraîner les modèles (une seule fois)

```bash
python train_models.py
```

Ce script va :
- Charger le dataset `creditcard.csv`
- Entraîner les 3 modèles (Isolation Forest, One-Class SVM, LOF)
- Sauvegarder les modèles dans `trained_models.pkl`
- Sauvegarder les données de test dans `test_data.pkl`

### 3. Lancer l'application Streamlit

```bash
streamlit run app.py
```

L'application ouvrira automatiquement dans votre navigateur à `http://localhost:8501`

## 📊 Fonctionnalités de l'Application

### 1. Tableau de Bord 📊
- Informations générales sur les modèles
- Descriptions et avantages de chaque algorithme
- Statistiques du dataset

### 2. Prédictions 🔍
- **Saisie manuelle**: Entrer les valeurs des features et prédire
- **Fichier CSV**: Importer un fichier CSV avec plusieurs transactions
- **Exemple aléatoire**: Tester sur des exemples du dataset de test

Sélectionnez le modèle à utiliser :
- 🌳 **Isolation Forest** (Recommandé)
- 🎯 **One-Class SVM** (Bonne alternative)
- 📍 **Local Outlier Factor** (Alternative exploratoire)

### 3. Évaluation des Modèles 📈
- **Comparaison des métriques**: Précision, Rappel, F1-Score, AUC-ROC
- **Courbes ROC**: Visualisation graphique des performances
- **Matrices de Confusion**: Analyse détaillée des prédictions
- **Rapports de Classification**: Métriques détaillées par classe

### 4. À Propos ℹ️
- Informations sur le projet
- Description des modèles utilisés
- Technologies et ressources

## 🎯 Modèles Utilisés

### Isolation Forest ⭐⭐⭐⭐⭐
- **Principe**: Isole les anomalies par coupes aléatoires
- **Avantages**: Rapide, efficace en haute dimension
- **Recommandation**: Meilleur choix pour ce problème

### One-Class SVM ⭐⭐⭐⭐
- **Principe**: Trouve une frontière englobant les données normales
- **Avantages**: Bon rappel, efficace en haute dimension
- **Recommandation**: Bonne alternative

### Local Outlier Factor ⭐⭐
- **Principe**: Mesure la densité locale
- **Avantages**: Adaptatif aux variations locales
- **Recommandation**: Performances limitées (features PCA)

## 📊 Structure des Fichiers

```
.
├── app.py                    # Application Streamlit principale
├── train_models.py           # Script d'entraînement des modèles
├── requirements.txt          # Dépendances Python
├── creditcard.csv            # Dataset original
├── trained_models.pkl        # Modèles entraînés (généré)
├── test_data.pkl             # Données de test (généré)
├── resultats_modeles.csv     # Résultats des modèles
└── analyse_fraude_bancaire.ipynb  # Notebook d'analyse
```

## 💡 Utilisation

### Exemple 1: Prédiction Manuelle
1. Allez dans l'onglet "Prédictions"
2. Sélectionnez "Saisie manuelle"
3. Entrez les valeurs des features
4. Cliquez sur "Analyser la transaction"
5. Consultez le résultat et le score d'anomalie

### Exemple 2: Prédiction par Fichier
1. Allez dans l'onglet "Prédictions"
2. Sélectionnez "Fichier CSV"
3. Importez un fichier CSV avec les mêmes colonnes que le dataset original
4. Cliquez sur "Analyser les transactions"
5. Téléchargez les résultats

### Exemple 3: Évaluation des Modèles
1. Allez dans l'onglet "Évaluation des Modèles"
2. Consultez les métriques de comparaison
3. Analysez les courbes ROC
4. Explorez les matrices de confusion

## 📈 Métriques Clés

- **Précision**: Proportion de fraudes correctement identifiées
  - Formule: TP / (TP + FP)
  
- **Rappel (Recall)**: Proportion de fraudes réelles détectées
  - Formule: TP / (TP + FN)
  - ⚠️ **Métrique critique** pour la détection de fraude
  
- **F1-Score**: Équilibre entre précision et rappel
  - Formule: 2 * (Précision * Rappel) / (Précision + Rappel)
  
- **AUC-ROC**: Aire sous la courbe ROC (0 à 1)
  - Plus proche de 1 = meilleur modèle

## 🔍 Interprétation des Résultats

### Score d'Anomalie
- **Bas** (proche de 0): Transaction normale, peu de risque
- **Moyen** (0.1 à 1): Transaction suspecte, à surveiller
- **Haut** (> 1): Transaction anormale, risque de fraude

### Recommandations
1. **Privilégier le Rappel** plutôt que la Précision
   - Les faux négatifs coûtent plus cher que les faux positifs
   
2. **Utiliser Isolation Forest**
   - Meilleure performance sur ce dataset
   
3. **Combine les modèles** pour une meilleure robustesse
   - Voter majoritaire ou moyenne des scores

## 🛠️ Dépannage

### Erreur: "Les modèles n'ont pas été trouvés"
- Exécutez `python train_models.py` d'abord

### Erreur: "Module 'streamlit' not found"
- Installez les dépendances: `pip install -r requirements.txt`

### Lenteur de l'application
- Les prédictions sont cachées en mémoire (cache Streamlit)
- La première exécution sera plus lente

## 📚 Ressources

- [Streamlit Documentation](https://docs.streamlit.io/)
- [Scikit-learn](https://scikit-learn.org/)
- [Kaggle: Credit Card Fraud Detection](https://www.kaggle.com/mlg-ulb/creditcardfraud)

## 📝 Notes Importantes

- Le dataset est fortement déséquilibré (~0.17% de fraudes)
- Les modèles sont non supervisés (pas besoin de labels en entraînement)
- Les labels sont utilisés uniquement pour l'évaluation
- Les features V1-V28 sont le résultat d'une analyse PCA

## ✅ Checklist de Démarrage

- [ ] Installer Python 3.8+
- [ ] `pip install -r requirements.txt`
- [ ] `python train_models.py`
- [ ] `streamlit run app.py`
- [ ] Accéder à `http://localhost:8501` dans le navigateur

## 📞 Support

Pour plus d'informations, consultez :
- Le notebook d'analyse: `analyse_fraude_bancaire.ipynb`
- Le PDF du projet: `Projet intelligence artificielle.pdf`
