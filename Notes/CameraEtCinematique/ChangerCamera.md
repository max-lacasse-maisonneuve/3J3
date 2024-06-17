# Changer de camera par programmation

Dans Unity, il est possible de changer de camera par programmation. Pour cela, il suffit de désactiver la caméra courante et d'activer la caméra souhaitée.

```csharp
using UnityEngine;

public class CameraSwitcher : MonoBehaviour
{
    public Camera camera1;
    public Camera camera2;

    void Start()
    {
        camera1.enabled = true;
        camera2.enabled = false;
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.C))
        {
            camera1.enabled = !camera1.enabled;
            camera2.enabled = !camera2.enabled;
        }
        else if (Input.GetKeyUp(KeyCode.C))
        {
             camera1.enabled = !camera1.enabled;
            camera2.enabled = !camera2.enabled;
        }
    }
}
```

Dans cet exemple, nous avons deux caméras `camera1` et `camera2`. Au démarrage, la caméra 1 est activée et la caméra 2 est désactivée. Lorsque l'utilisateur appuie sur la touche `C`, les caméras sont alternativement activées et désactivées. Au relâchement de la touche `C`, les caméras reviennent à leur état initial.

On pourrait utiliser cette technique pour passer d'une vue à la première personne à une vue à la troisième personne, ou pour basculer entre différentes caméras dans une scène.