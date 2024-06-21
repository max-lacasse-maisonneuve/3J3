# Physique dans Unity

La physique est un aspect important de la programmation de jeux vidéo. Unity propose un moteur physique complet qui permet de simuler des interactions réalistes entre les objets. Dans cette section, nous allons voir comment utiliser la physique dans Unity pour créer des mouvements réalistes et des interactions entre les objets.

## Composants de physique

Unity propose plusieurs composants de physique qui permettent de simuler des interactions réalistes entre les objets. Voici quelques-uns des composants de physique les plus couramment utilisés :

-   **Rigidbody** : Le Rigidbody est un composant qui permet de simuler la physique d'un objet. Il permet de définir la masse, la gravité, la vitesse, etc. d'un objet. Le Rigidbody est très utile pour simuler des mouvements réalistes comme la chute d'un objet, la collision entre deux objets, etc. Pour que les objets soient affectés par la physique, il faut que les objets aient un Rigidbody attaché.

-   **Collider** : Le Collider est un composant qui permet de définir la forme d'un objet pour la détection des collisions. Il permet de définir des formes simples comme des boîtes, des sphères, des capsules, etc. Pour que les collisions soient détectées, il faut que les objets aient un Collider attaché. Npus verrons les détection de collisions dans un autre cours.

-   **Joint** : Le Joint est un composant qui permet de relier deux objets entre eux. Il permet de simuler des interactions physiques comme des articulations, des ressorts, des charnières, etc.

-   **Physics Material** : Le Physics Material est un composant qui permet de définir les propriétés physiques d'un objet comme la friction et le rebond. Pour créer un Physics Material, il faut aller dans le menu Assets > Create > Physics Material. On applique ensuite le Physics Material à un Collider pour définir les propriétés physiques de l'objet.

## Mouvements et physique

Il est possible de déplacer un objet en utilisant la physique. Pour cela, il faut ajouter un Rigidbody à l'objet et modifier sa vélocité. La vélocité est un vecteur qui représente la vitesse et la direction de l'objet. Plus la vélocité est élevée, plus l'objet se déplacera rapidement. Plus la vélocité est faible, plus l'objet se déplacera lentement dans la direction du vecteur.

Voici un exemple de script qui permet de déplacer un objet en utilisant la physique :

```csharp
public class DeplacementSimple : MonoBehaviour
{
    public float vitesse = 5f;
    private Rigidbody rb;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        rb.velocity = transform.forward * vitesse;
    }
}
```

## Impulsion de saut

Il est possible de créer une impulsion de saut en ajoutant une force à l'objet. Pour cela, il faut ajouter un Rigidbody à l'objet et utiliser la fonction AddForce pour ajouter une force dans la direction du vecteur. La force est un vecteur qui représente l'intensité et la direction de la force. Plus la force est élevée, plus l'objet sautera haut. Plus la force est faible, plus l'objet sautera bas.

Voici un exemple de script qui permet de créer une impulsion de saut :

```csharp
public class SautSimple : MonoBehaviour
{
    public float hauteur = 5f;
    private Rigidbody rb;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            rb.AddForce(Vector3.up * hauteur, ForceMode.Impulse);
        }
    }
}
```

Il existe plusieurs modes de force qui permettent de modifier le comportement de la force. Le mode Impulse permet de donner une impulsion à l'objet. L'objet est propulsé dans la direction du vecteur avec une intensité donnée. L'objet continuera de se déplacer dans la direction du vecteur jusqu'à ce qu'une autre force soit appliquée, comme par exemple la gravité.

## Rotation et physique

Il est possible de faire tourner un objet en utilisant la physique. Pour cela, il faut ajouter un Rigidbody à l'objet et modifier sa vélocité angulaire. La vélocité angulaire est un vecteur qui représente la vitesse de rotation de l'objet autour de ses axes. Plus la vélocité angulaire est élevée, plus l'objet tournera rapidement. Plus la vélocité angulaire est faible, plus l'objet tournera lentement autour de ses axes.

On peut s'en servir pour faire tourner un objet sur lui-même, comme les pales d'un hélicoptère.

```csharp

public class RotationSimple : MonoBehaviour{

    public float vitesse = 5f;
    private Rigidbody rb;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        rb.angularVelocity = Vector3.up * vitesse;
    }
}
```

Il est aussi possible d'ajouter une force de rotation à l'objet en utilisant la fonction AddTorque. La force de rotation est un vecteur qui représente l'intensité et la direction de la force de rotation. Plus la force de rotation est élevée, plus l'objet tournera rapidement. Plus la force de rotation est faible, plus l'objet tournera lentement autour de ses axes jusqu'à ce qu'une autre force de rotation soit appliquée.

On peut s'en servir pour faire tourner un objet avec une poussée comme au démarrage d'une fusée.

```csharp

public class RotationSimple : MonoBehaviour {

    public float vitesse = 5f;
    private Rigidbody rb;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        rb.AddTorque(Vector3.up * vitesse);
    }
}
```
