# Fall-detection-using-Machine-Learning
Détection des chutes à l’aide des algorithmes de Machine Learning

## 1- Objectif et méthodologie du travail
L’objectif de ce projet est d’étudier la performance de plusieurs algorithmes de machines learning à détecter
automatiquement les chutes grâce aux indicateurs fournis.
Pour ce faire nous allons suivre les étapes suivantes en utilisant la programmation Python :
### a) Entraîner et tester différents classificateurs binaires de machine learnig à utiliser, à savoir :
### I- Naive Bayes II- LDA III- QDA IV- Logistic regression V- KNN VI- Decison Tree VII- Random Forest VIIIAdaboost
XI- Gradient boosting.
### b) Comparer ces classificateurs pour détecter automatiquement les chutes.
### c) Tirer des conclusions sur les performances et les modèles utilisés.
## 2- Description du jeu de données
La base de données a été constituée à partir d’acquisitions de 28 volontaires simulant des chutes et d’autres
comportements.
Le jeu de données ***’falldataproject.csv’*** contient un échantillon d’observations caractérisant la marche puis la chute
(ou non) de plusieurs personnes. La marche est décrite grâce à 87 indicateurs et l’indicateur de chute (ou non)
est décrit par une étiquette binaire. Les variables correspondent à plusieurs indicateurs calculés sur les signaux
bruts ou sur le signal dérivé ou sur l’énergie des signaux (ff signifie Fast Fourier), signaux (fft signifie Fast Fourier
Transform). Pour des raisons de confidentialité, toutes les variables (sauf le label) ont été mises à l’échelle et le
nom des variables a été tronqué.

Il y a 202 falls pour 2619 marches normales. Il n’y a pas de données manquantes, mais le dataset n’est pas équilibré,
c’est pourcela on a essayé d’utiliser SMOTE2 pour équilibrer nos données. Ensuite nous avons essayé de detecter
les chutes en utilisant les méthodes vues en classe.
## Préparation des données
On note X les variables explicatives et Y la variables target, à expliquer qui est la variable ’FALL’ du dataset. On
prend pas la variable ’obs’ car elle correspond juste à un index pour les données.
Les données étant déséquilibrer on a creer un fonction qui permettrait d’oversample la classe minoritaire afin
d’avoir un peut plus d’exemple de ce classe. Cette fonction se base sur SMOTE qui est une excellente technique
d’oversampling.
Nous avons divisé notre base de données en 75% pour l’entrainement (X_train_originel, Y_train_originel) et 25%
pour le test (X_test_originel, Y_test_originel).
Dans la suite de document, on présentera les résultats obtenues sur un jeu de données de train réequilibré.

## 3- Les algorithmes de machines learning utilisés et comparaison des résultats

**Naive Bayes- Classificateur naif de Bayes** -- **LDA: Analyse discriminante linéaire** -- **QDA: Analyse discriminante quadratique** -- **Logistic regression** --
**KNN- K plus proche voisins** -- **Decision Tree- Arbre de décision** -- **Random Forest- Forêt aléatoire** -- **AdaBoost** -- **Gradient Boosting** 

### Comparaison des performances des algorithmes
Pour la comparaison des algorithmes, on s’est basé sur 5 métriques, principalement : accuracy, précision, recall,
f1 et AUC(Area Under the Curve). Au vu de la nature du problème et du jeu de données, les métriques les
plus importantes sont le recall et la précision. Elles sont très importantes, de très bons indicateurs de performance
pour nos algorithmes. Car plus le recall donne une mesure de la précision avec laquelle nos modèles identifient les
vrais chutes tandis que la précision (rapport des vrais positif sur tous les positifs) est plus elle est haute, moins le
modèle se trompe sur ce qu’est réellement une chute.
Dans un permier temps, on a entrainé les différents algorithmes sur les données d’entrainement puis on a évalué
leurs performances sur les données de test sans faire de recherche d’hyerparamètres.

Cette approche n’étant pas assez robuste, il est difficile de généraliser ces modèles entrainés pour la prédiction
car la division de dataset peut fortement biaiser nos modèles. Ainsi, à l’aide d’un gridsearch, on a réalisé une
recherche des meileurs hyperparamètres (les plus importants) pour KNN, Decision Tree, Random Forest, Adaboost
et Gradient Boosting, puis évaluer la performance des modèles en faisant un k-folds (avec k = 10) sur les données
d’entrainements.
La recherche d’hyperparamètres nécessitant une métrique à maximiser. On a choisi le recall car on veut un algorithme
capable de bien détecter les chutes. Aussi pour la grille de recherche de ces hyperparamètres on s’est basé
sur des valeurs empiriques tout en essayant de ne pas avoir des temps de calculs trop longs. Ainsi quelques modèles
finaux sont: KNN (K = 1), Adaboost (n_estimator = 81, learning_rate=0.1), Gradient Boosting (n_estimators
= 105, learning_rate = 0.3).
