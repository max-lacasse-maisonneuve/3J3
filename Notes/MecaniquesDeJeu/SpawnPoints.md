# Points d'apparition (Spawn Points)

Les points d'apparition sont des objets qui permettent de définir les positions où les joueurs apparaissent dans le jeu. Ils sont généralement placés à des endroits stratégiques pour permettre aux joueurs de réapparaître rapidement après avoir été éliminés. Il est possible de définir plusieurs points d'apparition dans une même scène pour offrir plus de variété aux joueurs.

Généralement, on place des empty GameObjects dans la scène pour définir les points d'apparition. Ces GameObjects sont ensuite référencés dans un script qui gère le système de spawn des joueurs sous forme d'une liste de Transform.

On peut alors choisir un point aléatoirement dans la liste pour faire apparaître un joueur à cet endroit. On peut aussi choisir un point en fonction de critères spécifiques, comme la distance par rapport à un autre joueur ou la proximité d'un objectif.

```csharp
public class SpawnManager : MonoBehaviour
{
    public List<Transform> spawnPoints;

    public Transform GetRandomSpawnPoint()
    {
        return spawnPoints[Random.Range(0, spawnPoints.Count)];
    }
}
```