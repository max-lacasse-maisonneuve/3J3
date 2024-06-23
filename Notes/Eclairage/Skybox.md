# Skybox

Un skybox est une technique de rendu 3D qui permet de simuler un environnement lointain, comme un ciel ou des montagnes, sans avoir à les modéliser en 3D. Cela permet de donner l'illusion que le joueur est dans un environnement plus grand qu'il ne l'est réellement.

## Créer un skybox avec un hdri

Pour créer un skybox avec un hdri, suivez ces étapes :

1. Téléchargez un hdri de qualité sur un site spécialisé. Ex: [HDRI Haven](https://hdrihaven.com/).

2. Importez le hdri dans votre projet Unity.

3. Créez un nouveau matériau et appliquez le hdri comme texture. Modifiez les paramètres du matériau pour qu'il soit utilisé comme skybox en changeant le shader de `Standard` à `Skybox/Panoramic`.

4. Créez un nouveau skybox dans votre scène et appliquez le matériau que vous venez de créer. Create > Rendering > Skybox.

5. Modifiez les paramètres du skybox pour ajuster l'intensité, la rotation, la taille, etc. du hdri.

6. Dans le menu Window -> Rendering -> Lighting, dans l'onglet environnement, sélectionnez le skybox que vous venez de créer.
   La scène sera maintenant éclairée par le skybox que vous avez créé.
