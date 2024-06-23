# Types d'éclairages

Dans unity, il existe plusieurs types d'éclairages. Chacun a ses avantages et inconvénients. Voici une liste des types d'éclairages les plus courants :

-   **Directional Light** : C'est une lumière qui émet de la lumière dans une direction donnée. Elle est souvent utilisée pour simuler la lumière du soleil. Elle n'a pas de position, seulement une direction. Elle éclaire tous les objets de la scène de la même manière, quelle que soit leur position.

-   **Point Light** : C'est une lumière qui émet de la lumière dans toutes les directions à partir d'un point donné. Elle est souvent utilisée pour simuler des sources de lumière ponctuelles, comme des lampes ou des bougies. Elle éclaire les objets de la scène en fonction de leur distance par rapport à la lumière.

-   **Spot Light** : C'est une lumière qui émet de la lumière dans une direction donnée à partir d'un point donné. Elle est souvent utilisée pour simuler des projecteurs ou des phares. Elle éclaire les objets de la scène en fonction de leur distance par rapport à la lumière et de leur angle par rapport à la direction de la lumière.

-   **Area Light** : C'est une lumière qui émet de la lumière dans toutes les directions à partir d'une surface donnée. Elle est souvent utilisée pour simuler des sources de lumière étendues, comme des fenêtres ou des écrans. Elle éclaire les objets de la scène en fonction de leur distance par rapport à la surface de la lumière et de leur angle par rapport à la surface de la lumière.

## Créer un éclairage

Pour créer un éclairage dans unity, vous pouvez utiliser l'option "GameObject > Light" dans le menu principal. Cela ajoutera un nouvel objet lumière à votre scène. Vous pouvez ensuite modifier les propriétés de l'éclairage dans l'inspecteur pour ajuster sa couleur, son intensité, sa portée, etc.

## Matériel éclairant

Pour que les objets de votre scène soient éclairés par une lumière, ils doivent avoir un matériau éclairant. Vous pouvez créer un matériau éclairant en utilisant l'option "Assets > Create > Material" dans le menu principal. En ajoutant la propriété emissive à votre matériau, vous pouvez spécifier la couleur et l'intensité de la lumière qu'il émet. Pour accentuer l'effet, parentez une spot light à un objet émissif.

Combiné avec la propriété bloom du post-processing, vous pouvez créer des effets lumineux très intéressants dans votre jeu.
