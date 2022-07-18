# Data cleanup

Une étape fondamentale après l'obtention du fichier CSV est celle du nettoyage et de l'enrichissement du fichier. En effet, à partir du fichier TEI transformé en CSV, seules quelques colonnes sont remplies dans le tableur conçu pour les catalogues d'exposition de la base de données BasArt.  &#x20;

![Extrait du fichier CSV tel qu'il est généré à partir du fichier TEI](../.gitbook/assets/csvexemple.png)

Il fallait donc déconcatener certaines informations (noms, prénoms, adresses, ville, pays, sociétés photographiques auxquelles appartiennent les exposants) et les répartir dans les colonnes appropriées. De nombreuses informations issues des catalogues se trouvaient sous la forme d'abbréviations ou de sigles (sociétés photographiques et procédés photographiques employés pour réaliser les épreuves) qu'il fallait retranscrire entièrement pour faciliter leur compréhension. Lorsque les informations concernant les villes et les pays de résidence des exposants étaient absentes, il fallait également les compléter afin de permettre un géoréférencement le plus exhaustif possible. Nous avons également renseigné le sexe des exposants dans la mesure où il était possible de le connaître grâce au prénom et aux mentions de civilités. Lorsqu'il n'était pas possible, malgré quelques recherches, de déduire le sexe de l'exposant, nous ne l'avons pas renseigné. &#x20;

![Extrait du fichier CSV enrichi sur OpenRefine](../.gitbook/assets/openrefine.png)

* list of operations, transformations and data additions (déconcaténer nom, bio, adresse, pays, villes, reconciliation, géoréférencement, genre...)
