# Gestion du temps et Coroutines

## Gestion du temps

Unity propose plusieurs fonctions pour gérer le temps. Ces fonctions sont utiles pour créer des effets de ralentissement, de pause, de reprise, etc.

### Time.timeScale

La variable `Time.timeScale` permet de modifier la vitesse du temps. Plus la valeur est élevée, plus le temps s'écoule rapidement. Plus la valeur est faible, plus le temps s'écoule lentement. Si la valeur est égale à zéro, le temps est arrêté. Tout est modifié sauf les fonctions `FixedUpdate()`.

```csharp
public class GestionTemps : MonoBehaviour
{
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            if (Time.timeScale == 0f)
            {
                Time.timeScale = 1f;
            }
            else
            {
                Time.timeScale = 0f;
            }
        }
    }
}
```

### Time.deltaTime

La variable `Time.deltaTime` permet de connaître le temps écoulé entre deux frames. Elle est très utile pour créer des mouvements fluides et indépendants de la vitesse du jeu. Cela permet de s'adapter en fonction de la puissance de l'ordinateur du joueur. Un ordinateur plus faible aura un `Time.deltaTime` plus élevé, un ordinateur plus puissant aura un `Time.deltaTime` plus faible.

Il est donc recommandé d'utiliser `Time.deltaTime` pour les déplacements, les animations, les effets, etc.

```csharp

public class GestionTemps : MonoBehaviour
{
    public float vitesse = 5f;

    void Update()
    {
        transform.Translate(Vector3.forward * vitesse * Time.deltaTime);
    }
}
```

## Coroutines

Les Coroutines sont des fonctions qui permettent de créer des tâches asynchrones. Elles sont très utiles pour créer des effets, des animations, des délais, etc.

### Créer une Coroutine

Pour créer une Coroutine, il suffit de créer une fonction de type `IEnumerator` et d'utiliser le mot-clé `yield return` pour indiquer le délai.

```csharp
public class GestionTemps : MonoBehaviour
{
    public float delai = 2f;

    void Start()
    {
        StartCoroutine(Attendre());
    }

    IEnumerator Attendre()
    {
        yield return new WaitForSeconds(delai);
        Debug.Log("Fin de l'attente");
    }
}
```

### Arrêter une Coroutine

Il est possible d'arrêter une Coroutine en utilisant la fonction `StopCoroutine()`. Il faut cependant enregistrer la Coroutine dans une variable pour pouvoir l'arrêter.

```csharp
public class GestionTemps : MonoBehaviour
{
    public float delai = 2f;
    private Coroutine coroutine;

    void Start()
    {
        coroutine = StartCoroutine(Attendre());
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            StopCoroutine(coroutine);
        }
    }

    IEnumerator Attendre()
    {
        yield return new WaitForSeconds(delai);
        Debug.Log("Fin de l'attente");
    }
}
```

### Exécuter une Coroutine en boucle

Pour répéter une animation en boucle, il est possible de simplement rappeler StartCoroutine() à la fin de la Coroutine. En effet, une Coroutine est une fonction qui peut être appelée à tout moment.

```csharp
public class GestionTemps : MonoBehaviour
{
    public float delai = 2f;
    public GameObject objet;

    void Start()
    {
        StartCoroutine(Animation());
    }

    IEnumerator Animation()
    {
        objet.SetActive(true);
        yield return new WaitForSeconds(delai);
        objet.SetActive(false);
        yield return new WaitForSeconds(delai);

        StartCoroutine(Animation());
    }
}
```
