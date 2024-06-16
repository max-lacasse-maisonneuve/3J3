# Rotation

Il existe dans Unity plusieurs façons de tourner un objet.

## Tourner sur soi-même avec un angle en degrés

La façon la plus simple de tourner un objet est de le faire tourner sur lui-même. Pour cela, il suffit de modifier sa rotation en ajoutant un angle en degrés à son axe de rotation.

```csharp
public class RotationSimple : MonoBehaviour
{
    public float vitesseRotation = 90f;

    void Update()
    {
        transform.Rotate(0, vitesseRotation * Time.deltaTime, 0);
    }
}
```

### Gimbal lock

Le Gimbal lock est un problème qui survient lorsqu'on utilise les angles d'Euler pour décrire une rotation. Cela arrive lorsque deux axes de rotation sont alignés. Par exemple, si l'objet est tourné à 90° sur l'axe X, l'axe Y et l'axe Z sont alignés. Si on essaie de tourner l'objet sur l'axe Y, il tournera en réalité sur l'axe Z.

Pour éviter ce problème, on peut utiliser les quaternions pour décrire une rotation. Les quaternions sont plus complexes à manipuler mais ils permettent de décrire une rotation sans problème de Gimbal lock.

## Tourner sur soi-même avec un angle en degrés avec des Quaternions

Pour tourner un objet avec des quaternions, on utilise la fonction Quaternion.Euler qui permet de créer un quaternion à partir d'un angle en degrés.

```csharp
public class RotationSimple : MonoBehaviour
{
    public float vitesseRotation = 90f;

    void Update()
    {
        Vector3 direction = Quaternion.Euler(0, vitesseRotation * Time.deltaTime, 0)
        transform.Rotate(direction);
    }
}
```

## Tourner vers un angle fixe

Pour tourner un objet vers un angle fixe, il suffit de modifier sa rotation en lui donnant un angle en degrés.
Cela permet de tourner l'objet vers un angle fixe. L'objet tournera sur lui-même.

```csharp
public class RotationSimple : MonoBehaviour
{
    public float angle = 90f;

    void Update()
    {
        transform.rotation = Quaternion.Euler(0, angle, 0);
    }
}
```

### LookRotation

La fonction LookRotation permet de tourner un objet vers une direction donnée. Elle prend en paramètre la direction à regarder et renvoie la rotation correspondante. Elle est plus simple à utiliser que de calculer l'angle entre deux vecteurs.

```csharp
public class RotationSimple : MonoBehaviour
{
    public Vector3 direction = new Vector3(1, 0, 0);

    void Update()
    {
        transform.rotation = Quaternion.LookRotation(direction);
    }
}
```

## Tourner vers une position fixe

Pour tourner un objet vers une position fixe, il suffit de calculer la direction entre l'objet et la position cible, puis de calculer l'angle entre la direction et l'axe de rotation de l'objet.

### Trouver l'angle entre deux vecteurs

En mathématiques, l'angle entre deux vecteurs est l'angle formé par ces deux vecteurs. Pour trouver cet angle, on utilise la fonction Vector3.Angle qui prend deux vecteurs en paramètres et renvoie l'angle entre ces deux vecteurs.

```csharp
Vector3 depart = new Vector3(2, 0, 0);
Vector3 cible = new Vector3(5, 0, 0);
float angle = Vector3.Angle(depart, cible);//0
```

### Pour tourner vers une position fixe

```csharp
public class RotationSimple : MonoBehaviour
{
    public Transform cible;

    void Update()
    {
        Vector3 direction = cible.position - transform.position;
        float angle = Vector3.Angle(transform.forward, direction);
        transform.rotation = Quaternion.Euler(0, angle, 0);
    }
}
```

### Fonction LookAt

La fonction LookAt permet de tourner un objet vers une position cible. Elle prend en paramètre la position cible et la fonction s'occupe de calculer l'angle entre l'objet et la cible. Elle effectue la même opération que l'exemple précédent mais le code est plus lisible. L'objet tournera vers la cible en ligne droite sans interpolation.

Elle donne comme effet un mouvement de rotation instantané et brusque. Elle est souvent utilisée en combinaison avec SmoothDamp pour obtenir un mouvement de rotation fluide tout en regardant la cible.

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

### Tourner en orbite autour d'un point

Pour tourner un objet en orbite autour d'un point, il suffit de calculer la direction entre l'objet et le point d'orbite, puis de calculer l'angle entre la direction et l'axe de rotation de l'objet.

La fonction RotateAround permet de tourner un objet autour d'un point donné. Elle prend en paramètre le point d'orbite, l'axe de rotation et l'angle de rotation.

```csharp
public class RotationSimple : MonoBehaviour
{
    public Transform pointOrbite;
    public float vitesseRotation = 90f;

    void Update()
    {
        Vector3 direction = pointOrbite.position - transform.position;
        float angle = Quaternion.Angle(transform.rotation, Quaternion.LookRotation(direction));
        transform.RotateAround(pointOrbite.position, Vector3.up, vitesseRotation * Time.deltaTime);
    }
}
```

## Point de pivot par rapport au parent

Pour changer le point de pivot d'un objet par rapport à son parent, il suffit de modifier sa position locale. Cela permet de déplacer le point de pivot sans déplacer l'objet lui-même. On déplace l'objet par rapport à son parent et celui peut tourner par rapport à son axe local et non plus par rapport à l'axe global.

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

```csharp

public class RotationSimple : MonoBehaviour
{
    public Transform cible;
    public float vitesseRotation = 90f;

    void Update()
    {
        Vector3 direction = cible.position - transform.position;
        float angle = Vector3.Angle(transform.forward, direction);
        float rotation = Mathf.SmoothDampAngle(transform.rotation.eulerAngles.y, angle, ref vitesseRotation, 0.1f);
        transform.rotation = Quaternion.Euler(0, rotation, 0);
    }
}
```