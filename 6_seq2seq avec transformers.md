# TP 7

L'objet principal de ce TP est de traiter les données du TP6 avec un réseau de type 'transformer'. 

Il vous est demandée, au préalable, de compléter les exercices du TP6 avec des variantes de l'architecture RNN du TP6.


### Calcul de la performance du RNN

La dernière question du TP 6 était de décoder et d'afficher les séquences du jeu de test. Vous allez désormais calculer sa performance en mesurant l'accuracy moyenne. Il s'agit du pourcentage de caractères qui sont décodé correctement par le RNN

### Mesure de la performance sur un jeu de données plus difficile

Les fichiers 'train_set2.pt' et 'test_set2.pt' contiennent un jeu de données plus difficiles. 
Affichez les chaines de caractères codées et décodées et essayer de comprendre comment le codage est réalisez.
Mesurer la performance du RNN précédent sur ce nouveau jeu de données. Expliquez pourquoi la performance est beaucoup moins bonne qu'avec le jeu de données précédent.


### Réalisation d'un réseau de neurones seq2seq comprenant un encodeur et un décodeur séparés.
Réalisez réseau de neurones seq2seq comprenant un encodeur et un décodeur séparés, chacun étant obenu avec un RNN. Pourquoi ce type d'architecture est mieux adaptée que la précédernte ?
Mesurez la performance de ce nouveau réseau sur le nouveau jeu de test et sur le précédent.

### Réalisation d'un seqa2seq avec des couches linéaires
Expliquez comment réaliser un traducteur de séquence seq2seq uniquement avec des couches linéaires (pas de RNN). 
Mesurez sa performance sur les deux bases de séquences précédement étudiées.
Commentez les résultats

###  Mesure de la performance sur un jeu de données en core plus difficile
Les fichiers 'train_set3.pt' et 'test_set3.pt' contiennent un jeu de données encore plus difficiles que les deux précédent. 
Affichez les chaines de caractères codées et décodées et essayer de comprendre comment le codage est réalisez.
Mesurer la performance des 2 RNN précédents et du réseau entièrement basé sur des couches linéaires sur ce nouveau jeu de données.  

### Réseau à base de transformer
Vous construirez désormais un traducteur de séquence basé sur un transformer.
Mesurez sa performance sur le dernier jeu de données et sur les deux précédents.
