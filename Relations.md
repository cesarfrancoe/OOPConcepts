# Programación Orientada a Objetos

# Introducción

En la Programación Orientada a Objetos (POO), las clases no se utilizan de forma aislada. En la práctica, los sistemas están compuestos por múltiples clases que **interactúan y se relacionan entre sí** para representar entidades y comportamientos del mundo real.

Estas relaciones no solo permiten organizar el código, sino que constituyen una parte fundamental del **diseño del sistema**, ya que determinan:

* El nivel de acoplamiento entre clases
* La responsabilidad de cada objeto
* La gestión del ciclo de vida de los objetos
* La flexibilidad y mantenibilidad del sistema

Desde el punto de vista del modelado, estas relaciones se representan mediante el **diagrama de clases UML (UML Class Diagram)**, donde se definen aspectos como:

* Tipo de relación (asociación, agregación, composición)
* Cardinalidad (cuántos objetos participan en la relación)
* Direccionalidad (qué clase conoce a la otra)

En este documento se estudiarán tres tipos fundamentales de relaciones entre clases:

* **Asociación**: relación débil basada en conocimiento o uso
* **Agregación**: relación todo-parte con independencia de ciclo de vida
* **Composición**: relación todo-parte con dependencia total

Además, se analizarán conceptos complementarios necesarios para un modelado correcto:

* Cardinalidad
* Direccionalidad
* Representación en UML (diagrama de clases)
* Relaciones de tipo uno a uno, uno a muchos y muchos a muchos

El objetivo no es únicamente implementar estas relaciones en Java, sino **comprender cuándo utilizar cada una** en función del problema que se desea modelar.

# 1. Estructura de una relación en UML

Antes de estudiar los tipos de relaciones entre clases, es necesario entender **cómo se representa una relación en un diagrama de clases UML**.

Una relación entre dos clases se compone de tres elementos fundamentales:

* Las clases
* La línea de conexión
* La cardinalidad (multiplicidad)

---

## Representación básica

```text
[ClassA] --------> [ClassB]
      1              0..*
```

---

## Clases

Las clases se representan como **rectángulos (cajas)**.

Cada caja corresponde a una clase del sistema:

```text
[Person]        [Passport]
```

---

## Línea de relación

Las clases se conectan mediante una **línea**, que representa la existencia de una relación.

En este documento, siempre se utilizará una **línea con flecha** para indicar direccionalidad:

```text
Person --------> Passport
```

Interpretación:

* `Person` conoce a `Passport`
* `Person` tiene una referencia hacia `Passport`

Adicionalmente, según el tipo de relación, la línea puede incluir un símbolo en uno de sus extremos:

* **Sin símbolo** → Asociación
* **Rombo blanco (◇)** → Agregación
* **Rombo negro (◆)** → Composición

El símbolo siempre se ubica en el lado de la clase que representa el **todo** en una relación todo-parte.

---

## Cardinalidad (multiplicidad)

La cardinalidad se ubica en **cada extremo de la línea**, no en el centro.

Indica cuántas instancias de una clase pueden relacionarse con instancias de la clase del otro extremo.

```text
Person --------> Passport
   1               0..1
```

Interpretación:

* El `0..1` cerca de `Passport` indica cuántos pasaportes puede tener una persona
* El `1` cerca de `Person` indica a cuántas personas puede estar asociado un pasaporte (por ejemplo: `1`, `0..1`, `0..*`, etc., según el modelo)

> La cardinalidad siempre se interpreta desde el extremo opuesto de la relación.

---

## Tipos de cardinalidad

La cardinalidad puede expresarse de dos formas:

### Valor único

Cuando se muestra un solo número (por ejemplo, `1`):

* Indica una **cantidad exacta**
* No hay variación posible

Ejemplo:

* `1` → exactamente una instancia

---

### Rango (mínimo..máximo)

Cuando se expresa como un rango:

* El primer valor indica el **mínimo**
* El segundo valor indica el **máximo**

Ejemplos:

* `0..1` → cero o una instancia (opcional)
* `1..*` → una o muchas instancias
* `0..*` → cero o muchas instancias

---

## Nota importante

> El símbolo `*` representa “muchos”, es decir, un número no limitado de instancias.

> En UML es común utilizar `*` como abreviación de `0..*`. Sin embargo, en este documento se utilizará siempre `0..*` para hacer explícito que la relación permite desde cero hasta muchas instancias.

---

## Ejemplo completo

```text
[School] --------> [Teacher]
     1                0..*
```

Interpretación:

* Una escuela puede tener muchos docentes
* Un docente está asociado a una escuela (según este modelo)
* Solo `School` conoce a `Teacher`

---

## Conclusión

Una relación en UML se define mediante:

* Dos clases (cajas)
* Una línea con dirección (flecha)
* Una cardinalidad en cada extremo

Este esquema será la base para entender los diferentes tipos de relaciones entre clases.

## 2. Asociación

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

    public void setNumber(String newNumber){
        number = newNumber;
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

**Justificación:**

1. **`Passport` es creado fuera de `Person`**: La clase `Person` recibe o asigna un pasaporte ya existente, sin crearlo ni destruirlo. Esto permite la independencia entre los objetos.
2. **Flexibilidad total**: El pasaporte puede cambiarse dinámicamente mediante `setPassport()`, y la persona puede existir incluso sin uno. La relación es claramente opcional.
3. **Relación débil y no estructural**: `Person` conoce a `Passport`, pero no depende de él para existir. No hay una relación de propiedad ni de composición.


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

**Justificación:**

1. **Los objetos `Teacher` se crean fuera de `School`**: La escuela no es responsable de construir los docentes; simplemente los recibe y almacena. Esto permite que los mismos docentes puedan estar asociados a distintas escuelas si se desea.
2. **La relación es opcional y dinámica**: La lista de docentes puede establecerse o modificarse en cualquier momento mediante `setTeachers()`. Incluso podría quedar vacía sin afectar la existencia de `School`.
3. **No hay dependencia estructural**: `School` conoce a los `Teacher`, pero su existencia y funcionamiento no dependen de ellos. Esto confirma que se trata de una relación de asociación y no de agregación o composición.


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

    public String getModel() {
        return model;
    }

    public void setModel(String newModel) {
        model = newModel;
    }
}
```

```java
public class Car {
    private String plate;
    private Engine engine;

    public Car(String newPlate) {
        plate = newPlate;
    }

    public Car(String newPlate, Engine newEngine) {
        this(newPlate);
        setEngine(newEngine);
    }

    public Engine getEngine() {
        return engine;
    }

    public void setEngine(Engine newEngine) {
        if (newEngine != null) {
            engine = newEngine;
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

**Justificación:**

1. **El objeto `Engine` se construye fuera de `Car`**: El motor no es creado internamente por el carro, sino que se recibe como parámetro, permitiendo que exista de forma independiente.
2. **La clase `Car` valida y asigna el motor mediante un setter**: Esto permite establecer o cambiar el motor dinámicamente, siempre que sea válido.
3. **Independencia de ciclo de vida**: El motor podría ser compartido por otras clases, sustituido o eliminado sin afectar la existencia del objeto `Car`. Por tanto, se trata de una relación de agregación.


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

