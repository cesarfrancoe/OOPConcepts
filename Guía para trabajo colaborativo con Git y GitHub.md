### Guía para Trabajo Colaborativo con Git/GitHub – Proyecto LibraryRepo

Esta guía detalla los pasos necesarios para llevar a cabo un proyecto colaborativo utilizando Git y GitHub. El proyecto implica la creación de un repositorio llamado **LibraryRepo**, donde se desarrollarán diferentes clases relacionadas con la gestión de una biblioteca. El Desarrollador 1 será responsable de coordinar el flujo de trabajo y gestionar el repositorio, mientras que los Desarrolladores 2 y 3 contribuirán con la implementación de clases específicas.

1. **Desarrollador 1**: Crear el repositorio en GitHub y agregar colaboradores.

   * Inicia sesión en GitHub y crea un nuevo repositorio llamado **LibraryRepo**.
   * Invita a los otros dos desarrolladores agregando sus nombres de usuario de GitHub.

2. **Desarrollador 1**: Clonar el repositorio.

   * Clona el repositorio en tu repositorio local utilizando el comando `git clone <URL_del_LibraryRepo>`.

3. **Desarrollador 2**: Clonar el repositorio.

   * Clona el repositorio en tu repositorio local usando `git clone <URL_del_LibraryRepo>`.

4. **Desarrollador 3**: Clonar el repositorio.

   * Clona el repositorio en tu repositorio local usando `git clone <URL_del_LibraryRepo>`.

5. **Desarrollador 1**: Crear la clase Library.java en el repositorio local.

   * En el repositorio local, crea un archivo llamado `Library.java` con la estructura básica de una clase en la raíz del repositorio.

6. **Desarrollador 1**: Realizar push de la clase Library.java.

   ```bash
   git add Library.java
   git commit -m "Agregando clase Library"
   git push origin main
   ```

7. **Desarrollador 2**: Realizar un pull del repositorio.

   ```bash
   git pull origin main
   ```

8. **Desarrollador 3**: Realizar un pull del repositorio.

   ```bash
   git pull origin main
   ```

9. **Desarrollador 1**: Crear una rama.

   ```bash
   git checkout -b book_feature
   ```

10. **Desarrollador 2**: Crear una rama.

    ```bash
    git checkout -b author_feature
    ```

11. **Desarrollador 3**: Crear una rama.

    ```bash
    git checkout -b publisher_feature
    ```

12. **Desarrollador 1**: Crear la clase Book.java en el repositorio local.

    * En el repositorio local, crea un archivo llamado `Book.java` con la implementación de la clase Book en la rama `book_feature`.

13. **Desarrollador 2**: Crear la clase Author.java en el repositorio local.

    * En el repositorio local, crea un archivo llamado `Author.java` con la implementación de la clase Author en la rama `author_feature`.

14. **Desarrollador 3**: Crear la clase Publisher.java en el repositorio local.

    * En el repositorio local, crea un archivo llamado `Publisher.java` con la implementación de la clase Publisher en la rama `publisher_feature`.

15. **Desarrollador 1**: Hacer commit y push.

```bash
git add Book.java
git commit -m "Agregando clase Book"
git push origin book_feature
```

16. **Desarrollador 2**: Hacer commit y push.

```bash
git add Author.java
git commit -m "Agregando clase Author"
git push origin author_feature
```

17. **Desarrollador 3**: Hacer commit y push.

```bash
git add Publisher.java
git commit -m "Agregando clase Publisher"
git push origin publisher_feature
```

18. **Desarrollador 1**: Crear una solicitud de extracción.

* Desde GitHub, crea una solicitud de extracción (pull request) para fusionar la rama `book_feature` en la rama `main`.

19. **Desarrollador 2**: Crear una solicitud de extracción.

* Desde GitHub, crea una solicitud de extracción (pull request) para fusionar la rama `author_feature` en la rama `main`.

20. **Desarrollador 3**: Crear una solicitud de extracción.

* Desde GitHub, crea una solicitud de extracción (pull request) para fusionar la rama `publisher_feature` en la rama `main`.

21. **Desarrollador 1**: Actualizar el repositorio local.

```bash
git pull origin main
```

22. **Desarrollador 2**: Actualizar el repositorio local.

```bash
git pull origin main
```

23. **Desarrollador 3**: Actualizar el repositorio local.

```bash
git pull origin main
```
