# Déclencher une cinématique dans Unity

Dans Unity, il est possible de déclencher une cinématique à l'aide de scripts. Une cinématique est une séquence d'animations et de mouvements de caméra qui permet de raconter une histoire ou de mettre en scène une action. Voici comment déclencher une cinématique dans Unity :

## Créer une cinématique

Avant de pouvoir déclencher une cinématique, il faut d'abord la créer. Pour cela, il est possible d'utiliser l'outil **Timeline** de Unity. Cet outil permet de créer des séquences d'animations et de mouvements de caméra de manière visuelle. Il est possible d'ajouter des pistes d'animation, de mouvement de caméra, de son, etc. pour créer une cinématique complète.

## Déclencher la cinématique par script

Une fois la cinématique créée, il est possible de la déclencher par script. Pour cela, il faut ajouter un composant **Playable Director** à un objet de la scène. Ce composant permet de contrôler la lecture de la cinématique. Ensuite, il suffit d'ajouter un script à un autre objet de la scène pour déclencher la cinématique.

Il est possible de déclencher une cinématique de différentes manières en fonction des besoins du jeu. Par exemple, on pourrait déclencher une cinématique lorsqu'un ennemi est vaincu, lorsqu'un objectif est atteint, ou lorsqu'un événement particulier se produit dans le jeu.

### Bloquer les mouvements du joueur pendant la cinématique

Il est parfois nécessaire de bloquer les mouvements du joueur pendant une cinématique pour éviter qu'il ne puisse interagir avec le jeu pendant la séquence. Pour cela, il est possible de désactiver les scripts de mouvement du joueur pendant la cinématique et de les réactiver une fois la cinématique terminée.

Il est également possible de désactiver les contrôles du joueur, de verrouiller la caméra ou de masquer l'interface pendant la cinématique pour une meilleure immersion du joueur.

Dans cet exemple, le script `CinematiqueTrigger` est attaché à un objet de la scène qui déclenche la cinématique. Lorsque le joueur entre en collision avec cet objet, la cinématique est déclenchée en appelant la méthode `Play()` du composant `PlayableDirector`.

```csharp
using UnityEngine;

public class CinematiqueTrigger : MonoBehaviour
{
    public PlayableDirector director;
    public PlayerController playerController;

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            playerController.enabled = false;
            director.Play();
        }
    }
}
```
