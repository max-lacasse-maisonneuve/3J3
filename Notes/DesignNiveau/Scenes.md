# Gestion des scènes

## Scènes

Les scènes sont des éléments de jeu qui permettent de découper le jeu en différentes parties. Elles permettent de gérer les transitions entre les différentes parties du jeu, de gérer les éléments de jeu qui sont actifs ou non, de gérer les éléments de jeu qui sont visibles ou non, etc.

## Création d'une scène

Pour créer une scène, il suffit de créer un fichier `.unity` dans le dossier `Assets/Scenes`. Il est possible de créer des sous-dossiers pour organiser les scènes.

## Chargement d'une scène

Pour charger une scène, il suffit d'utiliser la méthode `SceneManager.LoadScene` en lui passant le nom de la scène à charger en paramètre. Il est important d'ajouter le namespace `UnityEngine.SceneManagement` pour pouvoir utiliser cette méthode.

Aussi, il est important de noter que la scène doit être ajoutée dans la liste des scènes à build dans les `Build Settings` du menu `File`. De plus, le nom de la scène doit être exactement le même que celui utilisé pour charger la scène.

```csharp

using UnityEngine.SceneManagement;

public class SceneLoader : MonoBehaviour
{
   public void Update()
   {
      if(Input.GetKeyDown(KeyCode.Space))
      {
         SceneManager.LoadScene("SceneName");
      }
   }
}

```
