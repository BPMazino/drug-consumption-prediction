# Projet d'IAS

### groupe
Arifette Nassim  
Derathe Pierre   
De Amorim Matthias  
Mesbah Slimane


## Présentation du projet
### Description des données
Tout est en float,  liste des colonnes, nombre d'echantillons
### Présentations des tâches prévus
Preprocessing, classifaication binaire sur une drogue, classification multilabel


## Préprocessing
Enlever lignes drogue semer, enlever colonne ethnicity, oneHot, standardisation


## Classification binaire pour une drogue
Choix de la drogue, choix du model (arbre de decision), separation train/valid/test, test hyper parametre avec cross validation  
Conclusion : résultat pas très satisfaisant


## Analyse plus avancé des données
matrice de corrélation, comparaison des models
Conclusion : un arbre de décisions n'était pas un très bon choix bon notre problème, une regression linéaire ou une randomForest auraient surement été plus intéressantes


## Classification multi label
Choix du model(arbre de decision puis randomForest), choix des drogues à prédire, test hyper parametre, matrices de confusion  
Conclusion : pas de très bon résultat, on aurait surement pu faire mieux avec plusieurs classificateurs binaires si on avait le temps de les entrainer