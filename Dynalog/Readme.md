Le projet **DYNALOG** s’inscrit dans un cadre de l’intra-logistique et de la robotisation d’entrepôts, où des robots mobiles répondent aux besoins de flexibilité et de performance des entreprises. En particulier, le projet porte sur l’étude de la solution de FIVES XCELLA, où la gestion des commandes est assurée par une flotte d’AGV capables de circuler et d’accéder aux rayonnages de l’entrepôt à travers un ensemble d’ascenseurs afin d’y récupérer ou d’y déposer des colis. Il s’agit d’une solution dite « case picking », méthode qui consiste à prélever une caisse complète d’un produit (bac ou colis) plutôt qu'une seule unité, pour soit être rangée dans le stock de l’entrepôt soit composer une commande de sortie (palette).

Cette solution met en évidence l’importance de la gestion du stock ainsi que de l’ordonnancement des tâches et du choix des chemins des AGV. 

![image](../images/Xcella.jpg)

Les entrepôts de la solution FIVES XCELLA organise le stock de produit en allées avec des étages possédant des ascenseurs de montée d’un côté et de descente de l’autre. Ces étages sont eux-mêmes organisés sous forme de baies, meuble possédant un certain nombre d’emplacements pour disposer les colis. Chaque baie est séparée par les supports des étagères.  

En plus du stock, est présente une zone au sol pour la partie préparation du stock et des commandes. Des robots dé-palettiseurs déposent les colis à stocker sur des convoyeurs pour que les AGV les récupèrent sur des points de collecte (Bases IN). De même, des robots palettiseurs récupèrent les colis à sortir du stock sur des convoyeurs, alimentés par les colis déposés par les AGV sur des points de dépose (Bases OUT). Nous supposons que les débits globaux en entrée et sortie sont égaux ; de telle sorte que le nombre de produits présents dans le stock soit constant en moyenne.

Les AGV peuvent se déplacer dans l’entrepôt en roulant au sol, emprunter les ascenseurs (Xcalator) pour accéder aux étages et se déplacer sur les rails. L’ensemble des déplacements autorisés par les AGV est modélisé par un graphe orienté. Les nœuds du graphe représentent les points d’intérêt au sol ou dans le stock. 

Le tableau ci-dessous présente les éléments principaux de l’entrepôt avec leur description et leur abréviation pour leur utilisation.


