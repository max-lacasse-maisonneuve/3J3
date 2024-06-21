# Déplacement de caméra dans Unity

## Caméra en première personne

### Déplacement de la caméra

Pour déplacer la caméra en première personne, il faut utiliser les axes horizontaux et verticaux de la souris pour faire tourner la caméra. Pour cela, on utilise la fonction `Input.GetAxis("Mouse X")` pour récupérer la valeur de l'axe horizontal de la souris et `Input.GetAxis("Mouse Y")` pour récupérer la valeur de l'axe vertical de la souris. On peut ensuite utiliser ces valeurs pour faire tourner la caméra en fonction de la position de la souris.

On positionne la caméra directement sur le joueur et on la fait tourner autour du joueur en fonction de la position de la souris. Pour éviter de voir l'objet du joueur, il est possible de masquer le joueur en désactivant le calque sur lequel il est affiché avec l'options `Culling Mask` de la caméra.

```csharp
void Update()
{
    float mouseX = Input.GetAxis("Mouse X");
    float mouseY = Input.GetAxis("Mouse Y");

    transform.Rotate(Vector3.up, mouseX * sensitivity);
    transform.Rotate(Vector3.right, -mouseY * sensitivity);
}
```

## Caméra en troisième personne

### Déplacement de la caméra

Pour déplacer la caméra en troisième personne, il faut utiliser les axes horizontaux et verticaux de la souris pour faire tourner la caméra autour du joueur. Pour cela, on utilise la fonction `Input.GetAxis("Mouse X")` pour récupérer la valeur de l'axe horizontal de la souris et `Input.GetAxis("Mouse Y")` pour récupérer la valeur de l'axe vertical de la souris. On peut ensuite utiliser ces valeurs pour faire tourner la caméra autour du joueur en fonction de la position de la souris.

On positionne la caméra à une certaine distance du joueur sur l'axe vertical et on la fait tourner autour du joueur en fonction de la position de la souris.

```csharp
void Update()
{
    float mouseX = Input.GetAxis("Mouse X");
    float mouseY = Input.GetAxis("Mouse Y");

    transform.RotateAround(player.position, Vector3.up, mouseX * sensitivity);
    transform.RotateAround(player.position, transform.right, -mouseY * sensitivity);
}
```

### Zoom de la caméra

Pour zoomer la caméra en troisième personne, il faut utiliser la molette de la souris pour faire avancer ou reculer la caméra par rapport au joueur. Pour cela, on utilise la fonction `Input.GetAxis("Mouse ScrollWheel")` pour récupérer la valeur de la molette de la souris. On peut ensuite utiliser cette valeur pour faire avancer ou reculer la caméra par rapport au joueur.

```csharp
void Update()
{
    float scroll = Input.GetAxis("Mouse ScrollWheel");

    transform.position += transform.forward * scroll * zoomSpeed;
}
```

## Caméra de surveillance

### Déplacement de la caméra

Pour déplacer la caméra de surveillance, il faut utiliser les axes horizontaux et verticaux de la souris pour faire tourner la caméra autour d'un point fixe. Pour cela, on utilise la fonction `Input.GetAxis("Mouse X")` pour récupérer la valeur de l'axe horizontal de la souris et `Input.GetAxis("Mouse Y")` pour récupérer la valeur de l'axe vertical de la souris. On peut ensuite utiliser ces valeurs pour faire tourner la caméra autour d'un point fixe en fonction de la position de la souris.

On positionne la caméra à une certaine distance du point fixe sur l'axe vertical et on la fait tourner autour du point fixe en fonction de la position de la souris.

```csharp
void Update()
{
    float mouseX = Input.GetAxis("Mouse X");
    float mouseY = Input.GetAxis("Mouse Y");

    transform.RotateAround(target.position, Vector3.up, mouseX * sensitivity);
    transform.RotateAround(target.position, transform.right, -mouseY * sensitivity);
}
```

## Caméra de suivi

### Déplacement de la caméra

Le plus simple est de parenter la caméra à l'objet que l'on veut suivre. La caméra suivra alors automatiquement l'objet en gardant la même distance et la même orientation par rapport à l'objet. Pour que celle-ci suive l'objet en gardant une certaine distance, il suffit de définir la position de la caméra par rapport à l'objet en utilisant Lerp et lookAt.

```csharp
void Update()
{
    transform.position = Vector3.Lerp(transform.position, target.position - target.forward * distance, Time.deltaTime * followSpeed);
    transform.LookAt(target);
}
```

## Caméra à vol d'oiseau

### Déplacement de la caméra

Pour déplacer la caméra à vol d'oiseau, on place la caméra directement au-dessus de la scène et on la fait tourner autour de la scène en fonction de la position de la souris. Pour cela, on utilise la fonction `Input.GetAxis("Mouse X")` pour récupérer la valeur de l'axe horizontal de la souris et `Input.GetAxis("Mouse Y")` pour récupérer la valeur de l'axe vertical de la souris. On peut ensuite utiliser ces valeurs pour faire tourner la caméra autour de la scène en fonction de la position de la souris. Une caméra orthographique est souvent utilisée pour donner une vue en 2D de la scène.

```csharp
void Update()
{
    float mouseX = Input.GetAxis("Mouse X");
    float mouseY = Input.GetAxis("Mouse Y");

    transform.RotateAround(Vector3.zero, Vector3.up, mouseX * sensitivity);
    transform.RotateAround(Vector3.zero, transform.right, -mouseY * sensitivity);
}
```

## Caméra libre

### Déplacement de la caméra

Pour déplacer la caméra librement, on utilise les touches de déplacement (W, A, S, D) pour déplacer la caméra dans l'espace. Pour cela, on utilise la fonction `Input.GetAxis("Horizontal")` pour récupérer la valeur de l'axe horizontal et `Input.GetAxis("Vertical")` pour récupérer la valeur de l'axe vertical. On peut ensuite utiliser ces valeurs pour déplacer la caméra dans l'espace en fonction des touches de déplacement.

```csharp
void Update()
{
    float horizontal = Input.GetAxis("Horizontal");
    float vertical = Input.GetAxis("Vertical");

    transform.Translate(Vector3.right * horizontal * speed * Time.deltaTime);
    transform.Translate(Vector3.forward * vertical * speed * Time.deltaTime);
}
```
