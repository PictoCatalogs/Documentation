# HTR et Layout Analysis

La première étape du traitement de notre corpus correspond à la transcription et la segmentation des pages de catalogues.

### FoNDUE&#x20;

Cette étape a été réalisée au moyen de [FoNDUE](https://github.com/FoNDUE-HTR), infrastructure d'HTR développée par l'Université de Genève basée sur [eScriptorium](https://escriptorium.fr). L'interface graphique facilite grandement les opérations. La transcription et la segmentation peuvent être réalisée entièrement manuellement ou être facilitée par l'usage de modèles entrainés. FoNDUE propose des modèles par défaut et permet d'entraîner ses propres modèles à partir de pages déjà traitées. Juliette Janès a également mis à disposition des [modèles](https://github.com/IMAGO-Catalogues-Jjanes/cataloguesSegmentationOCR/tree/eae51756eb24a6d0f431b9946389f4651446284d/4\_Models) entrainés à partir des catalogues qu'elle a traité au cours de son travail.&#x20;

La segmentation (ou layout analysis) permet d'identifier et décrire les différentes zones d'un document manuscrit ou imprimé. Cette opération connait de nombreuses applications en terme d'analyses computationnelles. Dans le cas précis du traitement des catalogues d'exposition, documents semi-structurés sous la forme d'entrées, la segmentation permet en particulier d'identifier les zones d'une page correspondant aux différentes entrées. La structure des entrées peut varier selon les catalogues, mais dans notre cas elle contient des informations factuelles concernant chaque exposant et chaque oeuvres exposées par ce dernier.&#x20;

La segmentation est, avec la transcription, essentielle dans la chaîne de traitement des catalogues car ces différentes informations seront contenues dans les fichiers XML ALTO générés par FoNDUE pour chaque page du catalogue traité. C'est ce qui permettra ensuite au programme Python de d'extraire automatiquement les données correspondant aux exposants et oeuvres exposées sous forme structurée en XML TEI.

![Capture d'écran de l'interface FoNDUE lors du traitement d'une page de catalogue](<../.gitbook/assets/fondue (1).png>)

### SegmOnto, vocabulaire controlé

Dans le cadre de la segmentation d'un document, il est important de définir et respecter un vocabulaire qui permettra de décrire chaque zone d'une page selon sa fonction. Afin de favoriser l'interopérabilité des données obtenues, nous avons adopté le vocabulaire controlé [SegmOnto](https://segmonto.github.io).&#x20;

**Les zones utilisées sont les suivantes :**&#x20;

* `MainZone`
* `NumberingZone`
* `MarginTextZone`
* `NumberingZone`
* `QuireMarksZone`
* `TitlePageZone`
* `GraphicZone:illustration`
* `GraphicZone:ornamentation`
* `CustomZone:entry`
* `CustomZone:entryEnd`

**Les lignes utilisées sont les suivantes :**&#x20;

* `DefaultLine`
* `HeadingLine`
*   `CustomLine`



### HTR-United et modèles&#x20;

* sharing groundtruth (HTR United)
* sharing models
