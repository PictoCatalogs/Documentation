# Workflow

![](<../.gitbook/assets/Untitled Diagram.drawio-2.png>)

Cette chaîne de traitement a été développée dans le cadre du projet [Artl@s](https://artlas.huma-num.fr/fr/), en particulier pour [BasArt](https://artlas.huma-num.fr/map/#/), sa base numérique et géoréférencée de catalogues d'expositions. Ce workflow est le fruit du travail de [Caroline Corbières](https://github.com/carolinecorbieres/ArtlasCatalogues) et de [Juliette Janès](https://github.com/Juliettejns/Memoire\_TNAH), qui ont apportés des améliorations successives dans le but d'extraire les données de catalogues d'exposition de façon semi-automatisée ([plus d'informations ici](https://hal.archives-ouvertes.fr/hal-03331838/document)).&#x20;

Nos données de départ sont des catalogues d'expositions disponibles au format IIIF, permettant de les importer très facilement dans [FoNDUE](https://github.com/FoNDUE-HTR), infrastructure d'HTR (Handwritten Text Recognition) développée par l'Université de Genève basée sur [eScriptorium](https://escriptorium.fr). Les données d'HTR et de segmentation issues des pages d'un catalogue sont ensuite exportées au format XML ALTO (Analysed Layout and Text Object).&#x20;

Un programme en Python développé par Juliette Janès et grandement amélioré par Esteban Sánchez Oeconomo (le programme mis à jour est[ disponible ici](https://github.com/IMAGO-Catalogues-Jjanes/extractionCatalogs)), permet ensuite d'extraire de manière automatisée les données textuelles et de mise en page des fichiers ALTO et de les structurer en XML TEI (Text Encoding Initiative). Une [feuille de transformation XSLT](https://github.com/carolinecorbieres/ArtlasCatalogues/tree/master/6\_TEItoCSV) (eXtensible Stylesheet Language Transformations_)_ permet enfin de transposer ces données structurées dans un fichier CSV (Comma-Separated Values), afin d'obtenir des données sous la forme d'un tableur adapté aux besoins de BaseArt.&#x20;

Les données contenues dans le fichier CSV sont ensuite nettoyés et enrichis grâce à [OpenRefine](https://openrefine.org), afin de répartir les données dans les colonnes correspondantes mais aussi de géoréférencer l'ensemble des données géographiques disponibles. A partir d'un CSV enrichi, il est alors possible de réaliser des visualisations de différentes natures (cartographies, graphiques, etc.) et ainsi de procéder à l'analyse les données issues des catalogues.&#x20;

Bien que nous renvoyions systématiquement dans cette documentation aux différents travaux qui composent notre chaîne de traitement, les différents fichiers nécessaires entrant en jeu dans cette dernière ont également été centralisés dans un dépôt GitHub dédié (_**lien à ajouter**_) afin de faciliter leur récupération par toute personne susceptible de les réemployer. &#x20;

Les pages suivantes détailleront davantage chaque étape de cette chaîne de traitement.&#x20;
