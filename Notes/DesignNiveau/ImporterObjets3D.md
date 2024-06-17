# Importer des objets 3D dans Unity

Unity permet d'importer des objets 3D dans un projet. Ces objets peuvent être des modèles 3D, des animations, des textures, des matériaux, etc. Ces objets peuvent être importés dans Unity à partir de fichiers créés dans des logiciels de modélisation 3D tels que Blender, 3DS Max, Maya, etc.

Pour que les textures et animations soient importées correctement dans Unity, il est important de respecter certaines règles lors de l'importation des objets 3D. Voici quelques conseils pour importer des objets 3D dans Unity :

1. **Appliquer les transformations** : Avant d'exporter l'objet 3D depuis le logiciel de modélisation 3D, il est important d'appliquer les transformations (rotation, échelle, position) de l'objet pour éviter les problèmes d'orientation ou d'échelle lors de l'importation dans Unity.

Par exemple, dans Blender, il est recommandé d'appliquer la rotation et l'échelle de l'objet en appuyant sur `Ctrl + A` et en sélectionnant "Rotation & Scale" dans le menu contextuel. Dans Maya, il est recommandé d'appliquer les transformations en sélectionnant l'objet, puis en allant dans `Modify > Freeze Transformations` dans le menu.

2. **Organiser les fichiers de l'objet 3D** : Avant d'importer l'objet 3D dans Unity, il est important d'organiser les fichiers de l'objet 3D de manière à ce que les textures, les matériaux, les animations, etc. soient correctement associés à l'objet principal.

Placer l'objet dans un élément vide qui sera le parent _root_ de l'objet 3D pour faciliter l'organisation des éléments dans Unity.

3. **Baker les textures** : Pour réduire le nombre de textures et améliorer les performances du jeu, il est recommandé de "baker" les textures de l'objet 3D avant de l'importer dans Unity. Cela consiste à fusionner les textures en une seule texture pour réduire la charge sur le processeur et la carte graphique.

4. **Exporter l'objet 3D dans un format compatible avec Unity** : Unity prend en charge plusieurs formats de fichiers 3D tels que FBX, OBJ, 3DS, DAE, etc. Il est recommandé d'exporter l'objet 3D dans l'un de ces formats pour une compatibilité maximale avec Unity.

Le format FBX est généralement le plus recommandé pour l'importation d'objets 3D dans Unity car il prend en charge les textures, les animations, les matériaux, etc.

4. **Paramétrer les options d'importation** : Lors de l'importation de l'objet 3D dans Unity, il est possible de paramétrer différentes options telles que l'échelle de l'objet, l'unité de mesure, les animations à importer, etc. Il est recommandé de vérifier et de paramétrer ces options en fonction des besoins du projet. Assurez-vous également de cocher les options d'importation des textures et des matériaux si nécessaire.

À titre d'exemple, une unité de mesure de 1 unité = 1 mètre est généralement recommandée pour une bonne échelle des objets dans Unity. Dans Maya, cette unité de mesure correspond à 1 unité = 1 cm. Dans Blender, cette unité de mesure correspond à 1 unité = 1 mètre.

L'axe de rotation peut également être différent entre les logiciels de modélisation 3D et Unity. Par exemple, dans Blender, l'axe de rotation par défaut est Z, tandis que dans Unity, l'axe de rotation par défaut est Y. Il est donc important de vérifier et de paramétrer l'axe de rotation correctement lors de l'importation de l'objet 3D dans Unity.

5. **Vérifier les textures et les matériaux** : Après l'importation de l'objet 3D dans Unity, il est important de vérifier que les textures et les matériaux sont correctement importés et associés à l'objet principal. Il est possible que certaines textures ou matériaux ne s'affichent pas correctement dans Unity en raison de problèmes de compatibilité ou de paramétrage incorrect. Cliquez sur "unpack materials" pour décompresser les matériaux.

6. **Déboguer les textures** : Réassocier les textures et les matériaux si nécessaire : Si les textures ou les matériaux ne sont pas correctement importés ou associés à l'objet principal, il est possible de les réassocier manuellement dans Unity en les faisant glisser et en les déposant sur l'objet.

7. **Optimiser les objets 3D** : Pour améliorer les performances du jeu, il est recommandé d'optimiser les objets 3D importés dans Unity. Cela peut inclure la réduction du nombre de polygones, la simplification des textures, l'utilisation de LODs (Levels of Detail), etc. Pour le jeu avec beaucoup d'éléments sur la scène, il est recommandé d'utiliser des LODs pour les objets 3D afin de réduire la charge sur le processeur et la carte graphique et d'avoir un maximum de 3000 à 5000 polygones par objet détaillé.
