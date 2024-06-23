# Raycast

Le raycast est une technique utilisée dans les moteurs de jeu pour détecter les collisions entre un rayon et les objets de la scène. Cela permet de déterminer si un objet est touché par un rayon et d'obtenir des informations sur l'objet touché, comme sa position, sa normale, sa distance, etc.

Cela est pratique pour savoir si un personnage touche au sol ou si la caméra est bloquée par un mur.

## Utilisation du Raycast

Pour utiliser le raycast dans Unity, il faut utiliser la méthode `Physics.Raycast` qui prend en paramètre l'origine du rayon, sa direction, sa longueur et un masque de collision pour déterminer quels objets sont touchés par le rayon.

On passe en paramètre un `RaycastHit` qui contiendra les informations sur l'objet touché si le rayon touche un objet.

À noter que le raycast ne détecte que les collisions avec les objets qui ont un collider.

Voici un exemple de script qui utilise le raycast pour détecter si un objet est touché par un rayon :

```csharp

using UnityEngine;

public class RaycastExample : MonoBehaviour
{
    public Transform origin;
    public Vector3 direction;
    public float distance;

    void Update()
    {
        RaycastHit hit;
        //Cherche uniquement les objets sur le layer "Default"
        LayerMask mask = LayerMask.GetMask("Default");

        if (Physics.Raycast(origin.position, direction, out hit, distance, mask))
        {
            Debug.Log("Object hit: " + hit.collider.name);
            Debug.Log("Hit point: " + hit.point);
            Debug.Log("Hit normal: " + hit.normal);
            Debug.Log("Hit distance: " + hit.distance);
        }
    }
}

```

