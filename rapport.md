# Projet d'IAS

### groupe
Arifette Nassim  
Derathe Pierre   
De Amorim Matthias  
Mesbah Slimane


## Présentation du projet
### Description des données
Le jeu de données est nommé Drug consumption (quantified) Data Set.
Link : <https://archive.ics.uci.edu/ml/datasets/Drug+consumption+%28quantified%29>  

Les colonnes de ce dataset correspondent à un ID et différentes caractéristiques des personnes ayant participé à l'étude : âge, genre, niveau d'éducation, pays de résidence, ethnicité ainsi que des résultats aux tests psychologiques NEO-FFI-R, BIS-11 et impSS. Ces tests permettent de mesurer les caractéristiques suivantes : névrosisme, extraversion, ouverture à l'expérience, agréabilité, conscienciosité, impulsivité et la recherche de sensation.   
Dans le jeu données toutes les valeurs sont des floats ce qui ne pose pas de problème pour certaines caractéristique comme les résultats aux tests psychologiques mais qui a moins de sens pour d'autres informations comme le genre ou le pays de résidence.  


Il y a en plus de cela 18 colonnes qui nous donnent des informations sur la consommation de différentes drogues, dont une drogue fictive. Pour chaque drogue, on sait si la personne ne la jamais consommé, en a consommé il y a plus de dix ans, consommé il y a moins de dix ans, moins d'un an, moins d'un mois, moins d'une semaine ou dans la dernière journée.  
Ces données là ne sont pas des floats mais des string de la forme CLx où x est remplacé par un chiffre indiquant une certaine classe (CL0 = n'a jamais consommé cette drogue, CL7 = en a consommé dans la journée).

### Présentations des tâches prévus

Notre dataset nous permettait d'aborder plusieurs problèmes de classifications différents. Nous avons décider de d'abord effectuer une classification binaire sur une drogue pour savoir si une personne est consommatrice ou non. Ensuite nous souhaitions réaliser une classification multilabel permettant de savoir si une personne consomme ou non chacune des drogues.  
Avant tout cela nous avions aussi du préprocessing à faire pour pouvoir utiliser nos données.


## Préprocessing
Pour commencer nous avons commencer par enlever les colonnes ID et ethnicity ainsi que les lignes des personnes ayant répondu qu'ils consommaient la drogue semeron. En effet, cette drogue fictive a été rajouté pour pouvoir repérer certains menteurs qui annonceraient qu'ils consomment plus qu'en réalité.  

Nous avons remplacé les strings dans les colonnes des drogues par des -1 et des 1. -1 correspond aux non consommateurs et 1 correspond aux consommateurs. Nous avons décidé de considérer comme consommatrice une personne ayant consommé la drogue durant la dernière année.

Ensuite nous avons décidé d'appliquer un one hot à certaines colonnes. Nous avions d'abord pensé ne faire que les colonnes genre et pays mais après plusieurs tests, nous avons décider d'aussi le faire pour les colonnes age et niveau d'éducation. Pour ces deux dernières colonnes nous pensions au départ que conservé un certain ordre avec des floats serait utile. Cependant après quelques tests, nous nous sommes rendu compte que les models performaient mieux avec un one hot sur ces colonnes.

Nous avons aussi appliquer une fonction permettant de standardiser toutes nos valeurs pour essayer d'avoir de meilleurs résultats.

## Arbre de décision

L'arbre de décision est un algorithme de classification. Il consiste a créé des noeuds. Chaque noeud pose un seuil sur une feature qui sépare les données en deux. Avec les hyper paramètres que nous avons utilisé, ce seuil est définie en parcourant toutes les features pour trouver la meilleur séparation, c'est-à-dire, dans le cas de notre classification binaire, le plus de consommateurs et le moins de non-consommateurs d'un côté et inversement de l'autre côté. Ces noeuds permettent de classer les données dans différentes feuilles où l'ont peut supposer la classe des données dedans.

## Classification binaire pour une drogue

Nous avons choisi de réaliser notre classification binaire avec le cannabis car c'est la drogue pour laquelle le nombre de consommateurs est le plus proche du nombre de non consommateurs. Nous nous sommes donc dit que ce serait plus pratique pour pouvoir avoir un model efficace.  

Nous avons choisi d'utiliser un arbre de décision pour effectuer cette classification car on peut facilement visualiser les différents branchement.  
Nous avons effectuez une séparation du dataset en conservant 20% des données pour le test final et 80% pour l'entrainement et la validation.  

![Plot de l'arbre de décision](./images/arbre_de_decision_cannabis.png)

Nous avons ensuite fait des tests d'hyper-paramètres avec de la cross-validation pour essayer de trouver quelle manière de limiter la taille de l'arbre était la plus efficace. Cependant quelque soit le paramètre choisi, on restait à un score de balanced accuracy d'environ 0.80, seul l'overfitting variait.  

![Figures des tests d'hyper-paramètres pour l'arbre de décision](./images/test_hyperparam_cannabis.png)

Nous n'avons donc pas réussi à améliorer notre model plus que cela et nous nous sommes demandé si avec un autre modèle nous aurions pu avoir de meilleurs résultats.


## Analyse plus avancé des données  

Après n'avoir pas réussi à obtenir de meilleur résultat avec notre premier model, nous avons réaliser de nouvelles analyses des données.  

Nous avons d'abord réalisé une matrice de corrélation qui nous a permis de voir que la plupart des résultat des tests psychologiques n'étaient que peu corréler entre eux. Les plus importantes corrélations étaient entre l'impulsivité et la recherche de sensation ainsi que entre l'ouverture à l'expérience et la recherche de sensation. On pouvait aussi voir que le névrosisme et l'extraversion était plutôt inversement corréler.  

![Matrice de corrélation](./images/matrice_de_correlation.png)

Nous avons ensuite observé la corrélation entre chacune des caractéristique et la consommation de cannabis. Ces corrélations correspondaient aux branchement que nous avions avec l'arbre de décision.  

Après cela, nous avons comparé différent models et nous avons pu observé qu'utiliser un arbre de décision pour réaliser cette classification n'était pas le meilleur choix. Utiliser une random forest ou une régression linéaire aurait été plus efficace.  

![Figure de comparaison de plusieurs models](./images/model_comparaison.png)

## Random Forest

## Classification multi label

Pour réaliser une classification multi label, nous avons décider de nous occuper uniquement des 15 drogues illégales. Nous avons donc retirer les drogues suivantes : chocolat, cafféine et alcohol ainsi que semeron puisque ce n'est pas une vraie drogue.  

Nous avons d'abord fait la classification avec un arbre de décision car cet algorythme peut traiter une target multilabel. En effet, les noeuds vont chercher à trouver la meilleur séparation en regardant tout les labels. La conséquence que l'ont va observer est que les labels déséquilibrés vont mal être prédits.

De plus, nous pourrons comparer nos résultats avec la classification bianaire fait précédemment. Pour afficher nos résultats, nous avons choisi de faire une matrice de confusion par drogue ainsi que de calculer les roc auc score et balanced accuracy score moyens.  
Nous avons obtenue une balanced accuracy de 0.62. Il n'y avait que quelques drogues qui étaient pas trop mal classé. Certaines drogues pour lesquelles il y a très peu de consommateurs n'étaient pas vraiment classé, tous les échantillons étaient considéré comme non-consommateur.  

![Matrices de confusion avec l'arbre de décision](./images/matrice_de_confusion_arbre_de_decision.png)

Nous avons ensuite fait la classification avec une random forest puisque cela semblait être un des meilleurs modèles selon nos analyses précédentes et qu'elle utilise encore des arbres de décisions. Nous nous sommes aussi dit que le hasard qu'apportait la random forest permettrait peut-être de moins être affecté par le problème d'équilibrage entre les consommateurs et les non-consommateurs de certaines drogues.  
Avec la random forest nous restions à un balanced accuracy score d'environ 0.63 donc nous avons réaliser des tests d'hyper-paramètres pour essayer d'améliorer nos résultats mais les différents tests ne permettaient pas d'améliorer le score de manière remarquable, juste de connaître l'overfitting.  

![Matrices de confusion avec la random forest](./images/matrice_de_confusion_random_forest.png)

![Figure du test des hyper-paramètres de la random forest](./images/test_hyperparam_random_forest.png)

Nous pensons qu'en réalisant un model de classification binaire pour chacune des drogues nous aurions sûrement pu avoir de meilleurs résultats, cependant cela nous aurais pris bien plus de temps.

