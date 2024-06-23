# Créer un gestionnaire de jeu

Un gestionnaire de jeu est un script qui permet de contrôler le déroulement d'une partie. Il peut gérer les points de vie des joueurs, les points de score, les objectifs à atteindre, les conditions de victoire ou de défaite, etc. C'est le chef d'orchestre du jeu, qui coordonne les différents éléments pour offrir une expérience de jeu cohérente et intéressante et qui appellera les fonctions nécessaires pour gérer les événements du jeu.

## Créer un script de gestionnaire de jeu

Pour créer un gestionnaire de jeu, il suffit de créer un nouveau script dans votre projet Unity et de l'attacher à un GameObject vide dans votre scène.

### Patron de conception Singleton

Il est souvent recommandé de créer un gestionnaire de jeu en utilisant le patron de conception Singleton. Ce patron de conception permet de s'assurer qu'il n'y a qu'une seule instance du gestionnaire de jeu dans la scène. Cela permet d'éviter les problèmes de synchronisation et de garantir que le gestionnaire de jeu est accessible de n'importe où dans le jeu.

```csharp
public class GameManager : MonoBehaviour
{
    public static GameManager instance;

    void Awake()
    {
        if (instance == null)
        {
            instance = this;
        }
        else
        {
            Destroy(gameObject);
        }
    }

    // Ajoutez ici les fonctions de gestion du jeu

    public void StartGame()
    {
        // Code pour démarrer le jeu
    }

    public void EndGame()
    {
        // Code pour terminer le jeu
    }

    public void RestartGame()
    {
        // Code pour redémarrer le jeu
    }
}
```

Dans cet exemple, le gestionnaire de jeu est un Singleton qui permet d'accéder à l'instance du gestionnaire de jeu à partir de n'importe où dans le code en utilisant `GameManager.Instance`. Le gestionnaire de jeu contient des fonctions pour démarrer, terminer et redémarrer le jeu, ainsi que d'autres fonctions pour gérer les événements du jeu.

Le Singleton assigne une instance de lui-même à la variable `instance` lors de son initialisation. Si une autre instance du Singleton est créée, elle est détruite pour garantir qu'il n'y ait qu'une seule instance du Singleton dans la scène.

### Utilisation du gestionnaire de jeu

Une fois que vous avez créé votre gestionnaire de jeu, vous pouvez l'utiliser pour contrôler le déroulement de votre partie. Vous pouvez appeler les fonctions du gestionnaire de jeu à partir d'autres scripts pour démarrer, terminer ou redémarrer le jeu, ou pour gérer d'autres événements du jeu.

```csharp

public class Player : MonoBehaviour
{
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            GameManager.instance.StartGame();
        }

        if (Input.GetKeyDown(KeyCode.Escape))
        {
            GameManager.instance.EndGame();
        }

        if (Input.GetKeyDown(KeyCode.R))
        {
            GameManager.instance.RestartGame();
        }
    }
}
```
