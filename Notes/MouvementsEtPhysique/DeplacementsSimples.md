# Déplacements simples

Il existe dans Unity plusieurs façons de déplacer un objet. Nous allons voir ici les plus simples.

## Déplacer en avant

La façon la plus simple de déplacer un objet est de le faire avancer en ligne droite. Pour cela, il suffit de modifier sa position en ajoutant une direction multipliée par une vitesse.

Transform.forward est le vecteur de direction de l'objet dans le sens de l'axe Z, donc en avant. C'est l'équivalent d'un new Vector3(0, 0, 1).

Il existe d'autres vecteurs de direction : Transform.up, Transform.down, Transform.right, Transform.left, , Transform.back. L'avantage d'utiliser le vecteur de direction est que si l'objet est tourné, il se déplacera toujours dans la direction de son axe Z local.

```csharp
public class DeplacementSimple : MonoBehaviour
{
public float vitesse = 5f;

    void Update()
    {
        transform.position += transform.forward * vitesse * Time.deltaTime;
    }

}

```

### Avec la fonction Translate

La fonction Translate permet de déplacer un objet en ajoutant un vecteur de déplacement à sa position. Elle est plus simple à utiliser que de modifier directement la position. Elle effectue la même opération que l'exemple précédent mais le code est plus lisible.

```csharp
public class DeplacementSimple : MonoBehaviour
{
    public float vitesse = 5f;

    void Update()
    {
        transform.Translate(Vector3.forward * vitesse * Time.deltaTime);
    }
}
```

## Déplacer vers une position fixe

Pour déplacer un objet vers une position fixe, il suffit de calculer la direction entre l'objet et la position cible, puis de normaliser cette direction pour obtenir un vecteur de direction. Ensuite, on ajoute ce vecteur à la position de l'objet multiplié par une vitesse comme dans l'exemple précédent.

### Trouver la direction entre deux points

En mathématiques, la direction entre deux points est un vecteur qui va du premier point au second. Pour trouver ce vecteur, on soustrait le premier point au second.

```csharp
    Vector3 depart = new Vector3(2, 0, 0);
    Vector3 cible = new Vector3(5, 0, 0);
    Vector3 direction = cible - depart;//(5, 0, 0) - (2, 0, 0) = (3, 0, 0)
```

### Normaliser un vecteur

Normaliser un vecteur signifie le rendre de longueur 1. Cela trouver la direction sans se soucier de la distance entre l'objet et la cible.

```csharp
    Vector3 depart = new Vector3(2, 0, 0);
    Vector3 cible = new Vector3(5, 0, 0);
    Vector3 direction = cible - depart;//(5, 0, 0) - (2, 0, 0) = (3, 0, 0)
    Vector3 directionNormalisee = direction.normalized;//(1, 0, 0)
```

### Pour se déplacer vers une position fixe

Ici la cible pourrait être un autre objet, un point d'apparition(spawn), un point de destination, etc. Le mouvement sera toujours en ligne droite et la vitesse sera constante.

```csharp
public class DeplacementSimple : MonoBehaviour
{
    public Transform cible;
    public float vitesse = 5f;

    void Update()
    {
        Vector3 direction = (cible.position - transform.position).normalized;
        transform.position += direction * vitesse * Time.deltaTime;
    }
}
```

### Fonction MoveTowards

La fonction MoveTowards permet de déplacer un objet vers une position cible en ligne droite. Elle prend en paramètre la position de départ, la position cible et la distance à parcourir. La fonction renvoie la nouvelle position de l'objet. Elle est plus simple à utiliser que de calculer la direction et de normaliser le vecteur.

```csharp
public class DeplacementSimple : MonoBehaviour
{
    public Transform cible;
    public float vitesse = 5f;

    void Update()
    {
        transform.position = Vector3.MoveTowards(transform.position, cible.position, vitesse * Time.deltaTime);
    }
}
```

## Utiliser la force et la masse

Pour déplacer un objet en utilisant la physique, il faut ajouter une force à l'objet. Pour cela, il faut ajouter un composant Rigidbody à l'objet. La force est appliquée à l'objet en utilisant la fonction AddForce. La masse de l'objet est importante car elle détermine la résistance de l'objet au mouvement. Plus la masse est élevée, plus l'objet sera difficile à déplacer.

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
        rb.AddForce(transform.forward * vitesse);
    }
}
```

### Force sous forme d'impulsion

L'impulsion permet de donner l'effet d'une fusée qui s'active une seule fois. L'objet est propulsé dans une direction donnée. L'impulsion est utile pour les sauts, les explosions, les coups, etc.

-   Impulsion : La force est appliquée une seule fois. Pour cela, il faut ajouter un paramètre supplémentaire à la fonction AddForce. Il s'agit du mode de la force.

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
        if (Input.GetKeyDown(KeyCode.Space))
        {
            rb.AddForce(transform.forward * vitesse, ForceMode.Impulse);
        }
    }
}
```

## Utiliser la vélocité

La vélocité est la vitesse d'un objet dans une direction donnée. En changeant la vélocité, l'objet sera en déplacement constant. Au contraire, en mettant la vélocité à zéro, l'objet s'arrêtera. On doit indiquer la direction en multipliant par la vitesse.

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

## Avec le composant CharacterController

Le CharacterController est un composant qui a été conçu pour gérer les déplacements des personnages. Il est très utile pour les jeux de plateforme, les jeux de tir, les jeux de combat, etc.

Nous verrons dans un prochain chapitre comment utiliser le composant CharacterController pour déplacer un objet.

## Avec le composant NavMeshAgent

Il est possible de déplacer un objet automatiquement en utilisant le composant NavMeshAgent. Ce composant permet de déplacer un objet sur un terrain en utilisant la navigation de l'IA. Il est très utile pour les jeux d'aventure, les jeux de rôle, les jeux de stratégie, etc.

Nous verrons dans un prochain chapitre comment utiliser le composant NavMeshAgent pour déplacer un objet automatiquement.

## Lerp

La fonction Lerp permet de modifier l'interpolation entre deux valeurs. Elle prend en paramètre la valeur de départ, la valeur d'arrivée et le pourcentage d'interpolation. Plus le pourcentage est élevé, plus la valeur sera proche de la valeur d'arrivée. Plus le pourcentage est faible, plus la valeur sera proche de la valeur de départ.

Lerp est très utile pour créer des transitions fluides entre deux valeurs comme un fondu enchaîné, un changement de couleur, un changement de taille, etc.

Il est possible de créer une décélération en utilisant la fonction Lerp. Pour cela, il faut diminuer le pourcentage d'interpolation à chaque frame.

```csharp
public class DeplacementSimple : MonoBehaviour
{
    public Transform cible;
    public float vitesse = 5f;
    private float pourcentage = 0f;

    void Update()
    {
        pourcentage += Time.deltaTime * vitesse;
        transform.position = Vector3.Lerp(transform.position, cible.position, pourcentage);
    }
}
```

## SmoothDamp

La fonction SmoothDamp permet de créer un mouvement fluide entre deux valeurs. Elle prend en paramètre la valeur de départ, la valeur d'arrivée, une référence à la vélocité et le temps de mouvement. La vélocité est une référence à la vitesse de l'objet. Plus la vélocité est élevée, plus l'objet se déplacera rapidement. Plus la vélocité est faible, plus l'objet se déplacera lentement.

SmoothDamp est très utile pour créer des mouvements fluides comme une caméra qui suit un personnage, un personnage qui suit un point, un objet qui suit un autre objet, etc.

```csharp
public class DeplacementSimple : MonoBehaviour
{
    public Transform cible;
    public float vitesse = 5f;
    private Vector3 velocity = Vector3.zero;

    void Update()
    {
        transform.position = Vector3.SmoothDamp(transform.position, cible.position, ref velocity, vitesse);
    }
}

```
