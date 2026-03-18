# Agregación

## Prerrequisito

[Fundamentos de relaciones en UML](UMLBasics.md)

## Definición

La agregación es una relación entre clases de tipo **todo-parte**, en la cual una clase contiene a otra, pero **las partes pueden existir independientemente del todo**.

A diferencia de la asociación, la agregación representa una relación estructural más clara, aunque sin dependencia de ciclo de vida.

En UML, se representa mediante:

* Una línea con dirección
* Un **rombo blanco (◇)** en el lado del “todo”

## Características

* Relación todo-parte
* No hay dependencia del ciclo de vida
* Las partes pueden existir sin el todo
* Puede ser unidireccional o bidireccional
* Puede ser 1:1 o 1:N
* Nivel de acoplamiento medio

## Diferencia clave con Asociación

En asociación:

* Solo hay conocimiento entre clases

En agregación:

* Existe una relación conceptual de **contenedor / contenido**

Sin embargo:

* El objeto contenido **no es creado ni destruido por el contenedor**

## Agregación uno a uno (1:1)

### Representación UML (unidireccional)

```text id="x7l2np"
Car ◇--------> Engine
  1               0..1
```

### Implementación (unidireccional)

```java id="7m91fp"
public class Engine {
    private String model;

    public Engine(String model) {
        this.model = model;
    }

    public String getModel() {
        return model;
    }
}
```

```java id="a4r9qx"
public class Car {
    private String plate;
    private Engine engine;

    public Car(String plate, Engine engine) {
        this.plate = plate;
        this.engine = engine;
    }

    public Engine getEngine() {
        return engine;
    }
}
```

### Test (unidireccional)

```java id="w2k8dt"
public class TestCar {
    public static void main(String[] args) {
        Engine engine = new Engine("V8");
        Car car = new Car("ABC123", engine);

        System.out.println("Motor: " + car.getEngine().getModel());
    }
}
```

### Representación UML (bidireccional)

```text id="m6f3z1"
Car ◇<--------> Engine
  1               0..1
```

### Implementación (bidireccional)

```java id="z9c2kq"
public class Engine {
    private String model;
    private Car car;

    public Engine(String model) {
        this.model = model;
    }

    public String getModel() {
        return model;
    }

    public Car getCar() {
        return car;
    }

    public void setCar(Car newCar) {
        this.car = newCar;
    }
}
```

```java id="n5r7ab"
public class Car {
    private String plate;
    private Engine engine;

    public Car(String plate) {
        this.plate = plate;
    }

    public void setEngine(Engine engine) {
        this.engine = engine;
        if (engine != null && engine.getCar() != this) {
            engine.setCar(this);
        }
    }

    public Engine getEngine() {
        return engine;
    }
}
```

### Test (bidireccional)

```java id="k8q1zm"
public class TestCarBidirectional {
    public static void main(String[] args) {
        Car car = new Car("ABC123");
        Engine engine = new Engine("V8");

        car.setEngine(engine);

        System.out.println("Motor del carro: " + car.getEngine().getModel());
        System.out.println("Carro del motor: " + engine.getCar());
    }
}
```

## Agregación uno a muchos (1:N)

### Representación UML (unidireccional)

```text id="d7p4y1"
Library ◇--------> Book
   1               0..*
```

### Implementación (unidireccional)

```java id="p1k8rz"
public class Book {
    private String title;

    public Book(String title) {
        this.title = title;
    }

    public String getTitle() {
        return title;
    }
}
```

```java id="v9z6bx"
import java.util.List;

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

### Test (unidireccional)

```java id="u3c5vn"
import java.util.ArrayList;
import java.util.List;

public class TestLibrary {
    public static void main(String[] args) {
        List<Book> books = new ArrayList<>();
        books.add(new Book("1984"));
        books.add(new Book("El Principito"));

        Library library = new Library(books);

        for (Book b : library.getBooks()) {
            System.out.println("Libro: " + b.getTitle());
        }
    }
}
```

### Representación UML (bidireccional)

```text id="y6m8q2"
Library ◇<--------> Book
   1               0..*
```

### Implementación (bidireccional)

```java id="t2f7qw"
public class Book {
    private String title;
    private Library library;

    public Book(String title) {
        this.title = title;
    }

    public String getTitle() {
        return title;
    }

    public Library getLibrary() {
        return library;
    }

    public void setLibrary(Library newLibrary) {
        this.library = newLibrary;
    }
}
```

```java id="r8x3kj"
import java.util.ArrayList;
import java.util.List;

public class Library {
    private List<Book> books;

    public Library() {
        this.books = new ArrayList<>();
    }

    public List<Book> getBooks() {
        return books;
    }

    public void addBook(Book book) {
        if (book != null && !books.contains(book)) {
            books.add(book);

            if (book.getLibrary() != this) {
                book.setLibrary(this);
            }
        }
    }

    public void removeBook(Book book) {
        if (book != null && books.contains(book)) {
            books.remove(book);

            if (book.getLibrary() == this) {
                book.setLibrary(null);
            }
        }
    }
}
```

### Test (bidireccional)

```java id="x4n2vb"
public class TestLibraryBidirectional {
    public static void main(String[] args) {
        Library library = new Library();

        Book b1 = new Book("1984");
        Book b2 = new Book("El Principito");

        library.addBook(b1);
        library.addBook(b2);

        for (Book b : library.getBooks()) {
            System.out.println("Libro: " + b.getTitle());
        }

        System.out.println("Biblioteca del libro: " + b1.getLibrary());
    }
}
```

## Consideración importante

Aunque existe una relación estructural, en agregación:

* El objeto contenido **puede existir sin el contenedor**
* Puede ser reutilizado o asociado a otros objetos

## Conclusión

La agregación se utiliza cuando:

* Existe una relación todo-parte
* Las partes tienen vida independiente
* No se desea imponer control sobre el ciclo de vida

Representa un nivel intermedio entre asociación (débil) y composición (fuerte).
