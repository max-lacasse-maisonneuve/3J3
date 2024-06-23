# Post-processing et effets visuels

Le post-processing est une technique utilisée dans les jeux vidéo pour appliquer des effets visuels à une scène après qu'elle a été rendue. Ces effets peuvent inclure des filtres de couleur, des effets de flou, des effets de distorsion, des effets de lumière, des effets de particules, etc. Le post-processing est généralement utilisé pour améliorer l'apparence visuelle d'un jeu en ajoutant des détails et des effets visuels supplémentaires.

## Ajouter un post-processing à une scène

Pour ajouter un post-processing à une scène dans Unity, vous pouvez utiliser le package Post Processing Stack V2. Par défaut, Unity ne prend pas en charge le post-processing, mais vous pouvez télécharger et importer le package Post Processing Stack V2 à partir de la fenêtre Package Manager pour ajouter cette fonctionnalité à votre projet.

Si vous avez démarré un nouveau projet en utilisant le template "High Definition RP" ou "Universal RP", le package Post Processing Stack V2 est déjà inclus dans votre projet. Vous pouvez activer le post-processing en ajoutant un composant Post Process Volume à votre scène et en configurant les effets visuels que vous souhaitez appliquer.

## Configurer les effets visuels

Ajoutez un objet vide à votre scène et ajoutez un composant Post Process Volume à cet objet. Le composant se trouve dans le menu "Component > Rendering > Post Process Volume".

Créez ensuite un nouveau profil de post-processing en cliquant sur le bouton "New" dans le composant Post Process Volume. Vous pouvez ensuite configurer les différents effets visuels en ajoutant des effets à la pile d'effets visuels du profil.

Pour que les effets soient pris en charge, vous devez également ajouter un composant Post Process Layer à votre caméra et assigner le profil de post-processing que vous avez créé au composant Post Process Layer. De plus, assurez-vous que le layer de la caméra est correctement configuré pour inclure les objets que vous souhaitez affecter avec les effets visuels.
