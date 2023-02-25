# Projet IAS : Drug Consumption Prediction

## Tâches à effectuer

<!-- TODO : Ajouter / Modifier les tâches
Pour cocher : [x]   -->

- [ ] Explication du projet
- [ ] Data exploration
- [ ] Data cleaning
- [ ] Model

## Présentation du projet (Rendu 1)

Le dataset est nommé Drug consumption (quantified) Data Set.
Link : <https://archive.ics.uci.edu/ml/datasets/Drug+consumption+%28quantified%29>

a) L'objectif est de déterminer si une personne est un consommateur de drogue. On considère une personne comme consommateur si elle a consommé de la drogue lors de l'année en cours. Nous allons commencer par nous concentrer sur la consommation de cannabis.

b) La travail sera une tâche supervisé de classification binaire. On aurait pu faire en multiclasse mais comme il y a une notion d'ordre entre ces classes et pour simplifié ce problème, nous avons choisi de se limiter à une classification binaire.

c) La database archive 1885 personnes interrogées. Pour chaque personne, il y a 12 attributs : l'ID pour référence dans la database, l'age, le genre, l'education, le pays de résidence, l'appartenance ethnique et une mesure de la personnalité selon les critères NEO-FFI-R (neuroticism, extraversion, openness to experience, agreeableness, and conscientiousness), BIS-11 (impulsivity), et ImpSS (sensation seeking).

La database contient 18 problèmes de classification correspondant à 18 drogues. Comme dit précédemment nous allons nous focaliser tout d'abord sur une drogue, le cannabis. Ce choix est expliqué dans la question e).

Tout d'abord il faut noter que les créateurs du dataset ont fait le choix de mettre tous attributs sous forme de réel que ça soit pour les catégories d'âge, le pays de résidence etc et les colonnes n'étaient pas nommées. Nous allons donc devoir nommer les colonnes à la main. Pour les pays nous allons devoir nommer les pays en fonction de la correspondance donnée par les auteurs de la database, pour l'âge par exemple nous n'avons pas encore décidé de comment traiter cela.

On commencera tout d'abord par supprimer la colonne ID.

Les classes existantes de problème dans le dataset sont "Never Used", "Used over a Decade Ago", "Used in Last Decade", "Used in Last Year", "Used in Last Month", "Used in Last Week", et "Used in Last Day".\
On fait le choix de fusionner ces classes : "Never Used", "Used over a Decade Ago", "Used in Last Decade" en une seule classe.
Et "Used in Last Year", "Used in Last Month", "Used in Last Week", et "Used in Last Day" également en une seule classe.

d) Les différents algorithmes possibles pour une classification binaire seraient : SVM, Perceptron, Random Forest, Logistic regression.
On pourra alors tester plusieurs de ces algorithmes et faire un tableau de comparaison.

e) Le point de vigilance se situe principalement dans l'équilibre des données. Concernant le cannabis le nombre de personnes ayant pris ou non du cannabis est plutôt équilibré. Nonobstant un léger rééquilibrage semble nécessaire.\
On remarque un déséquilibre concernant certaines données. Par exemple 90% des données ont été récupérées dans des pays anglophones et plus particulièrement 80% aux USA et au Royaume-Uni.

Concernant la mesure de performance :
La métrique "Balanced Accuracy" semble être une bonne chose pour des données déséquilibrées.
