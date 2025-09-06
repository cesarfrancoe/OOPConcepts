# Programación Orientada a Objetos
# Relaciones entre Clases (sin herencia)

**Objetivo:** Entender los diferentes tipos de relaciones entre clases en POO: asociación, agregación y composición, sus diferencias conceptuales y cómo implementarlas en Java con relaciones de tipo uno a uno y uno a muchos.

---

## Introducción

En la Programación Orientada a Objetos, las clases no solo definen objetos individuales, también se relacionan entre sí para formar sistemas más complejos. Estas relaciones permiten modelar el comportamiento y las estructuras del mundo real.

---

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

---

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

public class Car {
    private Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
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

public class Library {
    private List<Book> books;

    public Library(List<Book> books) {
        this.books = books;
    }

    public List<Book> getBooks() {
        return books;
    }
}
```

---

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

public class Human {
    private final Heart heart;

    public Human() {
        this.heart = new Heart(72);
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

---

## Comparación General

| Tipo de Relación | Ciclo de vida compartido | Propiedad | Ejemplo             |
| ---------------- | ------------------------ | --------- | ------------------- |
| Asociación       | No                       | No        | Estudiante – Curso  |
| Agregación       | No (pero lógica fuerte)  | Parcial   | Biblioteca – Libros |
| Composición      | Sí                       | Total     | Documento – Páginas |

---

## Comparación: ¿Se implementan igual?

| Característica                             | Asociación                  | Agregación                  | Composición                    |
| ------------------------------------------ | --------------------------- | --------------------------- | ------------------------------ |
| ¿Quién crea la instancia del objeto parte? | Fuera de la clase principal | Fuera de la clase principal | Dentro de la clase principal   |
| ¿Se pasa por constructor?                  | Sí o no (opcional)          | Generalmente sí             | No, se crean dentro del objeto |
| ¿Puede compartirse la parte con otros?     | Sí                          | Sí                          | No                             |
| ¿Dependencia de ciclo de vida?             | No                          | No                          | Sí                             |
| ¿Referencia nula posible?                  | Sí                          | Sí                          | Generalmente no                |

