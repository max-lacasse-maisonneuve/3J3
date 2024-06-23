# Cinemachine

Cinemachine est un système de caméra qui permet de créer des mouvements de caméra complexes et réalistes. Il est très utilisé dans les jeux vidéo pour créer des cinématiques ou des mouvements de caméra dynamiques.

## Installation de Cinemachine

Pour installer Cinemachine dans votre projet Unity, il suffit de passer par le Package Manager. Pour cela, suivez les étapes suivantes :

1. Ouvrez le Package Manager en allant dans `Window > Package Manager`.
2. Sélectionnez Packages: `Unity Registry` dans le menu déroulant en haut de la fenêtre.
3. Recherchez Cinemachine dans la barre de recherche.
4. Cliquez sur le bouton `Install` pour installer Cinemachine dans votre projet.

## Utilisation de Cinemachine

Une fois Cinemachine installé dans votre projet, vous pouvez commencer à l'utiliser pour créer des mouvements de caméra. Voici quelques étapes pour vous aider à démarrer :

1. Créez une nouvelle caméra dans votre scène en cliquant sur `GameObject > Camera > Cinemachine FreeLook`. Par défaut, la caméra principale de la scène aura un composant `CinemachineBrain` attaché qui permet de contrôler la caméra Cinemachine.
2. Sélectionnez la caméra Cinemachine que vous venez de créer dans la hiérarchie.
3. Dans l'inspecteur, vous verrez plusieurs paramètres que vous pouvez ajuster pour configurer le mouvement de la caméra. Par exemple, vous pouvez régler la vitesse de rotation, la sensibilité de la souris, etc.
4. Pour contrôler la caméra à l'aide d'un script, utilisez le composant `CinemachineBrain`qui est sur la caméra principale de la scène. Vous pouvez accéder à ce composant en utilisant la méthode `CinemachineBrain.GetMainCamera()`.

Avec Cinemachine, vous pouvez créer des mouvements de caméra complexes, des transitions fluides entre différentes caméras, des effets de post-traitement, etc. C'est un outil puissant pour créer des cinématiques et des mouvements de caméra immersifs dans vos jeux.
