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







