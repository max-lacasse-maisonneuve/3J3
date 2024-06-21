# Rotation

Il existe dans Unity plusieurs façons de tourner un objet.

## Angle en degrés

Les angles Euler sont des angles qui décrivent une rotation en trois dimensions. Ces angles sont souvent exprimés en degré en géométrie 3D. Ils sont utilisés pour décrire la rotation d'un objet autour de ses axes X, Y et Z.

-   Axe X : C'est l'axe qui traverse le côté de l'objet. L'objet roule sur lui-même, de l'avant vers l'arrière, comme quelqu'un qui tombe en avant ou en arrière.
-   Axe Y : C'est l'axe qui traverse l'objet de haut en bas. L'objet tourne de gauche à droite comme la tête d'une personne.
-   Axe Z : C'est l'axe qui traverse l'objet de l'avant vers l'arrière. L'objet tangue de gauche à droite comme un bateau qui roule sur les vagues.

Par défaut, pour modifier l'angle Euler d'un objet, il est possible de modifier la composant transform.eulerAngles.

```csharp
public class RotationSimple : MonoBehaviour
{
    public float vitesseRotation = 5f;

    void Update()
    {
        Vector3 angles = transform.eulerAngles;
        angles.y += vitesseRotation * Time.deltaTime;
        transform.eulerAngles = angles;
    }
}
```

## Tourner sur soi-même avec un angle en degrés

La façon la plus simple de tourner un objet est d'utiliser la méthode Rotate. Pour cela, il suffit de modifier sa rotation en ajoutant un angle en degrés à son axe de rotation. On passe l'angle à modifier pour chaque axe.

Dans l'exemple suivant nous faisons tourner l'objet sur son axe Y à une vitesse de 5 degrés par seconde.

```csharp
public class RotationSimple : MonoBehaviour
{
    public float vitesseRotation = 5f;

    void Update()
    {
        transform.Rotate(0, vitesseRotation * Time.deltaTime, 0);
    }
}
```

### Gimbal lock

Même si les angles Euler sont plus simples à manipuler, ils ont un problème appelé Gimbal lock.

Le Gimbal lock est un problème qui survient lorsque deux axes de rotation sont alignés. Par exemple, si l'objet est tourné à 90° sur l'axe X, l'axe Y et l'axe Z sont alignés. Si on essaie de tourner l'objet sur l'axe Y, il tournera en réalité sur l'axe Z. Les axes sont bloqués et l'objet ne peut plus tourner correctement.

Pour éviter ce problème, on peut utiliser les quaternions pour décrire une rotation. Les quaternions sont plus complexes à manipuler mais ils permettent de décrire une rotation sans problème de Gimbal lock car ils utilisent quatre composantes pour décrire une rotation.

La propriété transform.rotation permet de modifier la rotation de l'objet en utilisant des quaternions.

### Tourner sur soi-même avec un angle en degrés avec des Quaternions

Il est préférable d'utiliser les quaternions pour tourner un objet. Les quaternions permettent de décrire une rotation sans problème de Gimbal lock. Ils sont plus complexes à manipuler que les angles d'Euler mais ils sont plus précis et plus rapides.

Il est possible d'utiliser la fonction Quaternion.Euler qui permet de créer un quaternion à partir d'un angle en degrés pour réaliser le même effet l'exemple précédent.

```csharp
public class RotationSimple : MonoBehaviour
{
    public float vitesseRotation = 5f;

    void Update()
    {
        Vector3 direction = Quaternion.Euler(0, vitesseRotation * Time.deltaTime, 0)
        transform.Rotate(direction);
    }
}
```

## Tourner dans une direction précise

Pour tourner un objet dans une direction précise, il suffit de calculer la direction entre l'objet et la position cible, puis de calculer l'angle entre la direction et l'axe de rotation de l'objet.

### Fonction LookAt

La fonction LookAt permet de tourner un objet vers une position cible. Elle prend en paramètre la position cible et la fonction s'occupe de calculer l'angle entre l'objet et la cible. Elle effectue la même opération que l'exemple précédent mais le code est plus lisible. L'objet tournera vers la cible en ligne droite sans interpolation.

Elle est utilisée souvent pour faire tourner un objet vers un point précis. Elle est plus simple à utiliser que de calculer l'angle entre deux vecteurs. Par exemple, on peut s'en servir pour qu'une camera regarde un objet ou pour que le joueur regarde un point précis.

```csharp

public class RotationSimple : MonoBehaviour
{
    public Transform cible;

    void Update()
    {
        transform.LookAt(cible);
    }
}
```

### Fonction RotateTowards

La fonction RotateTowards permet de tourner un objet vers une position cible en ligne droite. Elle prend en paramètre la position de départ, la position cible et l'angle à parcourir. La fonction renvoie la nouvelle rotation de l'objet. Elle est plus simple à utiliser que de calculer l'angle entre deux vecteurs.

Elle permet de tourner l'objet vers la cible en ligne droite avec une vitesse constante et donne comme effet un mouvement de rotation fluide mais linéaire.

La fonction LookRotation permet de calculer la rotation à partir d'un vecteur direction. Elle prend en paramètre le vecteur direction et renvoie la rotation correspondante.

Elle permet de tourner l'objet vers la cible en ligne droite avec une vitesse constante et donne comme effet un mouvement de rotation fluide mais linéaire.

```csharp

public class RotationSimple : MonoBehaviour
{
    public Transform cible;
    public float vitesseRotation = 90f;

    void Update()
    {
        Vector3 direction = cible.position - transform.position;
        Quaternion rotation = Quaternion.RotateTowards(transform.rotation, Quaternion.LookRotation(direction), vitesseRotation * Time.deltaTime);
        transform.rotation = rotation;
    }
}
```

## Tourner en orbite autour d'un point

Pour tourner un objet en orbite autour d'un point, il suffit de calculer la direction entre l'objet et le point d'orbite, puis de calculer l'angle entre la direction et l'axe de rotation de l'objet.

La fonction RotateAround permet de tourner un objet autour d'un point donné. Elle prend en paramètre le point d'orbite, l'axe de rotation et l'angle de rotation.

```csharp
public class RotationSimple : MonoBehaviour
{
    public Transform pointOrbite;
    public float vitesseRotation = 5f;

    void Update()
    {
        transform.RotateAround(pointOrbite.position, transform.up, vitesseRotation * Time.deltaTime);
    }
}
```

Exemple d'une camera orbitant autour d'un point.

```csharp

public class RotationSimple : MonoBehaviour
{
    public Transform pointOrbite;
    public float rayon;
    public float sensibilite = 5f;

    void Update()
    {
        rayon += Input.mouseScrollDelta.y;
        transform.position = pointOrbite.position - (transform.forward * rayon);
        transform.RotateAround(pointOrbite.position, Vector3.up, Input.GetAxis("Mouse X") * sensibilite);
        transform.RotateAround(pointOrbite.position, transform.right, Input.GetAxis("Mouse Y") * sensibilite);
    }
}
```

## Slerp

La fonction Slerp permet de tourner un objet de manière fluide entre deux rotations. Elle prend en paramètre la rotation de départ, la rotation cible et le pourcentage de rotation à effectuer. La fonction renvoie la nouvelle rotation de l'objet. Elle est plus simple à utiliser que de calculer l'angle entre deux vecteurs.

```csharp

public class RotationSimple : MonoBehaviour
{
    public Transform cible;
    public float vitesseRotation = 90f;

    void Update()
    {
        Vector3 direction = cible.position - transform.position;
        Quaternion rotation = Quaternion.Slerp(transform.rotation, Quaternion.LookRotation(direction), vitesseRotation * Time.deltaTime);
        transform.rotation = rotation;
    }
}
```

### Fonction SmoothDampAngle

La fonction SmoothDampAngle permet de tourner un objet de manière fluide entre deux angles. Elle prend en paramètre l'angle de départ, l'angle cible et la vitesse de rotation. La fonction renvoie le nouvel angle de l'objet. Elle est plus simple à utiliser que de calculer l'angle entre deux vecteurs.

La fonction est plus complexe à utiliser mais elle permet de contrôler la vitesse de rotation de manière plus précise et plus fluide.

Permet de tourner en cherchant la rotation la plus courte entre deux angles.

```csharp

public class RotationSimple : MonoBehaviour
{
    public Transform cible;
    public float sensibilite = 1f;
    public Vector3 nouvelleRotation;

    float xVelocity;
    float yVelocity;
    float zVelocity;

    void Update()
    {
        Vector3 direction = cible.position - transform.position;
        Vector cibleRotation = Quaternion.LookRotation(direction).eulerAngles;

        float x = Mathf.SmoothDampAngle(nouvelleRotation.x, cibleRotation.x, ref xVelocity, sensibilite);
        float y = Mathf.SmoothDampAngle(nouvelleRotation.y, cibleRotation.y, ref xVelocity, sensibilite);
        float z = Mathf.SmoothDampAngle(nouvelleRotation.z, cibleRotation.z, ref xVelocity, sensibilite);

        nouvelleRotation = new Vector3(x, y, z);
        transform.eulerAngles = nouvelleRotation;
    }
}
```

## Tourner en utilisant la physique

### AddTorque

La fonction AddTorque permet de tourner un objet en utilisant la physique. Elle prend en paramètre la force de rotation à appliquer sur l'objet. La fonction renvoie la nouvelle rotation de l'objet. La physique est plus réaliste et l'objet finira par ralentir avec la friction.

```csharp

public class RotationSimple : MonoBehaviour
{
    public float vitesseRotation = 5f;

    void Update()
    {
        GetComponent<Rigidbody>().AddTorque(0, vitesseRotation, 0);
    }
}
```
