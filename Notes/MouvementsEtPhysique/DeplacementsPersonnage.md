# Deplacement d'un personnage

Il existe plusieurs stratégies pour déplacer un personnage dans un jeu vidéo. Nous allons voir les différentes méthodes pour déplacer un personnage dans un jeu vidéo dans Unity.

## Avec les touches du clavier uniquement

Avec l'ancien système d'input, il était possible de déplacer un personnage en utilisant les touches du clavier. Pour cela, il suffisait de récupérer les valeurs des touches du clavier et de les utiliser pour déplacer le personnage. On peut récupérer les valeurs des touches du clavier avec la fonction `Input.GetKey(KeyCode key)`.

À noter que la détection des touches du clavier se fait dans la fonction `Update()`. Si vous utilisez la physique, il est recommandé d'utiliser la fonction `FixedUpdate()` pour appliquer les forces sur le personnage.

```csharp
void Update()
{
    if (Input.GetKey(KeyCode.LeftArrow))
    {
        transform.Translate(Vector3.left * speed * Time.deltaTime);
    }
    if (Input.GetKey(KeyCode.RightArrow))
    {
        transform.Translate(Vector3.right * speed * Time.deltaTime);
    }
    if (Input.GetKey(KeyCode.UpArrow))
    {
        transform.Translate(Vector3.forward * speed * Time.deltaTime);
    }
    if (Input.GetKey(KeyCode.DownArrow))
    {
        transform.Translate(Vector3.back * speed * Time.deltaTime);
    }
}
```

Cependant, pour faciliter la lecture, certaines touches sont déjà configurées par défaut dans Unity. Par exemple, les touches fléchées pour se déplacer en haut, en bas, à gauche et à droite et la touche espace pour sauter. Il est possible de récupérer les valeurs des touches du clavier avec la fonction `Input.GetAxis(string axisName)`. Les valeurs des touches du clavier sont configurées dans le menu Edit -> Project Settings -> Input Manager.

À noter que le nom est sensible à la casse, il faut donc bien respecter la casse des noms des touches.

-   Horizontal : Les touches A et D ou les touches fléchées de gauche et de droite
-   Vertical : Les touches W et S ou les touches fléchées du haut et du bas
-   Jump : La touche espace
-   Fire1 : La touche gauche de la souris
-   Fire2 : La touche droite de la souris
-   Fire3 : La touche du milieu de la souris

```csharp
void Update()
{
    float horizontal = Input.GetAxis("Horizontal");
    float vertical = Input.GetAxis("Vertical");

    Vector3 direction = new Vector3(horizontal, 0, vertical);
    transform.Translate(direction * speed * Time.deltaTime);
}
```

## Avec un clavier et une souris

## Avec un controleur

## Avec la physique

Pour déplacer un personnage avec la physique, il est recommandé d'ajouter le composant `CharacterController` au personnage. Le `CharacterController` est un composant qui permet de gérer les collisions et les déplacements d'un personnage. Il est possible de déplacer un personnage avec la fonction `Move(Vector3 motion)`.

Le composant contient un collider qui permet de gérer les collisions avec les autres objets. Il est possible de récupérer les collisions avec la fonction `OnControllerColliderHit(ControllerColliderHit hit)`.Il réagit également aux forces extérieures comme la gravité, donc pas besoin d'ajouter les composants `Rigidbody` et `Collider`.

```csharp
void Update()
{
    float horizontal = Input.GetAxis("Horizontal");
    float vertical = Input.GetAxis("Vertical");

    Vector3 direction = new Vector3(horizontal, 0, vertical);
    controller.Move(direction * speed * Time.deltaTime);
}
```

## Avec un pathfinding

## Stratégie - Déplacement en ligne vertical et rotation horizontale

Pour déplacer un personnage en ligne vertical et en rotation horizontale, il suffit de récupérer les valeurs des touches du clavier pour déplacer le personnage en ligne vertical et de récupérer la position de la souris pour faire tourner le personnage en rotation horizontale.

```csharp
void Update()
{
    float vertical = Input.GetAxis("Vertical");
    float horizontal = Input.GetAxis("Horizontal");

    Vector3 direction = new Vector3(0, 0, vertical);
    transform.Translate(direction * speed * Time.deltaTime);

    float mouseX = Input.GetAxis("Mouse X");
    transform.Rotate(Vector3.up * mouseX * rotationSpeed * Time.deltaTime);
}
```

## Stratégie - Déplacement horizontal et vertical avec rotation avec la souris

## Stratégie - Déplacement en 8 directions

Pour déplacer un personnage en 8 directions, il suffit de récupérer les valeurs des touches du clavier pour déplacer le personnage en 8 directions. Pour s'assurer que le personnage se déplace en 8 directions, il faut s'assurer que la somme des valeurs des touches du clavier soit égale à 1.

Il faut donc normaliser le vecteur de direction pour s'assurer que la somme des valeurs des touches du clavier soit égale à 1.

```csharp
void Update()
{
    float horizontal = Input.GetAxis("Horizontal");
    float vertical = Input.GetAxis("Vertical");

    Vector3 direction = new Vector3(horizontal, 0, vertical).normalized;
    transform.Translate(direction * speed * Time.deltaTime);
}
```

## Stratégie - Déplacement en diagonale
