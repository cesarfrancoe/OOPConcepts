# Guía para trabajo colaborativo con Git y GitHub

Esta guía presenta una práctica básica de trabajo colaborativo utilizando **Git** y **GitHub**. El objetivo es comprender cómo varios desarrolladores pueden trabajar simultáneamente sobre un mismo proyecto, registrar sus cambios localmente, compartirlos mediante un repositorio remoto y sincronizar el trabajo realizado por otros integrantes del equipo.

La práctica será realizada por tres desarrolladores que trabajarán sobre un proyecto denominado `LibraryRepo`.

La práctica está organizada por **fases**. Algunas actividades deben realizarse de manera secuencial, mientras que otras pueden realizarse **en paralelo**, tal como ocurre durante el desarrollo colaborativo de un proyecto.

## Requisitos previos

Antes de iniciar la práctica, cada desarrollador debe contar con:

- Una cuenta activa en **GitHub**.
- **Git instalado** en su computador.
- **Visual Studio Code (VS Code)** instalado, o un editor de código equivalente.
- Acceso a una **terminal del sistema operativo**.

Todos los comandos de Git presentados en esta guía deberán ingresarse desde una terminal del sistema operativo. En **Windows** se utilizará como referencia **CMD (Símbolo del sistema)**; en **macOS** y **Linux** se puede utilizar la aplicación Terminal correspondiente.

### Verificar la instalación de Git

Abra una terminal y ejecute:

```bash
git --version
```

Si Git se encuentra correctamente instalado, deberá mostrarse la versión instalada. Por ejemplo:

```text
git version 2.51.0
```

El número de versión puede ser diferente dependiendo de la instalación.

Si el comando no es reconocido, deberá instalar Git antes de continuar con la práctica.

> **Importante:** salvo que se indique expresamente lo contrario, todos los comandos mostrados en esta guía deben ejecutarse desde la terminal y estando ubicado en la carpeta correspondiente al repositorio.

---

# Fase 1. Preparación del repositorio remoto

Esta fase debe ser realizada inicialmente por un solo integrante del equipo.

## 1. Crear el repositorio en GitHub

El **Desarrollador 1** debe iniciar sesión en GitHub y crear un nuevo repositorio denominado:

```text
LibraryRepo
```

Al crear el repositorio, inicialícelo con un archivo `README.md`.

Una vez creado el repositorio, el Desarrollador 1 debe agregar a los Desarrolladores 2 y 3 como colaboradores.

Los Desarrolladores 2 y 3 deben aceptar la invitación antes de continuar.

---

# Fase 2. Preparación de los repositorios locales

Una vez creado el repositorio y aceptadas las invitaciones, **los tres desarrolladores pueden realizar las siguientes actividades en paralelo desde sus respectivos computadores**.

## 2. Ubicarse en la carpeta Documents

Cada desarrollador debe almacenar su copia local del repositorio dentro de la carpeta `Documents` de su usuario.

La carpeta de usuario es el directorio que contiene los archivos personales asociados a cada usuario del sistema operativo. Algunas ubicaciones habituales son:

```text
Windows:
C:\Users\NombreUsuario

macOS:
/Users/NombreUsuario

Linux:
/home/NombreUsuario
```

Dentro de esta carpeta normalmente se encuentran directorios como `Documents` y `Downloads`.

Para ubicarse en `Documents`, ejecute:

### Windows (CMD)

```cmd
cd %USERPROFILE%\Documents
```

### macOS y Linux

```bash
cd ~/Documents
```

## 3. Clonar el repositorio

Cada desarrollador debe obtener desde GitHub la URL del repositorio `LibraryRepo`.

Posteriormente debe ejecutar:

```bash
git clone <URL_DEL_REPOSITORIO>
```

Por ejemplo:

```bash
git clone https://github.com/usuario/LibraryRepo.git
```

Git descargará el contenido del repositorio y creará dentro de `Documents` una carpeta denominada:

```text
LibraryRepo
```

Ingrese a ella:

```bash
cd LibraryRepo
```

## 4. Comprobar el estado del repositorio

Ejecute:

```bash
git status
```

Git deberá indicar que el repositorio se encuentra actualizado y que no existen cambios pendientes.

El comando `git status` permite consultar el estado de los archivos del repositorio y será utilizado varias veces durante esta práctica.

## 5. Abrir el repositorio en Visual Studio Code

Estando ubicado dentro de `LibraryRepo` desde la terminal, puede abrir la carpeta completa del repositorio en **Visual Studio Code (VS Code)** ejecutando:

```bash
code .
```

El punto (`.`) representa la carpeta actual. Por tanto, el comando anterior indica a VS Code que abra la carpeta en la que se encuentra actualmente la terminal.

Si el comando `code` no está disponible, abra VS Code y seleccione:

```text
File > Open Folder...
```

o su equivalente:

```text
Archivo > Abrir carpeta...
```

Seleccione posteriormente la carpeta `LibraryRepo` ubicada dentro de `Documents`.

Es importante abrir **la carpeta completa del repositorio** y no únicamente un archivo individual.

---

# Fase 3. Creación inicial del proyecto

Esta fase debe realizarse de manera **secuencial**.

## 6. Crear la clase Library

El **Desarrollador 1** debe crear, desde el explorador de archivos de VS Code, el archivo:

```text
Library.java
```

Inicialmente, el archivo debe contener únicamente la declaración de la clase vacía:

```java
public class Library {

}
```

Guarde el archivo.

## 7. Consultar los cambios

Regrese a la terminal y ejecute:

```bash
git status
```

Git deberá mostrar `Library.java` como un archivo nuevo que todavía no está siendo rastreado (*untracked file*).

## 8. Preparar el archivo

Ejecute:

```bash
git add Library.java
```

Consulte nuevamente el estado:

```bash
git status
```

Observe cómo cambia el estado de `Library.java` después de ejecutar `git add`.

## 9. Crear el commit

Ejecute:

```bash
git commit -m "Add Library class"
```

Un **commit** registra un conjunto de cambios en el historial del repositorio local.

Compruebe nuevamente el estado:

```bash
git status
```

## 10. Publicar el cambio

El commit creado hasta este momento existe únicamente en el repositorio local del Desarrollador 1.

Para enviarlo al repositorio remoto en GitHub, ejecute:

```bash
git push origin main
```

## 11. Sincronizar los demás repositorios

Los Desarrolladores 2 y 3 todavía tienen la versión que clonaron inicialmente.

Para obtener los cambios publicados por el Desarrollador 1 deben ejecutar:

```bash
git pull origin main
```

Compruebe desde VS Code que ahora los tres desarrolladores tienen el archivo:

```text
Library.java
```

Todos deben partir de este mismo estado antes de continuar.

---

# Fase 4. Trabajo colaborativo en paralelo

A partir de este momento, los tres desarrolladores trabajarán **en paralelo**.

Cada desarrollador creará un archivo diferente:

| Desarrollador | Archivo |
|---|---|
| Desarrollador 1 | `Book.java` |
| Desarrollador 2 | `Author.java` |
| Desarrollador 3 | `Publisher.java` |

Debido a que cada desarrollador modificará un archivo diferente, Git podrá posteriormente integrar los cambios sin que exista un conflicto sobre su contenido.

## 12. Desarrollador 1: crear Book

Desde VS Code, el Desarrollador 1 debe crear el archivo:

```text
Book.java
```

con el siguiente contenido:

```java
public class Book {

}
```

Guarde el archivo.

Compruebe el cambio:

```bash
git status
```

Prepare el archivo:

```bash
git add Book.java
```

Cree el commit:

```bash
git commit -m "Add Book class"
```

## 13. Desarrollador 2: crear Author

Desde VS Code, el Desarrollador 2 debe crear el archivo:

```text
Author.java
```

con el siguiente contenido:

```java
public class Author {

}
```

Guarde el archivo.

Compruebe el cambio:

```bash
git status
```

Prepare el archivo:

```bash
git add Author.java
```

Cree el commit:

```bash
git commit -m "Add Author class"
```

## 14. Desarrollador 3: crear Publisher

Desde VS Code, el Desarrollador 3 debe crear el archivo:

```text
Publisher.java
```

con el siguiente contenido:

```java
public class Publisher {

}
```

Guarde el archivo.

Compruebe el cambio:

```bash
git status
```

Prepare el archivo:

```bash
git add Publisher.java
```

Cree el commit:

```bash
git commit -m "Add Publisher class"
```

En este momento, los tres desarrolladores han realizado cambios diferentes y creado sus respectivos commits de manera independiente.

---

# Fase 5. Publicación e integración de cambios sin conflictos

Los tres desarrolladores tienen ahora commits diferentes en sus respectivos repositorios locales, pero todos comparten la misma rama `main` del repositorio remoto.

La publicación se realizará de manera **secuencial** para observar cómo se sincronizan diferentes repositorios locales.

## 15. Publicar Book

El Desarrollador 1 ejecuta:

```bash
git push origin main
```

El archivo `Book.java` quedará publicado en GitHub.

## 16. Publicar Author

El repositorio local del Desarrollador 2 todavía no contiene el commit realizado por el Desarrollador 1.

Si intenta ejecutar:

```bash
git push origin main
```

Git rechazará la operación porque el repositorio remoto contiene cambios que todavía no existen en su repositorio local.

Antes de publicar, debe incorporar esos cambios:

```bash
git pull origin main
```

Como los desarrolladores modificaron archivos diferentes, Git puede integrar automáticamente ambos trabajos.

Compruebe que ahora el Desarrollador 2 también dispone de:

```text
Book.java
```

Posteriormente publique los cambios:

```bash
git push origin main
```

Ahora el repositorio remoto contiene `Book.java` y `Author.java`.

## 17. Publicar Publisher

El Desarrollador 3 se encuentra en una situación equivalente.

Si intenta publicar directamente:

```bash
git push origin main
```

Git rechazará la operación debido a que existen cambios más recientes en el repositorio remoto.

Debe obtenerlos mediante:

```bash
git pull origin main
```

Git incorporará automáticamente los cambios correspondientes a `Book.java` y `Author.java`.

Posteriormente ejecute:

```bash
git push origin main
```

El repositorio remoto deberá contener ahora:

```text
Library.java
Book.java
Author.java
Publisher.java
```

## 18. Sincronizar los tres repositorios

Los tres desarrolladores deben ejecutar:

```bash
git pull origin main
```

Comprueben que todos tienen exactamente los mismos archivos.

La estructura del proyecto será:

```text
LibraryRepo
├── Author.java
├── Book.java
├── Library.java
├── Publisher.java
└── README.md
```

---

# Fase 6. Trabajo colaborativo sobre un mismo archivo

Hasta este punto, cada desarrollador ha trabajado sobre archivos diferentes. Aunque las modificaciones fueron realizadas de manera simultánea, Git pudo integrarlas automáticamente porque no existían modificaciones incompatibles sobre el mismo contenido.

En un proyecto real es frecuente que dos o más desarrolladores necesiten modificar simultáneamente un mismo archivo.

Git intenta combinar automáticamente los cambios realizados por diferentes desarrolladores. Incluso cuando dos personas modifican el mismo archivo, Git puede realizar la integración automáticamente si los cambios afectan regiones diferentes.

Sin embargo, cuando existen modificaciones incompatibles sobre las mismas líneas o sobre una misma región del archivo, Git no puede determinar automáticamente cuál debe ser el resultado. Esta situación se denomina **conflicto de merge (*merge conflict*)**.

Un conflicto no significa que se haya perdido información ni que el repositorio esté dañado. Significa que Git necesita que un desarrollador determine manualmente cómo deben combinarse las diferentes modificaciones.

En las siguientes fases se provocará intencionalmente esta situación para observar cómo Git identifica un conflicto y cómo puede resolverse.

## 19. Verificar el punto de partida

Antes de continuar, los tres desarrolladores deben ejecutar:

```bash
git pull origin main
```

El archivo `Library.java` debe ser exactamente igual para todos:

```java
public class Library {

}
```

Es importante que **los tres desarrolladores completen este paso antes de que cualquiera continúe**.

---

# Fase 7. Modificación simultánea de Library

Una vez comprobado que todos tienen exactamente la misma versión de `Library.java`, los tres desarrolladores realizarán las siguientes actividades **en paralelo**.

Durante esta fase, ningún desarrollador debe ejecutar `git pull` ni `git push` hasta que se indique expresamente.

## 20. Desarrollador 1: agregar books

El Desarrollador 1 debe modificar `Library.java` para que contenga:

```java
public class Library {

    private Book[] books = new Book[]{};

}
```

Prepare el cambio:

```bash
git add Library.java
```

Cree el commit:

```bash
git commit -m "Add books collection to Library"
```

## 21. Desarrollador 2: agregar authors

El Desarrollador 2 debe modificar su propia copia de `Library.java` para que contenga:

```java
public class Library {

    private Author[] authors = new Author[]{};

}
```

Prepare el cambio:

```bash
git add Library.java
```

Cree el commit:

```bash
git commit -m "Add authors collection to Library"
```

## 22. Desarrollador 3: agregar publishers

El Desarrollador 3 debe modificar su propia copia de `Library.java` para que contenga:

```java
public class Library {

    private Publisher[] publishers = new Publisher[]{};

}
```

Prepare el cambio:

```bash
git add Library.java
```

Cree el commit:

```bash
git commit -m "Add publishers collection to Library"
```

En este momento los tres repositorios locales contienen versiones diferentes de `Library.java`, todas creadas a partir de la misma versión original.

---

# Fase 8. Publicación y aparición del conflicto

Esta fase vuelve a realizarse de manera **secuencial**.

## 23. Publicar el cambio del Desarrollador 1

El Desarrollador 1 ejecuta:

```bash
git push origin main
```

Su modificación queda publicada correctamente.

El repositorio remoto contiene ahora:

```java
public class Library {

    private Book[] books = new Book[]{};

}
```

## 24. Intentar publicar el cambio del Desarrollador 2

El Desarrollador 2 intenta publicar su commit:

```bash
git push origin main
```

Git rechazará la operación porque `main` en GitHub contiene cambios que todavía no existen en su repositorio local.

Es importante distinguir esta situación:

> **El rechazo del `push` todavía no es un conflicto de merge.**

Git simplemente está indicando que el repositorio remoto ha avanzado y que primero deben incorporarse esos cambios.

## 25. Obtener los cambios remotos

El Desarrollador 2 ejecuta:

```bash
git pull origin main
```

Git intentará integrar el cambio remoto:

```java
private Book[] books = new Book[]{};
```

con el cambio local:

```java
private Author[] authors = new Author[]{};
```

Como ambas modificaciones se realizaron sobre la misma región de `Library.java`, Git no puede determinar automáticamente cómo deben combinarse.

Se produce entonces un **conflicto de merge**.

---

# Fase 9. Resolución del conflicto

## 26. Consultar el estado

El Desarrollador 2 debe ejecutar:

```bash
git status
```

Git indicará que `Library.java` presenta un conflicto que debe resolverse.

Abra `Library.java` desde VS Code.

Git representará las modificaciones en conflicto mediante marcadores similares a los siguientes:

```text
<<<<<<< HEAD
    private Author[] authors = new Author[]{};
=======
    private Book[] books = new Book[]{};
>>>>>>> ...
```

Los marcadores delimitan las diferentes versiones que Git no pudo combinar automáticamente:

```text
<<<<<<< HEAD
cambio existente en el repositorio local
=======
cambio que se está intentando integrar
>>>>>>> ...
```

## 27. Resolver el conflicto

En este caso ambas modificaciones son necesarias.

Edite manualmente `Library.java`, elimine los marcadores del conflicto y conserve ambos atributos:

```java
public class Library {

    private Book[] books = new Book[]{};
    private Author[] authors = new Author[]{};

}
```

Guarde el archivo.

## 28. Marcar el conflicto como resuelto

Compruebe inicialmente el estado:

```bash
git status
```

Posteriormente prepare el archivo corregido:

```bash
git add Library.java
```

Consulte nuevamente:

```bash
git status
```

Git deberá indicar que el conflicto ha sido resuelto y que el archivo está preparado para completar la integración.

Cree el commit:

```bash
git commit -m "Resolve Library merge conflict"
```

## 29. Publicar el resultado

Ejecute:

```bash
git push origin main
```

El repositorio remoto contendrá ahora:

```java
public class Library {

    private Book[] books = new Book[]{};
    private Author[] authors = new Author[]{};

}
```

---

# Fase 10. Resolución del siguiente conflicto

El Desarrollador 3 todavía tiene localmente:

```java
public class Library {

    private Publisher[] publishers = new Publisher[]{};

}
```

mientras que el repositorio remoto contiene las modificaciones realizadas por los Desarrolladores 1 y 2.

## 30. Intentar publicar

El Desarrollador 3 ejecuta:

```bash
git push origin main
```

Git rechazará la operación porque el repositorio remoto contiene cambios que todavía no existen en su repositorio local.

## 31. Obtener los cambios

Ejecute:

```bash
git pull origin main
```

Git intentará integrar ambas versiones de `Library.java`.

Consulte el estado:

```bash
git status
```

Abra `Library.java` desde VS Code y analice las modificaciones que Git identifica como incompatibles.

## 32. Resolver el conflicto

Edite `Library.java`, elimine los marcadores generados por Git y conserve los cambios realizados por los tres desarrolladores:

```java
public class Library {

    private Book[] books = new Book[]{};
    private Author[] authors = new Author[]{};
    private Publisher[] publishers = new Publisher[]{};

}
```

Guarde el archivo.

## 33. Registrar la resolución

Prepare el archivo:

```bash
git add Library.java
```

Cree el commit:

```bash
git commit -m "Resolve Library merge conflict"
```

Finalmente publique el resultado:

```bash
git push origin main
```

---

# Fase 11. Sincronización final

El repositorio remoto contiene ahora el trabajo realizado por los tres desarrolladores.

Todos deben sincronizar nuevamente sus repositorios locales:

```bash
git pull origin main
```

Compruebe el estado:

```bash
git status
```

Los tres desarrolladores deben tener exactamente la misma versión del proyecto.

La estructura final será:

```text
LibraryRepo
├── Author.java
├── Book.java
├── Library.java
├── Publisher.java
└── README.md
```

El archivo `Library.java` deberá contener:

```java
public class Library {

    private Book[] books = new Book[]{};
    private Author[] authors = new Author[]{};
    private Publisher[] publishers = new Publisher[]{};

}
```

---

# Resultado de la práctica

Al finalizar esta práctica, los estudiantes habrán utilizado un repositorio Git compartido para experimentar un flujo básico de trabajo colaborativo.

En particular, habrán realizado las siguientes operaciones:

- Verificar la instalación de Git mediante `git --version`.
- Utilizar una terminal del sistema operativo para ejecutar comandos de Git.
- Clonar un repositorio remoto mediante `git clone`.
- Navegar hasta el repositorio utilizando la terminal.
- Abrir la carpeta de un repositorio desde Visual Studio Code.
- Consultar el estado del repositorio mediante `git status`.
- Identificar archivos nuevos y modificados.
- Preparar cambios mediante `git add`.
- Registrar cambios localmente mediante `git commit`.
- Publicar cambios mediante `git push`.
- Obtener e integrar cambios realizados por otros desarrolladores mediante `git pull`.
- Trabajar simultáneamente sobre archivos diferentes.
- Integrar automáticamente cambios que no presentan conflictos.
- Identificar el rechazo de un `push` cuando el repositorio remoto contiene cambios más recientes.
- Diferenciar un `push` rechazado de un conflicto de merge.
- Trabajar simultáneamente sobre un mismo archivo.
- Identificar un conflicto de merge.
- Interpretar los marcadores utilizados por Git para representar un conflicto.
- Resolver manualmente un conflicto utilizando Visual Studio Code.
- Registrar y publicar el resultado de una resolución.
- Sincronizar finalmente los repositorios locales de todos los integrantes del equipo.
