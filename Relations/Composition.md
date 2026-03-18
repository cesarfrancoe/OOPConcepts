# Composición

## Prerrequisito

[Fundamentos de relaciones en UML](UMLBasics.md)

## Definición

La composición es una relación entre clases de tipo **todo-parte**, en la cual una clase es **dueña absoluta de sus partes**.

Las partes:

* No pueden existir sin el todo
* Son creadas y destruidas por el todo
* No pueden compartirse con otros objetos

En UML, se representa mediante:

* Una línea con dirección
* Un **rombo negro (◆)** en el lado del “todo”

## Características

* Relación todo-parte fuerte
* Dependencia total del ciclo de vida
* No hay compartición de objetos
* Puede ser unidireccional o bidireccional
* Puede ser 1:1 o 1:N
* Alto acoplamiento

## Diferencia clave con Agregación

En agregación:

* Las partes pueden existir independientemente

En composición:

* Las partes **no pueden existir sin el todo**

## Composición uno a uno (1:1)

### Representación UML (unidireccional)

```text id="2p7kxm"
Human ◆--------> Heart
   1               1
```

### Implementación (unidireccional)

```java id="v1m8qt"
public class Heart {
    private int beatsPerMinute;

    public Heart(int bpm) {
        this.beatsPerMinute = bpm;
    }

    public int getBeatsPerMinute() {
        return beatsPerMinute;
    }
}
```

```java id="g7n2rs"
public class Human {
    private Heart heart;

    public Human() {
        this.heart = new Heart(72); // creación interna
    }

    public Heart getHeart() {
        return heart;
    }
}
```

### Test (unidireccional)

```java id="d4x9kq"
public class TestHuman {
    public static void main(String[] args) {
        Human human = new Human();

        System.out.println("Latidos: " + human.getHeart().getBeatsPerMinute());
    }
}
```

### Representación UML (bidireccional)

```text id="q9z1lu"
Human ◆<--------> Heart
   1               1
```

### Implementación (bidireccional)

```java id="m3k8zr"
public class Heart {
    private int beatsPerMinute;
    private Human human;

    public Heart(int bpm, Human human) {
        this.beatsPerMinute = bpm;
        this.human = human;
    }

    public int getBeatsPerMinute() {
        return beatsPerMinute;
    }

    public Human getHuman() {
        return human;
    }
}
```

```java id="t7p4xv"
public class Human {
    private Heart heart;

    public Human() {
        this.heart = new Heart(72, this); // creación interna con referencia
    }

    public Heart getHeart() {
        return heart;
    }
}
```

### Test (bidireccional)

```java id="k6n3zb"
public class TestHumanBidirectional {
    public static void main(String[] args) {
        Human human = new Human();

        System.out.println("Latidos: " + human.getHeart().getBeatsPerMinute());
        System.out.println("Dueño del corazón: " + human.getHeart().getHuman());
    }
}
```

## Composición uno a muchos (1:N)

### Representación UML (unidireccional)

```text id="z5x2vr"
Document ◆--------> Page
    1                0..*
```

### Implementación (unidireccional)

```java id="f2k7mn"
public class Page {
    private int number;

    public Page(int number) {
        this.number = number;
    }

    public int getNumber() {
        return number;
    }
}
```

```java id="h8r1qp"
import java.util.ArrayList;
import java.util.List;

public class Document {
    private List<Page> pages;

    public Document(int totalPages) {
        pages = new ArrayList<>();

        for (int i = 1; i <= totalPages; i++) {
            pages.add(new Page(i)); // creación interna
        }
    }

    public List<Page> getPages() {
        return pages;
    }
}
```

### Test (unidireccional)

```java id="c4w9yt"
public class TestDocument {
    public static void main(String[] args) {
        Document doc = new Document(3);

        for (Page p : doc.getPages()) {
            System.out.println("Página: " + p.getNumber());
        }
    }
}
```

### Representación UML (bidireccional)

```text id="u2m7nk"
Document ◆<--------> Page
    1                0..*
```

### Implementación (bidireccional)

```java id="r6p3dz"
public class Page {
    private int number;
    private Document document;

    public Page(int number, Document document) {
        this.number = number;
        this.document = document;
    }

    public int getNumber() {
        return number;
    }

    public Document getDocument() {
        return document;
    }
}
```

```java id="x9v4jq"
import java.util.ArrayList;
import java.util.List;

public class Document {
    private List<Page> pages;

    public Document(int totalPages) {
        pages = new ArrayList<>();

        for (int i = 1; i <= totalPages; i++) {
            pages.add(new Page(i, this));
        }
    }

    public List<Page> getPages() {
        return pages;
    }
}
```

### Test (bidireccional)

```java id="n1k8qw"
public class TestDocumentBidirectional {
    public static void main(String[] args) {
        Document doc = new Document(2);

        for (Page p : doc.getPages()) {
            System.out.println("Página: " + p.getNumber());
            System.out.println("Documento asociado: " + p.getDocument());
        }
    }
}
```

## Restricción importante

En composición:

* Un objeto **no puede pertenecer a múltiples “todos”**
* Por esta razón, una relación N:N **no es válida**

## Conclusión

La composición se utiliza cuando:

* Existe una relación todo-parte fuerte
* El todo controla completamente a sus partes
* Las partes no deben existir independientemente

Representa el nivel más alto de acoplamiento en relaciones entre clases.
