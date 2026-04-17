# Herencia entre Clases en POO

Este documento presenta el concepto de **herencia** en Programación Orientada a Objetos, su propósito, características y ejemplos de implementación en Java.

---

## Introducción

En la Programación Orientada a Objetos, las clases pueden relacionarse de diferentes maneras. En los documentos anteriores se estudiaron relaciones estructurales como:

* Asociación
* Agregación
* Composición

Estas relaciones describen cómo los objetos se conectan entre sí.

Sin embargo, existe otro tipo de relación fundamental que no describe estructura sino **especialización**: la **herencia**.

La herencia permite modelar relaciones del tipo **“es un” (is-a)**, en las cuales una clase representa una versión más específica de otra.

---

## Herencia

La **herencia** es un mecanismo mediante el cual una clase puede **extender otra clase**, heredando sus atributos y métodos.

* La clase que hereda se denomina **subclase**
* La clase de la cual se hereda se denomina **superclase**

La subclase puede:

* reutilizar atributos y métodos
* agregar nuevos atributos y métodos
* redefinir comportamientos heredados

---

## Características

* Representa una relación **“es un”**
* Permite **reutilización de código**
* Define **jerarquías de clases**
* Opera a nivel de **clases, no de objetos**
* No transmite valores, sino **definiciones**

---

## Aclaración importante

La herencia no debe interpretarse como una copia de valores entre objetos.

> Una subclase hereda **atributos**, no **valores**.

Analogía conceptual:

* Incorrecto: “el hijo hereda el color de ojos del padre”
* Correcto: “el hijo hereda la característica ‘ojos’”

Esto implica que cada objeto tendrá sus propios valores.

---

## Ejemplo 1: Herencia simple

### Clase base

```java
public class Person {

    protected String name;

    public Person(String name) {
        this.name = name;
    }

    public void greet() {
        System.out.println("Hello, my name is " + name);
    }

}
```

### Clase derivada

```java
public class Student extends Person {

    private String studentId;

    public Student(String name, String studentId) {
        super(name);
        this.studentId = studentId;
    }

    public void study() {
        System.out.println(name + " is studying.");
    }

}
```

### Clase de prueba

```java
public class TestInheritance {

    public static void main(String[] args) {

        Student student = new Student("Alice", "S001");

        student.greet();
        student.study();

    }

}
```

---

## Justificación

* `Student` es un tipo de `Person`
* Se reutiliza el método `greet()`
* Se añade comportamiento específico (`study()`)

Esto representa correctamente una relación de especialización.

---

## Ejemplo 2: Jerarquía de clases

### Clase base

```java
public class Vehicle {

    protected int speed;

    public void accelerate() {
        speed += 10;
    }

}
```

### Subclases

```java
public class Car extends Vehicle {

    private String plate;

    public Car(String plate) {
        this.plate = plate;
    }

}
```

```java
public class Motorcycle extends Vehicle {

    private int engineCapacity;

    public Motorcycle(int engineCapacity) {
        this.engineCapacity = engineCapacity;
    }

}
```

---

## Justificación

* `Vehicle` define comportamiento común
* `Car` y `Motorcycle` reutilizan ese comportamiento
* Cada subclase agrega sus propias características

---

## Representación conceptual

```text
        Vehicle
        /    \
      Car  Motorcycle
```

La flecha implícita indica que ambas clases derivan de `Vehicle`.

---

## Diferencia con otras relaciones

| Tipo de relación | Descripción                 | Ejemplo          |
| ---------------- | --------------------------- | ---------------- |
| Asociación       | Relación de uso             | Student – Course |
| Agregación       | Relación todo-parte débil   | Library – Book   |
| Composición      | Relación todo-parte fuerte  | House – Room     |
| Herencia         | Relación de especialización | Student – Person |

---

## Cuándo usar herencia

Se debe usar herencia cuando:

* Existe una relación clara de tipo **“es un”**
* Se comparten comportamientos comunes
* Se desea evitar duplicación de código

Ejemplos válidos:

* `Dog` → `Animal`
* `Student` → `Person`

Ejemplos inválidos:

* `Engine` → `Car` (no es un tipo de carro)

En estos casos se debe usar composición.

---

## Conclusión

La herencia es un mecanismo fundamental en la Programación Orientada a Objetos que permite construir jerarquías de clases mediante relaciones de especialización.

Su uso adecuado facilita:

* reutilización de código
* organización del sistema
* mantenimiento
