# Programación Orientada a Objetos
# Relaciones entre Clases (sin herencia)

**Objetivo:** Entender los diferentes tipos de relaciones entre clases en POO: asociación, agregación y composición, sus diferencias conceptuales y cómo implementarlas en Java con relaciones de tipo uno a uno y uno a muchos.

## Introducción

En la Programación Orientada a Objetos, las clases no solo definen objetos individuales, también se relacionan entre sí para formar sistemas más complejos. Estas relaciones permiten modelar el comportamiento y las estructuras del mundo real.

## 1. Asociación

### Definición

La asociación ocurre cuando una clase usa o conoce a otra, pero no es responsable de su creación ni destrucción. Es una relación más débil y flexible.

### Características:

* No hay dependencia del ciclo de vida.
* Representa un vínculo lógico entre objetos.
* Puede ser uno a uno o uno a muchos.
* Puede ser unidireccional o bidireccional.

### Ejemplo 1: Asociación uno a uno

```java
public class Passport {
    private String number;

    public Passport(String number) {
        this.number = number;
    }

    public String getNumber() {
        return number;
    }
}
```

```java
public class Person {
    private String name;
    private Passport passport;

    public Person(String name, Passport passport) {
        this.name = name;
        this.passport = passport;
    }

    public Passport getPassport() {
        return passport;
    }
}
```

```java
public class TestPerson {
    public static void main(String[] args) {
        Passport passport = new Passport("A1234567");
        Person person = new Person("Jane", passport);

        System.out.println("Pasaporte de " + person.getPassport().getNumber());
    }
}
```

### Ejemplo 2: Asociación uno a muchos

```java
public class Teacher {
    private String name;

    public Teacher(String name) {
        this.name = name;
    }
}
```

```java
import java.util.List;

public class School {
    private List<Teacher> teachers;

    public School(List<Teacher> teachers) {
        this.teachers = teachers;
    }

    public List<Teacher> getTeachers() {
        return teachers;
    }
}
```

```java
import java.util.ArrayList;
import java.util.List;

public class TestSchool {
    public static void main(String[] args) {
        List<Teacher> teachers = new ArrayList<>();
        teachers.add(new Teacher("John"));
        teachers.add(new Teacher("Jane"));

        School school = new School(teachers);

        for (Teacher t : school.getTeachers()) {
            System.out.println("Docente: " + t.getName());
        }
    }
}
```

## 2. Agregación

### Definición

La agregación representa una relación "tiene un", en la que una clase contiene a otra, pero las partes pueden seguir existiendo aunque el todo desaparezca. Es una relación fuerte, pero con independencia de ciclo de vida.

### Características:

* El objeto agregado puede existir por sí solo.
* Implica una relación de todo-parte, pero débil.
* Puede ser uno a uno o uno a muchos.

### Ejemplo 1: Agregación uno a uno

```java
public class Engine {
    private String model;

    public Engine(String model) {
        this.model = model;
    }
}
```

```java
public class Car {
    private Engine engine;

    public Car(Engine engine) {
        setEngine(engine);
    }

    public void setEngine(Engine engine) {
        if (engine != null) {
            this.engine = engine;
        }
    }
}
```

```java
public class TestCar {
    public static void main(String[] args) {
        Engine engine = new Engine("V8 Turbo");
        Car car = new Car(engine);

        System.out.println("Motor del auto: " + car.getEngine().getModel());
    }
}
```

### Ejemplo 2: Agregación uno a muchos

```java
public class Book {
    private String title;

    public Book(String title) {
        this.title = title;
    }
}
````

```java
import java.util.ArrayList;
import java.util.List;

public class Library {
    private List<Book> books;

    public Library() {
        this.books = new ArrayList<>();
    }

    public Library(List<Book> books) {
        this();
        for (Book book : books) {
            addBook(book);
        }
    }

    public void addBook(Book book) {
        if (book != null && !books.contains(book)) {
            books.add(book); // validación y control de agregación
        }
    }

    public List<Book> getBooks() {
        return books;
    }
}
```

```java
import java.util.ArrayList;
import java.util.List;

public class TestLibrary {
    public static void main(String[] args) {
        List<Book> books = new ArrayList<>();
        books.add(new Book("Cien años de soledad"));
        books.add(new Book("El Principito"));

        Library library = new Library(books);

        for (Book book : library.getBooks()) {
            System.out.println("Libro: " + book.getTitle());
        }
    }
}
```

## 3. Composición

### Definición

La composición también es una relación todo-parte, pero en este caso el todo es dueño total de las partes. Las partes no existen sin el todo y su ciclo de vida está completamente ligado.

### Características:

* El objeto compuesto crea y destruye sus componentes.
* La dependencia es fuerte.
* No puede compartir sus partes con otros objetos.
* Puede ser uno a uno o uno a muchos.

### Ejemplo 1: Composición uno a uno

```java
public class Heart {
    private int beatsPerMinute;

    public Heart(int bpm) {
        this.beatsPerMinute = bpm;
    }
}
```

```java
public class Human {
    private final Heart heart;

    public Human() {
        this.heart = new Heart(72);
    }
}
```

```java
public class TestHuman {
    public static void main(String[] args) {
        Human human = new Human();
        System.out.println("Latidos por minuto: " + human.getHeart().getBeatsPerMinute());
    }
}
```

### Ejemplo 2: Composición uno a muchos

```java
public class Page {
    private int pageNumber;

    public Page(int number) {
        this.pageNumber = number;
    }
}
```

```java
public class Document {
    private List<Page> pages;

    public Document(int totalPages) {
        pages = new ArrayList<>();
        for (int i = 1; i <= totalPages; i++) {
            pages.add(new Page(i));
        }
    }
}
```

```java
public class TestDocument {
    public static void main(String[] args) {
        Document doc = new Document(3);
        for (Page p : doc.getPages()) {
            System.out.println("Página: " + p.getPageNumber());
        }
    }
}
```


## Comparación General

| Tipo de Relación | Ciclo de vida compartido | Propiedad | Ejemplo             |
| ---------------- | ------------------------ | --------- | ------------------- |
| Asociación       | No                       | No        | Estudiante – Curso  |
| Agregación       | No (pero lógica fuerte)  | Parcial   | Biblioteca – Libros |
| Composición      | Sí                       | Total     | Documento – Páginas |


## Comparación: ¿Se implementan igual?

| Característica                             | Asociación                  | Agregación                  | Composición                    |
| ------------------------------------------ | --------------------------- | --------------------------- | ------------------------------ |
| ¿Quién crea la instancia del objeto parte? | Fuera de la clase principal | Fuera de la clase principal | Dentro de la clase principal   |
| ¿Se pasa por constructor?                  | Sí o no (opcional)          | Generalmente sí             | No, se crean dentro del objeto |
| ¿Puede compartirse la parte con otros?     | Sí                          | Sí                          | No                             |
| ¿Dependencia de ciclo de vida?             | No                          | No                          | Sí                             |
| ¿Referencia nula posible?                  | Sí                          | Sí                          | Generalmente no                |

