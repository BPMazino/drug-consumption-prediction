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

b) La travail sera une tâche supervisé de classification binaire. On aurait pu faire en multiclasse mais comme il y a une notion d'ordre entre ces classes, que le sens des classes n'est pas significatif et pour simplifié ce problème, nous avons choisi de se limiter à une classification binaire.

c) La database archive 1885 personnes interrogées. Pour chaque personne, il y a 12 attributs : l'ID pour référence dans la database, l'age, le genre, l'education, le pays de résidence, l'appartenance ethnique et une mesure de la personnalité selon les critères NEO-FFI-R (neuroticism, extraversion, openness to experience, agreeableness, and conscientiousness), BIS-11 (impulsivity), et ImpSS (sensation seeking).

La database contient 18 problèmes de classification correspondant à 18 drogues. Comme dit précédemment nous allons nous focaliser tout d'abord sur une drogue, le cannabis. Ce choix est expliqué dans la question e).

Tout d'abord il faut noter que les créateurs du dataset ont fait le choix de mettre tous attributs sous forme de réel que ça soit pour les catégories d'âge, le pays de résidence etc et les colonnes n'étaient pas nommées. Nous allons donc devoir nommer les colonnes à la main. Pour les pays et l'appartenance ethnique nous allons devoir par exemple nommer les pays en fonction de la correspondance donnée par les auteurs de la database puis faire des vecteurs one-hot, pour l'âge par contre nous n'avons pas encore décidé de comment traiter cela.

On commencera tout d'abord par supprimer la colonne ID.

Les classes existantes de problème dans le dataset sont "Never Used", "Used over a Decade Ago", "Used in Last Decade", "Used in Last Year", "Used in Last Month", "Used in Last Week", et "Used in Last Day".\
On fait le choix de fusionner ces classes : "Never Used", "Used over a Decade Ago", "Used in Last Decade" en la classe "non-user".
Et "Used in Last Year", "Used in Last Month", "Used in Last Week", et "Used in Last Day" également en la class "user".
On finira par une standardisation.

d) Les différents algorithmes possibles pour une classification binaire seraient : SVM, Naive Bayes, Random Forest, Logistic regression et K-Nearest Neighbours. Les deux dernières on souvent des problèmes si il y a trop de feature mais dans ce cas là devrait bien marché.
On pourra alors tester plusieurs de ces algorithmes et faire un tableau de comparaison.

e) Le point de vigilance se situe principalement dans l'équilibre des données. Concernant le cannabis le nombre de personnes ayant pris ou non du cannabis est plutôt équilibré. Nonobstant un léger rééquilibrage semble nécessaire.\
On remarque un déséquilibre concernant certaines données. Par exemple 90% des données ont été récupérées dans des pays anglophones et plus particulièrement 80% aux USA et au Royaume-Uni.

Concernant les hypers paramètres, on fera de la cross validation et on testera la feature map au vu du nombre raisonnable d'attribut et la régularisation.

Concernant la mesure de performance :
La métrique "Balanced Accuracy" semble être une bonne chose pour des données déséquilibrées. On peut aussi se posé la question de si on préfère éviter les faux négatifs ou les faux positifs. Je pense qu'identifier un non-user en user est plus intéréssant dans l'idée de chercher les profils à risque.
