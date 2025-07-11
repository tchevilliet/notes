#Journal de bord

## 24 juin 2025

### Exploration de l'observatoire RE2020

L'exploration porte sur les données envoyées par l'observatoire de la RER2020 en mai 2025. Elle se compose des exports par groupe, zone, bâtiments, et opérations des données pour lesquelles il y a eu une Déclaration Attestant l'Achèvement et la Conformité des Travaux (DAACT) depuis la mise en place de la RE2020 (1er janvier 2022) stockés [ici](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/IN/). Un descriptif succinct des champs nous a également été fourni.

Le fichier traitant des bâtiments contient 80581 lignes et 271 colonnes.
En nombre et en surface, les maisons individuelles sont très majoritaires [tableau récapitulatif ici](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/OUT/surfaces_par_usage.xlsx) : 97% en nombre, 80% en surface de référence. 

Le taux de remplissage est très important pour tous les champs à l'exception de 18 qui semblent anecdotiques et/ou pour lesquels il semble naturels d'être peu remplis (par exemple, champ qui induqe le générateur de froid, ou celui secondaire de chauffage, la hauteur des ascenseurs, le second usage principal, etc.)

####Parenthèse définition des surfaces

La surface de référence est définie, à l'[annexe de l'article R. 172-4 du code de la construction et de l'habitation](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000045292850/2022-03-04), ainsi :

_La surface de référence d'un bâtiment ou d'une partie de bâtiment, noté Sref est :_

- _Pour un bâtiment ou une partie de bâtiment à usage d'habitation, la surface habitable du bâtiment ou de la partie de bâtiment ;_

- _Pour les autres cas, la surface utile du bâtiment ou de la partie de bâtiment._

La surface utile est définie comme suit dans l'annexe 1 du même arrêté :

_La surface utile d’un bâtiment ou d’une partie de bâtiment, au sens de la RE2020, est la surface de plancher construite des locaux soumis à la réglementation environnementale qui, en utilisation normale, sont chauffés à une température supérieure à 12°C ou refroidis à une température inférieure à 30°C, après déduction des :_

- _Surfaces occupées par les murs, y compris l'isolation ;_
- _Cloisons fixes prévues aux plans ;_
- _Poteaux ;_
- _Marches et cages d'escaliers ;_
- _Gaines ;_
- _Ébrasements de portes et de fenêtres ;_
- _Parties des locaux d'une hauteur inférieure à 1,80 m ;_
- _Parties du niveau inférieur servant d'emprise à un escalier, à une rampe d'accès ou les parties du niveau inférieur auquel s'arrêtent les trémies des ascenseurs, des monte-charges, des gaines et des conduits de fumée ou de ventilation ;_
- _Locaux techniques exclusivement affectés au fonctionnement général du bâtiment et à occupation passagère_

La surface habitable est définie comme suit dans l'[article R156-1 du Code de la construction et de l'habitation](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000043819221/)

_La surface habitable d'un logement est la surface de plancher construite, après déduction des surfaces occupées par les murs, cloisons, marches et cages d'escaliers, gaines, embrasures de portes et de fenêtres. Le volume habitable correspond au total des surfaces habitables ainsi définies multipliées par les hauteurs sous plafond._
_Il n'est pas tenu compte de la superficie des combles non aménagés, caves, sous-sols, remises, garages, terrasses, loggias, balcons, séchoirs extérieurs au logement, vérandas, volumes vitrés prévus à l'article R. 155-1, locaux communs et autres dépendances des logements, ni des parties de locaux d'une hauteur inférieure à 1,80 mètre._

En conséquence, quand on utilisera la Sref, on sera toujours un peu en-dessous de la surface de plancher : doit-on utiliser un ratio ? Pas trouvable aisément...


## 25 juin 2025

### Reprise exploration de l'observatoire RE2020

Malgré le fort taux de remplissage, beaucoup de champs importants pour déterminer _a priori_ les quantités de matières (matériau de la structure, nature de l'isolant, etc.) sont indiquer comme "Autre" (63% pour le matériau de la structure au global, ordre de grandeur similaire pour autres champs), résultats consignés [ici](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/OUT/Résultats globaux/dc_materiau_structure.xlsx). Il semble y avoir un plus grand usage de la valeur "Autre" pour les maisons individuelles, voir les tableaux par usage [ici](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/OUT/Par usage/dc_materiau_structure.xlsx) et les graphiques [là](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/OUT/graphs).

En ne gardant que ceux dont le matériau de structure est indiqué, on tombe à 30146 bâtiments. Une grande partie des champs a vu le taux d'usage de la valeur "Autre" diminué, sans disparaître (petite corrélation entre mauvais remplissage du champ structure et des autres), voir [graphiques](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/OUT/graphs/graphs_sans_autre_mat_struct). Les proportions en nombre sont à peu près conservées (95% de maisons individuelles, résultats [ici](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/OUT/nombres_par_usage_filtre.xlsx)), mais sont changées en surface (68% de surfaces de maisons individuelles et 21% de logements collectifs, résultats [là](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/OUT/surfaces_par_usage_filtre.xlsx)).

#### Réflexion sur les raisons et la possibilité d'utiliser une telle base de donnée : 

Je me pose là question en ces termes : je veux comparer des projets urbains qui sont des vecteurs de surfaces d'archétypes, et je veux savoir si un arbitrage est possible malgré les incertitudes de premier et d'arrière-plan. Je veux aussi pouvoir faire des analyses de contribution de toutes sortes, en remontant à quelques rangs dans le graphe ou jusqu'aux flux élémentaires, des analyses de sensibilités globales et locales, et autre analyses d'incertitudes. Aussi, il faut que je connecte le graphe d'avant-plan au graphe d'arrière-plan (ecoinvent).


h = CBA¹Dx

Ou x est le vecteur de surfaces d'archétypes décrivant le projet et D la matrice associant ces archétypes à des procédés ecoinvent. On peut considérer D comme le produit d'une matrice Darch qui associe chaque archétype à un ensemble de matériaux et de consommations et Dmc une matrice qui associe chacun des matériaux et consommations à des procédés du graphe d'arrière-plan. Les coefficients de Dmc sont déjà implémentés dans les échanges des procédés matériaux avec ecoinvent dans la BDD réalisé pour Tirado, même s'il en faudrait des nouveaux : des micro puis macro-composants du bâtiments que chaque archétype viendrait appeler. Darch contient justement les valeurs d'échanges entre ces composants et les archétypes, et ce sont eux que j'essaye de déterminer grâce à la base de donnée.
Démarche en trois temps activée : 
- demande faite à l'observatoire si ils ne disposent pas des quantités
- creuser la manière dont TyPy fonctionne vraiment
- Avoir recours à des régressions Bayesiennes comme montrées par Maxime pour estimer quantités de matières à partir des résultats d'impacts... 


## 26 juin 2025

### Lecture des retours feuille de route

Question FJ sur utilisation du stock récent :
Pour l'instant, la plage de temps considérée est dépendante de la source utilisée et se cale sur réglementations thermiques.

FJ sur incertitudes des méthodes d'impact : limite importante de la caractérisation sans indiquer d'incertitudes, limite inhérente à l'ACV. Benchmark des méthodes qui fournissent des distributions de CF ?

FJ sur prise en compte de l'environnement : intégrer une partie sur comment c'est pris en compte (labels écoquartier, bbca, les outils opérationnels existants aussi : urbanprint notamment)

CR sur les seuils programme : il faudrait une référence qui a du sens, voir travail de marin pellan sur acv bâtiment et budget national carbone ?

CR sur AWARE comme article : oui, petit travail d'actualisation à mener car nouveaux coefficients, voir notamment si effets littoraux existe encore

FJ sur contextualisation possible des archétypes : L'idée est de filtrer selon une zone géographique, un archétype par usage.

FJ sur hypothèse pour paroi : utilisation pourquoi pas de RE2020 ou BDNB.

### Reprise exploration de l'observatoire RE2020

Tentative de détection de corrélation compacité Cef chaud, pas convaincant, jointplot [ici](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/OUT/graphs/correlation?/).


## 8 juillet 2025

### Lecture articles 

#### Sigurdardottir, 2023

ACV d'un quartier neuf à Rekjavik : restreint à la phase pre-use, avec un focus GWP, même si autre indicateurs REciPe calculés. Le plan est divisé en 3 domaines : Bâtiments, autres espaces et réseaux. Le dernier est laissé de côté par manque d'information. Les bâtiments sont projetés à partir d'esquisses architecturales simples pour comptabiliser les matières. On a un archétype unique qui est utilisé pour tous les bâtiments, celui de Heinonen 2016 sur une une "ACV" pre-use d'une résidence multi-étages (attention, ici, pas mention d'archétype ni d'usage de notion d'intensité matériel). Quelques hypothèses supplémentaires sur la couverture, les façades, à partir des documents de planification et des "current trend"... Subdivision des autres espaces en 7 types : routes, chemins piétons, surfaces enherbées, pistes cyclables, parkings végétalisés, cour d'école et parking silo. Ils sont tous la combinaison de market for grass, asphalt, concrete aciers pour le parking. Sur les résultats, on a des différences par types de programme, qui ne sont dus qu'aux différences géométriques si je comprends bien.
Dans les discussions, mention est faite de la question des durées de vie, en citant principalement Ji 2021 qui présente une approche big data IA, à regarder...
Évoque la comparaison IO et process-based (lire article saynajoki 2017 sur comparaison pour ACV bâtiment.) Les incertitudes sont évoquées snas être quantifiées (un chiffre est tout de même donné indiquant que le ferraillage des fondations pourrait doubler et augmenter le bilan carbone de 10%).

#### Ruiz-Valero, 2025

Review sur la base de l'idée que les ACV de logement devrait étendre les limites de leur système pour intégrer le bâti, la mobilité quotidienne des résidents, les espaces extérieurs et les réseaux. Trois dénominations proposées en fonction du périmètre spatial et des types d'éléments proposés : ACV standard de logements (un bâtiment), ACV holistique de logements (un bâtiment + mobilité + espaces extérieurs + réseaux), ACV de quartier (plusieurs bâtiments + mobilité + espaces extérieurs + réseaux). Nomenclature claire, mais on peut discuter de l'appellation neighborhood lorsque tous les bâtiments ont le même usage ? C'est un critère que l'on pourrait ajouter pour distinguer ce qu'on appelle ACV de quartier. Rappel sur les approches ACV possibles : process based lorsque l'info est disponible, mais demandeuse en ressource et problème de troncature, IO lorsque données économiques dispo, mais peu spécifiques ; hybrid qui tente de résoudre les deux problèmes de complétude et de spécificité. 
La durée de vie est évoquée comme paramètre important mais variable des études. Un graphiques montr une prédominance du 50 ans. Côté quartier, on monte à 100 ans. Idem sur méthode ACV, prédominance des hybrides pour le quartier. 
Les logiciels utilisés pour la modélisation thermique sont évoqués, EnergyPlus et Pleiades sont évoqués. Pour les données d'espaces extérieurs, de réseaux et de mobilités, la revue confirme que sont utilisés statistiques et proxys.
L'article différencie les objectifs de recherche du cadre standard (optimisation des choix structurels, de matériaux, et mesures d'efficacité énergétique), du cadre holistique (choix de la forme urbaine, maison individuelle vs bâtiment en centre-ville) et du cadre quartier (projets de développement urbain). La différence holistique quartier est ici clairement compliquée à établir : Dans une comparaison bâtiment résidentiel centre-ville / maisons individuelle, l'unité fonctionnelle commune implique d'avoir plusieurs maisons individuelles, ce qui transforme l'étude en étude de quartier selon les définitons de l'article. Le multi-programme semble donc être un critère de définition pertinent pour parler d'ACV de quartier. 
Régionalisation simplement évoquée comme moyen de rendre plus "représentatif" les résultats.

### Réflexion sur mon modèle
Penser à construire les process (matériaux, archétypes et projets) pour pouvoir faire analyse de ocntribution par phase du cycle de vie. Mettre par ailleurs des paramètres partout pour les questions de durée de vie, notamment si l'on souhaite un moment voir ce que donne une différentiation des durées de vies de références considérées pour les archétypes...
A la lecture de Ruiz-Valero sur toutes ces études qui définissent des unités fonctionnelles précises pour être comparables, mais qui choisissent des durées de vie différentes donnent envie d'être clair sur ces sujets et de prendre en compte la DVR comme un pur paramètre de l'étude avec analyse de sensibilité. Par ailleurs, cela donne envie d'intégrer des modèles simples de réseaux et mobilités pour être complet.


## 8 juillet 2025

### Lecture articles 

#### Nematchoua et Reiter, 2019

L'article présente une étude d'écoquartier, son but étant de déterminer "les coûts environnementaux les plus importants". Pour ce faire, les impacts sont traduits en coûts monétaires par la méthode de monétisation MMG (table de conversion issu d'une agence de gestion des déchets de Flandres...) La partie résidentielle uniquement a été modélisée, avec l'UF suivante : "eco-quartier résidentiel de 3,5 ha comprenant [surfaces exactes du projets], hébergeant 220 personnes, étudié sur un cycle de vie de 80 ans et situé à Liège, en Belgique". On voit ici que l'objet étudié est uniquement la géométrie du quartier.Pas de méthode utilisé, mais un ensemble d'indicateurs avec auto-citation pour les réfs en plus de Guinée. L'article semble catastrophique, lecture arrêtée.

#### Dorra et al, 2022

Introduction claire sur une différence entre évaluation territorial-based et consumption-based qui demande à être précis sur les limites du système.


### GT ACV Maxime

Algo supervisés : pb Y =f(X) + e avec X et Y des entrées et sorties connues et e l'erreur aléatoire. pb du sur-ajustement : erreur minimale pour des modèles sur-ajustés.
Algo non supervisés : on a X mais pas Y. On essaye donc de comprendre la structure de X, on cherche à détecter des groupes par exemple, détecter des anomalies, ou enfin de réduire la dimension du problème. On cherche par exemple g et f tq Z = g(X) et X_estimé = f(Z) et on cherche à minimiser la moyenne quadratique de X - f(g(X).

## 10 juillet 2025

### Lecture articles

#### Schildt et al, 2024

L'objectif est de mieux estimer la quantité de murs intérieurs des bâtiments à une échelle urbaine. Évoque en introduction le format de données CityGML, voir si l'on souhaite/a besoin de se mettre dans ce cadre pour qualifier la maquette (LOD suffit sûrement). 
Utilisation du terme archétypes pour enrichir les géométries et les modèles de simulations énergétiques.
Modèle en graphe pour avoir les surfaces de murs intérieurs en fonctions des longueurs, largeurs de pièces et hauteurs d'étages... Cela permet d'avoir cette quantité sur des intervalles de paramètres.
Des tirages LHS sont faits pour distribution uniforme en faible temps de calcul.
Cas d'étude sur un quartier de maisons individuelles en Allemagne avec 4 types de maisons. Beaucoup d'informations sont disponibles, l'incertitude n'est vraiment considérée que sur les murs intérieurs. Toutefois, ça permet d'avoir une validation de l'estimation de surfaces de murs (l'estimation semble plutôt mauvaise). Démarche de validation d'inventaire que j'aimerais avoir 

#### Lausselet 2022

ACV hybride pour l'étude d'un écoquartier norvégien, seulement sur les gazs à effet de serre seulement pour phases de production et de construction. Des coefficients hybrid sont calculés pour chaque matière contenu dans cahcun des types de bâtiments. Les coefficients sont construits : 1) en identifiant les process concernés dans ecoinvent, et les secteurs concernés dans EXIOBASE 2) en supprimant les process qui font doublons

### Réflexion sur mon modèle

A la lecture de Schildt 2024, il semble nécessaire de préciser, au moment de la construction des archétypes statistiques leur statut et leur différence avec les archétypes usuellement utilisés dans les simulations énergétiques (les définir en somme) : alors que le terme est souvent utilisé pour désigner un ensemble d'entrées de la simulation (détails géométriques, cractéristiques thermiques, planning d'occupation, etc.) qui sont dépendantes de certaines caractéristiques des bâtiments (années de construction, programme, localisation, etc.), je l'utilise pour désigner directement les quantités de matières et d'énergie associées à ces caractéristiques. 




