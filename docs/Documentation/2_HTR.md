# HTR et Layout Analysis

La première étape du traitement de notre corpus correspond à la transcription et la segmentation des pages de catalogues.

### FoNDUE&#x20;

Cette étape a été réalisée au moyen de [FoNDUE](https://github.com/FoNDUE-HTR), infrastructure d'HTR développée par l'Université de Genève basée sur [eScriptorium](https://escriptorium.fr). L'interface graphique facilite grandement les opérations d'acquisition et de correction. La transcription et la segmentation peuvent être réalisées entièrement manuellement ou être facilitées par l'usage de modèles entrainés. FoNDUE propose des modèles de transcription et de segmentation par défaut mais permet aussi d'importer d'autres modèles ainsi que d'entraîner ses propres modèles à partir de pages déjà traitées.&#x20;

La segmentation (ou layout analysis) permet d'identifier et décrire les différentes zones d'un document manuscrit ou imprimé. Cette opération connait de nombreuses applications en terme d'analyses computationnelles. Dans le cas précis du traitement des catalogues d'exposition, documents semi-structurés sous la forme d'entrées, la segmentation permet en particulier d'identifier les zones d'une page correspondant aux différentes entrées. La structure des entrées peut varier selon les catalogues, mais dans notre cas elle contient des informations factuelles concernant chaque exposant et chaque oeuvres exposées par ce dernier.&#x20;

La segmentation est, avec la transcription, essentielle dans la chaîne de traitement des catalogues car ces différentes informations seront contenues dans les fichiers XML ALTO générés par FoNDUE pour chaque page du catalogue traité. C'est ce qui permettra ensuite au programme Python de d'extraire automatiquement les données correspondant aux exposants et oeuvres exposées sous forme structurée en XML TEI.

![Interface FoNDUE-eScriptorium lors du traitement d'une page de catalogue](<../.gitbook/assets/fondue (1).png>)

### SegmOnto, vocabulaire controlé

Dans le cadre de la segmentation d'un document, il est important de définir et respecter un vocabulaire qui permettra d'annoter et décrire chaque zone d'une page selon sa fonction. Nous avons adopté le vocabulaire controlé [SegmOnto](https://segmonto.github.io) afin de favoriser l'interopérabilité des données obtenues, notamment dans la perspective d'une mutualisation de la vérité de terrain et de l'entraînement de nouveaux modèles.

**Les zones utilisées pour l'annotation de notre corpus sont les suivantes :**&#x20;

* `MainZone`:  pour la zone contenant l'ensemble du texte d'une page.
* `NumberingZone`:  pour la numérotation des pages.
* `MarginTextZone` :  pour les légendes des illustrations.&#x20;
* `QuireMarksZone`:  pour les numéros de cahier.&#x20;
* `TitlePageZone`:  pour la ou les pages de titre.&#x20;
* `GraphicZone:illustration`: pour les illustrations.&#x20;
* `GraphicZone:ornamentation`: pour les ornements typographiques.&#x20;
* `CustomZone:entry`: pour les entrées de catalogue.&#x20;
* `CustomZone:entryEnd`: pour les entrées qui se poursuivent sur la page suivante (rares dans notre corpus).&#x20;

`CustomZone` est une type à utiliser pour toute zone autre que celles définies par SegmOnto, elle permet à ce vocabulaire controlé de s'adapter à une typologie de document spécifique grâce à l'ajout d'un sous-type librement choisi par l'utilisateur. Dans le cas des catalogues, les sous-types retenus sont `entry` et `entryEnd`. L'usage de `CustomZone:entry` et `CustomZone:entryEnd` pour la segmentation est particulièrement importante dans le cadre de la chaîne de traitement appliquée aux catalogues, ce sont ces zones qui permettront de délimiter et extraire les données concernant les items exposés et leurs exposants.&#x20;

**Les lignes utilisées pour l'annotation de notre corpus sont les suivantes :**&#x20;

* `HeadingLine`: pour les lignes contenant un élément de titre.&#x20;
* `DefaultLine`: pour le reste des lignes du document.&#x20;

![](../.gitbook/assets/fondue2.png)

Dans l'exemple ci-dessus, la zone orange est une `NumberingZone`, la zone rose une `MainZone` et les zones bleues des `CustomZone:entry`. Les lignes sont ici toutes des `DefaultLine`.&#x20;

### Modèles d'entrainement et vérité de terrain.&#x20;

Juliette Janès a également mis à disposition des [modèles](https://github.com/IMAGO-Catalogues-Jjanes/cataloguesSegmentationOCR/tree/eae51756eb24a6d0f431b9946389f4651446284d/4\_Models) entrainés à partir des catalogues qu'elle a traité au cours de son travail. Le plus performant sur notre corpus était le modèle de transcription "Gruyère". Les données à partir desquelles ont été entrainés ces différents modèles n'étant pas natives d'eScriptorium, car préparées à l'origine grâce à Transkribus, les résultats obtenus lors d'un usage du modèle sur eScriptorium demande encore énormément de corrections. De nouveaux modèles ont été entraînés avec des pages de notre corpus grâce à FoNDUE, mais n'ayant été entrainés que sur un nombre limité de pages toutes semblables, ils ne sont vraisemblablement performants que pour les catalogues de notre corpus.&#x20;

Un entraînement sur FoNDUE ne permet de selectionner que les pages d'un seul document comme vérité de terrain. Pour procéder à un entraînement sur un nombre plus important de documents présentant une plus grande variété, il faut utiliser directement un outil d'HTR tel que [Kraken](https://kraken.re/master/index.html) (logiciel OpenSource sur lequel s'appuient eScriptorium et FoNDUE). Cependant, un ordinateur personnel n'offre pas la puissance nécessaire pour réaliser efficacement un tel entraînement, en particulier concernant des modèles de segmentation.&#x20;

L'ensemble des données issues de la transcription et la segmentation réalisées dans le cadre de ce projet de recherche représente une vérité de terrain suffisamment importante en terme de quantité pour entraîner de nouveaux modèles plus performants pour les catalogues historiques. A ces données s'ajoutent celles mises à disposition par Juliette Janès à l'issue de son travail, lesquelles ont été transformées par nos soins pour être conformes à la nouvelle version de SegmOnto. Esteban Sánchez Oeconomo et Paul Kervegan ont également contribué à augmenter cette vérité de terrain avec l'ajout de données issues d'autres catalogues. Ces jeux de données (fichiers ALTO et images correspondantes) sont disponibles sur le [dépôt GitHub](https://github.com/PictoCatalogs/TrainingDataOCR) du projet PictoCatalogs et pourront servir à l'entraînement de nouveaux modèles d'HTR et de segmentation pour des catalogues de différentes natures.&#x20;

Ce dépôt GitHub intègre différentes GitHub actions visant à automatiser le controle qualité des données partagées sur le dépôt et la compatibilité avec l'initiative [HTR-United](https://htr-united.github.io/index.html#top). HTR-United vise à [mutualiser la vérité de terrain](https://hal.archives-ouvertes.fr/hal-03398740) issues de différents projets de recherche. Il s'agit de favoriser ainsi le décloisonnement des ressources, en particulier pour l'entraînement de nouveaux modèles de transcription automatique grâce à une verité de terrain de qualité et couvrant une grande variété de documents et de période historique.&#x20;

