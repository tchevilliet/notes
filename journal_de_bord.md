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
Les logiciels utilisés pour la modélisation thermique sont évoqués, EnergyPlus et Pleiades sont cités. Pour les données d'espaces extérieurs, de réseaux et de mobilités, la revue confirme que sont utilisés statistiques et proxys.
L'article différencie les objectifs de recherche du cadre standard (optimisation des choix structurels, de matériaux, et mesures d'efficacité énergétique), du cadre holistique (choix de la forme urbaine, maison individuelle vs bâtiment en centre-ville) et du cadre quartier (projets de développement urbain). La différence holistique/quartier est ici clairement compliquée à établir : Dans une comparaison bâtiment résidentiel centre-ville / maisons individuelle, l'unité fonctionnelle commune implique d'avoir plusieurs maisons individuelles, ce qui transforme l'étude en étude de quartier selon les définitons de l'article. Le multi-programme semble donc être un critère de définition pertinent pour parler d'ACV de quartier. 
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

## 14 août 2025

### Question à propos RE2020 

Les quantités fournies comptent-elle les renouvellements éventuels ? (Sur les éléments non structurels)

### Lecture articles

#### Stephan et al 2022
Proposition ambitieuse de cadre pour étude des environnements construits pour tous les acteurs à toutes les échelles en se basant sur une structure de programmation objet. L'introduction cible les problèmes suivants :
 -  d'abord que les études existantes sont mono disciplinaire, mono-echelle et parfois mono étape.
 - a l'échelle des bâtiments, 2 problèmes soulignés : la sous estimation des flux élémentaires embodied par les analyses basées sur des procédés (il cite Crawford 2018, islam 2016, majeau bettez 2011, suh 2004); la non intégration des infrastructures nécessaires autour de ces bâtiments, ou encore celle de la mobilité (il cite Stephan et Crawford 2014a, Stephan 2012, 2013 et Stephan & Stephan 2014 et 2016)
 -  aux échelles quartier et ville : problème majeur, construction depuis des détails, donc usage de valeurs moyennes pour tout un quartier (même valeurs dynamiques parfois, Sartori 2016, Sandberg 2016), donc ne peut être utilisé pour plus petites échelles que celle de la ville ( voir Lanau 2019 qui est cité).
 
##### Methode de construction d'inventaire 

INTERMÉDIAIRES : De la même manière que dans TyPy, sont associés à une géométrie simplifiée (type BD TOPO / LOD 100) des macro-composants ("assemblies"), eux-même reliés à des quantités de matières et d'éléments. Des renouvellements sont considérés sur la période d'étude sur la base de des durées de vie ou "courbes de survie" des éléments ou macro-composants (tirés notamment de Stephan et al 2018).

ÉLÉMENTAIRES : Les flux associés aux matériaux/éléments sont issus d'une approche hybride (Path-Exchange hybrid analysis) dont les coefficients permettent d'accéder à l'énergie, l'eau et les GES embodied. Durant l'exploitation, les consommations de chaud et de froid sont calculés via EnergyPlus, mais on ne sait pas exactement comment. Les consommations d'électriques spécifiques et d'eau sont calculés au ratio par type de bâtiment, planning d'occupation et nombre de systèmes/appareils (mais on ne sait pas comment tout ça pourrait être déterminé à grande échelle). Les flux élémentaires liés à la mobilité des occupants sont obtenus en mutlipliant les distances moyennes des occupants pour chaque mode de mobilité par les intensités de flux directes et indirectes de ces modes de mobilités. Une séquestration carbone de la végétation et des sols est prise en compte selon méthode de l'US department of energy datant de 1998...

Tous les flux se voient traités de manière dynamique, ie ils disposent d'un indice y et peuvent changer dans le temps. Les valeurs évoluent selon les entrées arbitraires de l'utilisateur et autre scénarios prospectifs. 
Le modèle sera lié à des SIG : comment ?

##### Méthode de caractérisation

Aucun mot sur les méthodes d'impact. La base utilisée (EPiC Database) ne contient que les flux d'énergie, d'eau et de GES. La base s'appuie sur AusLCI, base australienne de macro-procédés réalisés à partir d'ecoinvent 2.2 pour la partie process-based et sur des tables Input-Output de 2014-15 pour la partie IO.

##### Démarches d'interpretation 
Les incertitudes sont énoncées très importantes (±40% sur les indicateurs calculés par cette méthode), mais sont exclus de la démarche d'interprétation sous couvert de comparaison de scénarios souffrant des même incertitudes, qui se compenseraient donc... Ce qui est répété en discussion.
Diagram sankey qui permet analyse de contribution des phase, lots, typologies de bâtiment aux émissions de GES. Diagramme des masses de matériaux et graphe de GES cumulées par an.



## 18 août 2025

### Présentation Vicente

slide 1 : "de vie de vie"
slide intro : "créé avec UGE/CNRS"
slide revue : ne pas laisser entendre que l'ACV permet de quantifier tous ces indices
slide ACV approche matricielle : f!= flux de référence
slide ACV ? : rappeler la structure de la présentation sur les slides. ACV multi-critère mais étude mono-critère, pourquoi ? (CIOGEN multi, brightway multi)
slide brightway : enlever précision
slide CIOGEN 1 résultats : variation significative ?
slide CIOGENs : nbre de chiffres significatifs
slide brightway vs ciogen : pourquoi prioriser, pas immédiat. Comment fin de vie est représenté si contrib négative.
slide conclusion : souligner ce qu'il faudrait faire pour valider les hypothèses énoncées.

## 19 août 2025

### Création archétypes RE2020

Première exploration des envois avec quantités de matières de la RE2020 dans le fichier [250812_main.py](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/250812_main.py). La table envoyée (enregistrée [là](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/IN/composant_open_data_0525.parquet))contient plus de 6 millions de lignes, pour environ 80 000 bâtiments déclarés achevés, soit en moyenne 75 lignes par bâtiment. Chaque ligne est une quantité : le projet auquel elle appartient est identifiée dans un champ "projet\_id", existant aussi dans les précédentes tables ; le produit auquel elle se rattache est décrit par 5 champs de nomenclature inies :

- niveau 1 : longueur 3 -> Produit de construction, Services ou Équipements
- niveau 2 : longueur 28 -> lots type Isolation, ou Structure/Gros Oeuvre 
- niveau 3 : longueur 144 -> sous-lots parfois très précis si lots de faible ampleur (Évier par exemple) ou moins précis si lots importants (Traitement d'air pour Équipements de Génie Climatique ou Dalles et prédalles pour Structure)
- niveau 4 : longueur 280 -> éléments ou matériaux (Chaudières pour sous-lot "Chauffage et/ou rafraîchissement et/ou production d’eau chaude sanitaire" ou Bois pour sous-lot "Bardages (vêture / vêtage / parement)")
- niveau 5 : longueur 154 -> précision sur l'élément, très souvent vide (plus de 85% des lignes vides)

_In fine_, 670 nomenclatures uniques apparaissent dans la table. On pourrait donc exprimer tous les bâtiments à partir de celles-ci, à voir tout de même si on ne priorise pas certains lots et sous-lots pour simplifier la modélisation...

On ajoute à la table des quantités des champs importants des tables précédentes (notamment [celle-ci](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/IN/202505_export_batiments_daact.csv)), à savoir l'usage principal (champ "usage\_principal\_1\_txt") et la surface de référence "sref" pour le calcul (voir définition des surfaces plus haut), la jointure se faisant par le champ "projet\_id". On crée un champ de quantités surfaciques ("quant\_surf"). Cette table augmentée est enregistrée [ici](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/OUT/quantites_augmentees.parquet) en format parquet.

On peut ensuite extraire/afficher les distributions de valeurs de certains éléments de nomenclatures et tenter de les fitter avec une distribution lognormale comme cet exemple avec le béton armé de fondations pour les maisons individuelles [ici](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/OUT/quantités_par_usage_par_nomenclature/Maison individuelle ou accolée_['Fondations '].pdf) et les logements collectifs [là](/home/thibault.chevilliet@enpc.fr/Documents/Obs_RE2020/OUT/quantités_par_usage_par_nomenclature/Logement collectif_['Fondations '].pdf).


## 20 août 2025

### Lecture articles

#### Li et Feng, 2025

##### Objectifs et périmètre analyse
L'article propose un cadre de travail pour des ACV spatialisées des bâtiments existants canadiens, dont l'objectif, illustré dans un cas d'étude, est d'identifier des zones à haut impact environnemental pour y prioriser les réhabilitations et le passage aux énergies renouvelables.
L'étude évalue les impacts de l'utilisation d'énergie des bâtiments sur tout leur cycle de vie, avec une PER de 60 ans, ainsi que ceux , directs et indirects, des stratégies de rénovations dans certains scénarios. Le cas d'étude est Richmond en Colombie Britannique, au Canada.
Unité fonctionnelle : m2 de bâtiment. Le flux de référence étant la surface "nette" de plancher. La définiton des intensités d'impact considérée comme une normalisation.

##### Methode de construction d'inventaire 
5 archétypes sont modélisés (maison individiuelle, maisons mitoyennes "townhouse residential", bâtiment tertiaire, commerce de détail, et bâtiment industriel) sur REVIT. Des intensités matérielles et énergies sont calculées pour chacun, via energyPlus (les caractéristiques thermiques étant fonction de la période de construction) et Revit. Ces intensités sont appliquées à une maquette LOD1 (emprise extrudée par élévation) du territoire étudié pour le scénario BAU. Sont ajoutées à ces intensités les impacts nécessaires à la réhab pour atteindre les objectifs net-zero (PV pour couvrir 100% des besoins annuels en élec, pompe à chaleur partout, et une isolation améliorée pour atteindre les objectifs de consos du net-zéro, rappelés dans l'article) dans le cas du scénario UNZEB.

##### Méthode de caractérisation
ReciPe est utilisée partiellement : 12 midpoint indicators (sur 18) et 2 endpoint indicators (sur 3). En plus, les demandes d'énergies fossile et issue de la biomasse sont calculées. La raison évoquée est un alignement avec la littérature, dont Mastrucci 2020, qui ne fait que du carbon footprint...

##### Démarches d'interpretation 
Les incertitudes sur les indicateurs d'impacts de chacun des archétypes sont fournies via les variances, écarts-types et relative standard deviation estimate. Cependant, il n'est pas dit quelles incertitudes sont propagées dans le modèle ni comment. (On imagine incertitude sur A et B, C a priori n'en a pas puisque ReciPe et quid de l'avant-plan ? a priori rien non plus car résultats par archétype, il n'y a pas de distance à l'archétype à estimer...)
L'analyse de sensibilité réalisée est ce que Heijungs 2024 appelle une analyse de sensibilité discrète par scénarios ou 8 augmentations de certains paramètres sont considérés et les effets relatifs par rapport à la baseline sont cumulés dans un score. Ne sont commentés que les parts de chacun des scénarios à ce score cumulé, ce qui est très dicutable (la variation du paramètre étant arbitraire, le poids dans ce score ne veut rien dire). 
La correlation entre indicateurs d'impacts est évaluées par test de Mantel, et une forte corrélation entre GWP, CED-fossil et Acidification terrestre est identifiée, synergie des actions suggérée.
Un diagramme de sankey est fourni décrivant graphique la contribution des phase, des lots et produits de construction. 
Hotspot spatiaux permis par GIS
Les limites identifiées sont : l'usage dans le modèle en temps réel du comportement des occupants, l'absence d'étude en coût global, les incertitudes sur les COP et les données, la variabilité par rapport aux archétypes qui empêche la généralisation 


## 21 août 2025

### Lecture articles

#### Su et al, 2025

Évoque Pfister 2020 en introduction, qui propose un shapefile global pour la régionalisation à venir des ACV. A déjà identifié l'intérêt des ACV dynamiques (DLCA), et décide d'y incorporer un système multi-agent (MAS).

##### Objectifs et périmètre analyse
Le but du modèle est l'évaluation dynamique des impacts d'un quartier. Il est annoncé que les impacts considérés sont uniquement ceux ayant lieu dans le périmètre du quartier, mais il a plus l'iar de s'agir d'une étude sur la phase d'usage seulement que d'impacts directs uniquement.

##### Méthode de construction d'inventaire 
6 agents participent à déterminer l'inventaire (climat, bâtiment, espaces verts, éclairage, mobilité, individus), avec pour chacun d'eux des attributs, déterminés par des données (par exemple météo), des inputs de l'utilisateur et des règles d'interaction entre attributs d'agents différents. Des "flux élémentaires d'avant-plan" (en fait consommations d'énergies et GES directs) sont calculés à l'instant t, multipliés par une intensité d'émissions par type d'énergie à l'instant t, puis sommé sur l'année. Les captations des espaces verts sont déduites des émissions de CO2 calculées.

##### Méthode de caractérisation
Pas de méthode de caractérisation spécifique utilisée. Quatre catégories d'impacts sont considérées : réchauffement climatique, acidification (on ne sait pas de quoi), eutrophisation (on ne sait pas de quoi) et les particules en suspension. Les facteurs de caractérisation sont issus de Cao 2012 (inaccessible). Une pondération en euros par kilogrammes de polluants est appliquée...

##### Démarches d'interpretation 
Pas d'analyse de contribution, ni d'incertitudes (le mot n'est écrit nulle part, une des limitations identifiées étant plutôt le manque de données). Pas d'analyse de sensibilité non plus, mais quatre scénarios d'optimisation des usages sont comparés sur la base du score unique pondéré.

#### Famiglietti et al, 2023

##### Objectifs et périmètre
Le but de l'outil présenté est d'évaluer l'impact des bâtiments (anciens ou neufs, mais existant) à une échelle urbaine par ACV process-based en considérant toutes les phases du cycle. Pour la vie en oeuvre, seuls le remplacement des produits et les consommations d'énergie sont considérées, l'auteur identifiant un manque de données pour les autres modules (maintenance, réparation, réhabilitation ou consommation d'eau).

##### Méthode de construction d'inventaire 
L'auteur opère une "simplification" l'équation h =CBA-1f en basculant sur h'=A'Q' ou les lignes d'A' sont les éléments de construction (macro-composants par phase) utilisés et les colonnes sont des produits et EF direct utilisés par ces éléments. Les lignes de la matrice Q' sont ces produits et EF, et ses colonnes les catégories d'impact.
Pour réaliser l'inventaire, des lois empiriques sont établies (polynôme second degré) pour établir la masse de béton armé en fonction du nombre d'étage par exemple. Les quantités de matériaux étant disponibles dans des bases de données. Pour les enveloppes, les quantités de matières sont inférées à partir du U, disponible dans la base évoquée, et du type de bâtiment et des compositions de parois qui lui sont liés. Des donnés moyennes de la littérature sont utilisées pour le transport, l'installation, la démolition/deconstruction et le transpor vers le traitement de fin de vie. ecoinvent 3.9.1 EN15804 est utilisée pour les procédés d'arrière-plan

##### Méthode de caractérisation
La méthode EF v3.1 est utilisée ainsi que la méthode de demande cumulée d'énergie. Chaque flux intermédiaire et élémentaire du système est directement caractérisé dans la matrice Q'.

##### Démarches d'interpretation 

Les résultats pour Milan sont présentés en tableau par phase et par élément (analyse de contribution). Les résultats sont comparés à d'autres articles, notamment Trigaux 2020. Une analyse de sensibilité OAT est annoncée dans l'annexe, c'est en fait une DSA au sens d'heijungs sur l'impact de la quantité de béton armé, la nature des isolants considérés et la conductivité des fenêtres sur le gwp, en distinguant le stock entier et les nouvelles constructions. Les résultats (globalement inférieurs à 10% de variations) sont jugés "consistent". Pas d'analyse d'incertitude, mais résultats sur la variabilité intra typologie pour chacun des impacts.


#### Long et al, 2024

##### Objectifs et périmètre
Un modèle "4D GIS-MFA-LCA" est proposé pour identifier la distribution spatiale et temporelle des stocks et des flux de matières, et leurs émissions associées. Objectif pratique : aider à la gestion des ressources matières, notamment au recyclage. L'étude ne se concentre que sur les émissions "incorporées" des materiaux de construction, en ignorant les phase de transport au site et à la mise en oeuvre (du fait d'un manque de données). La phase de vie en oeuvre des bâtiment est ignorée,mais la fin de vie considérée d'après figure (pas extrêmement explicite). Les bâtiments étudiés sont les existants, non patrimoniaux construits entre 1980 et 2020.

##### Méthode de construction d'inventaire 
Pour chacun des six types de bâtiments (tourisme, résidentiel, public, industriel, commercial et "Ecological reservation") sont établies des intensités matérielles pour 11 matériaux (ciment, bois, brique, graves, sable, argile, verre, asphalte, acier, aluminium et cuivre) d'après revue de la littérature, données empiriques sur site, rapport de l'administration et d'entreprises de construction. Ces intensités diffèrent également selon la période de construction. Le stock d'une année est déduit en multipliant ces intensités par les surfaces, puis les déchets produits sont estimés à partir du stock. Le flux de matière entrant est calculé en comparant les stocks de l'année à l'année précédente, en y ajoutant les déchets (delta stock = entrant - sortant). Les flux élémentaires ne sont pas quantifiés.

##### Méthode de caractérisation
Les émissions carbone sont obtenues en multipliant les flux entrants par les facteurs de caractérisation carbone de la (CLCD Database, 2015) et en retranchant l'absorption de carbone par les bâtiments béton.

##### Démarches d'interpretation 
Analyse de contribution des types de bâtiments aux masses de décehts, mais pas à l'impact. Visualition (peu lisible) de la distribution spatiale.
Des projections sont faites en comparant des scénarios de traitement des déchets jusqu'en 2080, même si on ne nous donne pas d'information sur les nouvelles constructions considérées. Par ailleurs, la comparaison porte sur la masse, pas l'impact. Donc pas d'analyse de sensibilité réalisée.
La seule variabilité évoquée est celle non prise en compte de la durée de vie des différents types de bâtiments. Pas d'analyse d'incertitude.

#### Papageorgiou et al, 2024

##### Objectifs et périmètre
Le modèle d'ACv du métabolisme urbain proposé vise à évaluer les impacts futurs des décisions d'aménagement et d'identifier les secteurs qui sont les contributeurs majeurs de ceux-là. Il s'agit aussi d'évaluer des stratégies d'économie circulaire à l'échelle urbaine. Le système étudié est constitué de tous les flux de matière et d'énergie entrants et sortant du système, et les impacts indirects de ces derniers sont pris en compte par ACV. Tous les secteurs d'activités sont considérés, à l'exception de l'agriculture, foresterie, pêche, de l'industrie manufacturière et des services par manque de données. L'article présente l'application du modèle à une commune moyenne de Suède. Une ACV rétrospective, et une ACV prospective sont réalisées.
Pas de définition de l'UF (comme dans Goldstein 2013, Garcia Guaita 2018 et Gonzalez-Garcia 2021), mais les impacts sont divisés par la population. Concept de responsabilité totale appliqué aux flux. Des flux jugés mineurs et n'ayant pas de données dans ecoinvent 3.8 (par exemple consommation pharmaceutique) ne sont pas pris en compte, tout comme le stock de la ville, puisque l'étude évalue les impacts annuels. Approche attributionnelle

##### Méthode de construction d'inventaire 
Les données de MEFA viennent d'un précédent article du même auteur, la même année (_Applying material and energy flow analysis to assess urban metabolism in the context of the circular economy_) et sont établies à partir de statistiques d'échelles urbaines, assez précises sur les questions d'énergies consommées par exemple puisqu'issue du producteur. Données de marché utilisées dès que possible, ce ui fait doublon avec le transport de marchandises compté aussi dans le secteur de transport.
Pour l'ACV prospective, les combinaisons de deux scénarios d'arrière-plan (SSP2-RCP 6.0 : pas de politique d'atténuation vs SSP2-RCP1.9 : politiques ambitieuses, avec premise) et de trois d'avant-plan (BAU vs réduction de la consommation vs augmentation du recyclage) sont étudiées.

##### Méthode de caractérisation
Douze indicateurs midpoint de la méthode ReCiPe 2008 (H) ont été utilisé pour pouvoir notamment se comparer aux précédentes études réalisées avec la même. Les indicateurs choisis sont ceux ayant été identifié comme les plus pertinents par les précédentes études.

##### Démarches d'interpretation
 
Analyse de contribution par secteur qui identifie les contributeurs majeurs et les sous-contributeurs à ces derniers. Pas d'analyse d'incertitude, même si un paragraphe est dédié à identifier les sources d'incertitudes dans le modèle. L'étude de différent scénarios pourrait être considéré comme une DSA, mais ce n'est pas annoncé comme une analyse de sensibilité. Les résultats sont comparés à d'autre ville, et l'ordre de grandeur de l'impact sur le changement climatique est le même que les autres études. Pour le reste, les grands écarts sur d'autres impacts sont imaginés dus aux différences inhérentes à ces villes de continents/pays différents.

#### Moisio et al, 2024

##### Objectifs et périmètre
L'article souhaite étendre le cadre des ACV conséquentielles déjà appliquées aux bâtiments à des une échelle urbaine en intégrant les infrastructures urbaines telles que routes et réseaux, afin de confirmer la réponse usuellement en faveur de la réhabilitation à la question : démolition-construction ou rénovation ?
Le périmètre de l'ACV dépend des effets de la décision étudiée. Les critères différenciant sont le caractère urbanisé (infrastructuré) de la zone ou non, et si l'on réhabilite, remplace ou construit.
Quatre scénarios vont être comparés : 
- Deux avec un besoin faible de densification, et donc extension ou démolition/construction;
- Deux avec un besoin fort de densification, si bien que l'extension maximale possible ne suffit pas et donc extension + viabilisation d'une nouvelle parcelle + construction ou démolition/construction plus dense.

##### Méthode de construction d'inventaire 
Pour la neuf comme la rénovaton/extension, un archétype est utilisé :
- celui d'un immeuble résidentiel des années 70 pour la réhabilitation, en ajustant le nombre de niveaux. Des étages identiques sont ajoutés pour modéliser l'extension
- celui d'une construction "typique" pour le neuf, à savoir un plan de tour carré contenant du studio au T3, avec balcons.
Les quantités de matières sont obtenues par maquette BIM (ArchiCad) ou tableur rempli manuellement avec surfaces et épaisseurs par exemple pour les revêtements.
Les consommations d'énergie sont obtenues par simulation pour les bâtiments modélisés en 3D (IDA ICE) et par applicaiton de ratio de consommation de bâtiments similaires sur les dernières années dans la ville en question.

##### Méthode de caractérisation
Méthode du ministère de l'environnement Finlandais, qui ne caractérise que l'impact sur le changement climatique (C02 data.fi).

##### Démarches d'interpretation
Sans graphe, une analyse de la contribution des phases et des matériaux aux émissions de GES.
Pas d'analyse d'incertitudes, qui sont même mises de côtés car similaires dans les scénarios comparés...
PAs d'analyse de sensibilité.

### Réflexion sur mon modèle

A la lecture de Papageorgiu et al, 2024, il me semble pertinent de revenir sur une comparaison des résultats énergie qu'on aurait au ratio, energyplus et relevés, et/ou statistiques d'échelle supérieur, non plus côté conso mais côté producteur haute-tension (RTE). 
Par ailleurs, on pourrait pour avoir des ratios pas ayant un sens, on pourrait prendre des stats par IRIS, selectionner l'IRIS qui ressemble le plus au programme, dans le même climat et regarder les consos à cette échelle. Leur appliquer un facteur pour prendre en compte une meilleure isolation. Si l'on obtient plusieurs IRIS ressemblants, on pourrait considérer une distribution pour ce ratio avec une distribution uniforme entre  les minimum et maximum.

## 25 août 2025

### Lecture articles

#### Dorra et al, 2022

Introduction claire sur une différence entre évaluation territorial-based et consumption-based qui demande à être précis sur les limites du système.

##### Objectifs et périmètre
L'objectif de l'ACV réalisée est de quantifier l'impact des secteurs du bâtiment résidentiel, de la consommation alimentaire et de la mobilité quotidienne à l'échelle de la ville et d'évaluer les mesures d'atténuation considérées par la personne publique. 

##### Méthode de construction d'inventaire 
Pour la nourriture, des ratios dépendants de l'âge, du genre et du niveau d'éducation (le sien ou celui des parents) sont appliqués aux populations du cas d'étude. Pour les bâtiments, 14 archétypes ont été modélisés sur Pleiades et les bâtiments de la ville ont été associés à ces derniers par proximité des propriétés thermiques. La durée de vie considérée est de 100 ans Pour les transports, à partir de modèles utilisant des données d'usage des sols et de trafic, les distances parcourues sur une zone du territoire par les habitants pour un mode donnée sont calculées.

##### Méthode de caractérisation
Douze catégories d'impacts issues de CML2001, deux d'EDIP 2003 et deux endpoints d'eco-indicator 99.


##### Démarches d'interpretation
Les résultats obtenus, notamment venant de la simulation énergétiques sont agrégés à l'échelle de la commune et comparés à des statistiques communales.
Des analyses de contribution sont réalisées : des secteurs aux indicateurs de changement climatique (44% nourriture, 34% bâtiments, 22% mobilité) de déchets, d'usage des sols (que alimentation) et d'utilisation d'énergie (60% bâtiments, 25% alimentation,15% mobilité) ; des catégories d'aliments et de boissons à la masse de l'inventaire et à l'indicateur de changement climatique.
Des scénarios de réduction d'impacts sont modélisés (DSA) sur chacun des secteurs, les scénarios pouvant appliquer plusieurs paramètres des modèles (isolation des façades par exemple).
Pas de mention des incertitudes.







 



