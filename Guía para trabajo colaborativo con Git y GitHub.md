### Guía para trabajo colaborativo con Git/GitHub

Esta guía detalla los pasos necesarios para llevar a cabo un proyecto colaborativo utilizando Git y GitHub. El proyecto implica la creación de un repositorio llamado ShapesRepo, donde se desarrollarán diferentes clases para representar formas geométricas. El líder del equipo, Desarrollador 1, será responsable de coordinar el flujo de trabajo y gestionar el repositorio, mientras que los Desarrolladores 2 y 3 contribuirán con la implementación de clases específicas.

1. **Desarrollador 1**: Crear el repositorio en GitHub y agregar colaboradores.
   - Inicia sesión en GitHub y crea un nuevo repositorio llamado ShapesRepo.
   - Invita a los otros dos desarrolladores agregando sus nombres de usuario de GitHub.

2. **Desarrollador 1**: Clonar el repositorio.
   - Clona el repositorio en tu repositorio local utilizando el comando `git clone <URL_del_ShapesRepo>`.

3. **Desarrollador 2**: Clonar el repositorio.
   - Clona el repositorio en tu repositorio local usando `git clone <URL_del_ShapesRepo>`.

4. **Desarrollador 3**: Clonar el repositorio.
   - Clona el repositorio en tu repositorio local usando `git clone <URL_del_ShapesRepo>`.

5. **Desarrollador 1**: Crear la clase Shape.java en el repositorio local.
   - En el repositorio local, crea un archivo llamado `Shape.java` con la estructura básica de una clase en la raíz del repositorio.

6. **Desarrollador 2**: Realizar un pull del repositorio.
   ```bash
   git pull origin main
   ```

7. **Desarrollador 3**: Realizar un pull del repositorio.
   ```bash
   git pull origin main
   ```

8. **Desarrollador 1**: Crear una rama.
   ```bash
   git checkout -b triangle_feature
   ```

9. **Desarrollador 2**: Crear una rama.
   ```bash
   git checkout -b circle_feature
   ```

10. **Desarrollador 3**: Crear una rama.
    ```bash
    git checkout -b square_feature
    ```

11. **Desarrollador 1**: Crear la clase Triangle.java en el repositorio local.
    - En el repositorio local, crea un archivo llamado `Triangle.java` con la implementación de la clase Triangle en la rama `triangle_feature`.

12. **Desarrollador 2**: Crear la clase Circle.java en el repositorio local.
    - En el repositorio local, crea un archivo llamado `Circle.java` con la implementación de la clase Circle en la rama `circle_feature`.

13. **Desarrollador 3**: Crear la clase Square.java en el repositorio local.
    - En el repositorio local, crea un archivo llamado `Square.java` con la implementación de la clase Square en la rama `square_feature`.

14. **Desarrollador 1**: Hacer commit y push.
    ```bash
    git add Triangle.java
    git commit -m "Agregando clase Triangle"
    git push origin triangle_feature
    ```

15. **Desarrollador 2**: Hacer commit y push.
    ```bash
    git add Circle.java
    git commit -m "Agregando clase Circle"
    git push origin circle_feature
    ```

16. **Desarrollador 3**: Hacer commit y push.
    ```bash
    git add Square.java
    git commit -m "Agregando clase Square"
    git push origin square_feature
    ```

17. **Desarrollador 1**: Crear una solicitud de extracción.
    - Desde GitHub, crea una solicitud de extracción (pull request) para fusionar la rama `triangle_feature` en la rama `main`.

18. **Desarrollador 2**: Crear una solicitud de extracción.
    - Desde GitHub, crea una solicitud de extracción (pull request) para fusionar la rama `circle_feature` en la rama `main`.

19. **Desarrollador 3**: Crear una solicitud de extracción.
    - Desde GitHub, crea una solicitud de extracción (pull request) para fusionar la rama `square_feature` en la rama `main`.

20. **Desarrollador 1**: Actualizar el repositorio local.
    ```bash
    git pull origin main
    ```

21. **Desarrollador 2**: Actualizar el repositorio local.
    ```bash
    git pull origin main
    ```

22. **Desarrollador 3**: Actualizar el repositorio local.
    ```bash
    git pull origin main
    ```