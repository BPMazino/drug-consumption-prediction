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
Preprocessing, classification binaire sur une drogue, classification multilabel
Avec les données que nous avions, nous avions prévu de faire du préprocessing avant de pouvoir commencer nos tâches de classification.  
Notre dataset nous permettait d'aborder plusieurs problèmes de classifications différents. Nous avons décider de d'abord effectuer une classification binaire sur une drogue pour savoir si une personne est consommatrice ou non. Ensuite nous souhaitions réaliser une classification multilabel permettant de savoir si une personne consomme ou non chacune des drogues.


## Préprocessing
Pour commencer nous avons commencer par enlever les colonnes ID et ethnicity ainsi que les lignes des personnes ayant répondu qu'ils consommaient la drogue semeron. En effet, cette drogue fictive a été rajouté pour pouvoir repérer certains menteurs qui annonceraient qu'ils consomment plus qu'en réalité.  

Nous avons remplacé les strings dans les colonnes des drogues par des -1 et des 1. -1 correspond aux non consommateurs et 1 correspond aux consommateurs. Nous avons décidé de considérer comme consommatrice une personne ayant consommé la drogue durant la dernière année.

Ensuite nous avons décidé d'appliquer un one hot à certaines colonnes. Nous avions d'abord pensé ne faire que les colonnes genre et pays mais après plusieurs tests, nous avons décider d'aussi le faire pour les colonnes age et niveau d'éducation. Pour ces deux dernières colonnes nous pensions au départ que conservé un certain ordre avec des floats serait utile. Cependant après quelques tests, nous nous sommes rendu compte que les models performaient mieux avec un one hot sur ces colonnes.

Nous avons aussi appliquer une fonction permettant de standardiser toutes nos valeurs pour essayer d'avoir de meilleurs résultats.

## Classification binaire pour une drogue
Choix de la drogue, choix du model (arbre de decision), separation train/valid/test, test hyper parametre avec cross validation  
Conclusion : résultat pas très satisfaisant  

Nous avons choisi de réaliser notre classification binaire avec le cannabis car c'est la drogue pour laquelle le nombre de consommateurs est le plus proche du nombre de non consommateurs. Nous nous sommes donc dit que ce serait plus pratique pour pouvoir avoir un model efficace.  
Nous avons choisi d'utiliser un arbre de décision pour effectuer cette classification car on peut facilement visualiser les différents branchement.



## Analyse plus avancé des données
matrice de corrélation, comparaison des models
Conclusion : un arbre de décisions n'était pas un très bon choix bon notre problème, une regression linéaire ou une randomForest auraient surement été plus intéressantes


## Classification multi label
Choix du model(arbre de decision puis randomForest), choix des drogues à prédire, test hyper parametre, matrices de confusion  
Conclusion : pas de très bon résultat, on aurait surement pu faire mieux avec plusieurs classificateurs binaires si on avait le temps de les entrainer