# Créer une mini-map dans Unity

Dans ce tutoriel, nous allons voir comment créer une mini-map dans Unity. Une mini-map est une petite carte qui permet de visualiser l'environnement du jeu et la position du joueur. Elle est souvent utilisée dans les jeux d'aventure, les jeux de stratégie ou les jeux de course pour aider le joueur à se repérer dans l'univers du jeu.

## Créer une caméra pour la mini-map

La première étape pour créer une mini-map est de créer une caméra qui affichera la vue de la mini-map. Pour cela, créez une nouvelle caméra dans la scène en cliquant sur **GameObject > Camera**. Placez la caméra en hauteur pour avoir une vue aérienne de la scène. Le mode de projection de la caméra doit être **Orthographic** pour avoir une vue en 2D de la scène.

## Créer une texture pour la mini-map

Ensuite, créez une nouvelle texture pour la mini-map en cliquant sur **Assets > Create > Render Texture**. Donnez un nom à la texture, par exemple "MiniMapTexture". Configurez la taille de la texture en fonction de la résolution de la mini-map que vous souhaitez afficher. Par exemple, une résolution de 256x256 pixels est souvent utilisée pour les mini-maps.

## Configurer la caméra pour afficher la texture de la mini-map

Sélectionnez la caméra que vous avez créée pour la mini-map. Dans les propriétés de la caméra, recherchez le champ **Target Texture** et assignez-lui la texture que vous avez créée pour la mini-map. La caméra affichera maintenant la vue de la mini-map dans la texture.

## Afficher la texture de la mini-map dans l'interface

Pour afficher la texture de la mini-map dans l'interface du jeu, créez un nouveau Canvas en cliquant sur **GameObject > UI > Canvas**. Créez un nouvel objet UI de type Raw Image en cliquant sur **GameObject > UI > Raw Image**. Assignez la texture de la mini-map à la propriété **Texture** de l'objet Raw Image. Redimensionnez et positionnez l'objet Raw Image pour qu'il affiche la mini-map à l'endroit souhaité dans l'interface.

## Suivre la position du joueur sur la mini-map

Pour suivre la position du joueur sur la mini-map, créez un nouvel objet UI de type Image en cliquant sur **GameObject > UI > Image**. Assignez une image à l'objet Image pour représenter le joueur sur la mini-map. Créez un script pour mettre à jour la position de l'objet Image en fonction de la position du joueur dans la scène. Par exemple, vous pouvez utiliser le script suivant :

```csharp

using UnityEngine;

public class MiniMap : MonoBehaviour
{
    public Transform player;
    public RectTransform playerIcon;

    void Update()
    {
        playerIcon.anchoredPosition = new Vector2(player.position.x, player.position.z);
    }
}
```

Attachez ce script à l'objet Image représentant le joueur sur la mini-map. Assignez le transform du joueur à la propriété **player** du script et le RectTransform de l'objet Image à la propriété **playerIcon**. L'objet Image suivra maintenant la position du joueur sur la mini-map.
