# Détection de la souris et du clavier dans un environnement 3D

Dans un jeu en 3D, il est souvent nécessaire de détecter les mouvements de la souris et les touches du clavier pour permettre au joueur d'interagir avec l'environnement. Unity offre plusieurs moyens de détecter ces interactions et de les utiliser pour contrôler les objets du jeu.

## Détection des mouvements et du clic de la souris

Pour détecter les mouvements de la souris et le clic de la souris dans Unity, il est possible d'utiliser les méthodes `Input.GetAxis` et `Input.GetMouseButtonDown`. Il faut ensuite convertir la position sur l'écran en une position dans l'espace 3D pour pouvoir interagir avec les objets du jeu en utilsant Camera.ScreenToWorldPoint.

```csharp

using UnityEngine;

public class MouseController : MonoBehaviour
{
    public Camera mainCamera;

    void Update()
    {
        // Détection du clic de la souris
        if (Input.GetMouseButtonDown(0))
        {
            // Conversion de la position de la souris en une position dans l'espace 3D
            Vector3 mousePosition = Input.mousePosition;
            mousePosition.z = mainCamera.nearClipPlane;//distance de la caméra
            Vector3 worldPosition = mainCamera.ScreenToWorldPoint(mousePosition);

            // Affichage de la position dans la console
            Debug.Log("Mouse position: " + worldPosition);
        }

        // Détection du mouvement de la souris
        float mouseX = Input.GetAxis("Mouse X");
        float mouseY = Input.GetAxis("Mouse Y");

        // Affichage du mouvement de la souris dans la console
        Debug.Log("Mouse movement: " + mouseX + ", " + mouseY);
    }
}
```

## Détection d'un clic sur un objet 3d

Pour détecter un clic sur un objet 3D dans Unity, il est possible d'utiliser un raycast. Le raycast permet de détecter les collisions entre un rayon et les objets de la scène. Cela permet de déterminer si un objet est touché par un rayon et d'obtenir des informations sur l'objet touché, comme sa position, sa normale, sa distance, etc.

```csharp

using UnityEngine;

public class ObjectClick : MonoBehaviour
{
    public Camera mainCamera;

    void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            Ray ray = mainCamera.ScreenPointToRay(Input.mousePosition);
            RaycastHit hit;

            if (Physics.Raycast(ray, out hit))
            {
                // Affichage du nom de l'objet touché dans la console
                Debug.Log("Object clicked: " + hit.collider.name);
            }
        }
    }
}
```

Dans cet exemple, nous utilisons un raycast pour détecter si un objet est touché par un clic de souris. Si un objet est touché, nous affichons son nom dans la console.

## Détection d'un survol d'objet 3d avec le curseur

Pour détecter le survol d'un objet 3D avec le curseur dans Unity, il est possible d'utiliser un raycast. Le raycast permet de détecter les collisions entre un rayon et les objets de la scène. Cela permet de déterminer si un objet est touché par un rayon et d'obtenir des informations sur l'objet touché, comme sa position, sa normale, sa distance, etc.

À noter que le raycast est effectué à chaque frame pour détecter le survol de l'objet par le curseur et que le rayon est généré à partir de la position du curseur sur l'écran.

```csharp

using UnityEngine;

public class ObjectHover : MonoBehaviour
{
    public Camera mainCamera;

    void Update()
    {
        Ray ray = mainCamera.ScreenPointToRay(Input.mousePosition);
        RaycastHit hit;

        if (Physics.Raycast(ray, out hit))
        {
            // Affichage du nom de l'objet survolé dans la console
            Debug.Log("Object hovered: " + hit.collider.name);
        }
    }
}
```
## Modifier l'icône du curseur

Pour modifier l'icône du curseur lorsque celui-ci survole un objet 3D dans Unity, il est possible d'utiliser la méthode `Cursor.SetCursor`. Cette méthode permet de définir une texture pour l'icône du curseur et de spécifier la position du point chaud de l'icône (le point qui est considéré comme le pointeur du curseur).
le cursorMode permet de définir le mode du curseur, il peut prendre les valeurs suivantes:
- Auto: le curseur est affiché normalement
- ForceSoftware: le curseur est affiché en mode logiciel
- ForceHardware: le curseur est affiché en mode matériel

```csharp

using UnityEngine;

public class CursorChange : MonoBehaviour
{
    public Texture2D cursorTexture;
    public Vector2 hotSpot = Vector2.zero;

    void Start()
    {
        Cursor.SetCursor(cursorTexture, hotSpot, CursorMode.Auto);
    }
}
```

## Détection des touches du clavier

Pour détecter les touches du clavier dans Unity, il est possible d'utiliser la méthode `Input.GetKeyDown`. Cette méthode permet de détecter si une touche du clavier est enfoncée à un instant donné. Il est également possible d'utiliser `Input.GetKey` pour détecter si une touche est maintenue enfoncée. Aussi, il est possible de détecter si une touche est relâchée en utilisant `Input.GetKeyUp`.

De plus, pour éviter d'avoir à se souvenirs des codes des touches, il est possible d'utiliser les codes des touches prédéfinis dans la classe `KeyCode`.

À noter que les touches du clavier sont détectées dans la méthode `Update` du script et que getKey est appelée à chaque frame donc il faut faire attention à ne pas surcharger la méthode Update avec trop de détections de touches.
Prévilégier l'utilisation de `GetKeyDown` ou `GetKeyUp` pour les actions qui ne doivent être déclenchées qu'une seule fois.

```csharp

using UnityEngine;

public class KeyboardController : MonoBehaviour
{
    void Update()
    {
        // Détection de l'appui sur la touche E
        if (Input.GetKeyDown(KeyCode.E))
        {
            Debug.Log("Key E pressed");
        }

        // Détection du maintien de la touche W
        if (Input.GetKey(KeyCode.W))
        {
            Debug.Log("Key W held down");
        }

        // Détection du relâchement de la touche Q
        if (Input.GetKeyUp(KeyCode.Q))
        {
            Debug.Log("Key Q released");
        }
    }
}
```
