## Introducción

La Programación Orientada a Objetos (POO) es un paradigma que modela el software a partir de **objetos**, los cuales representan entidades del mundo real o abstracto. Cada objeto posee:

* **Estado:** representado por sus atributos.
* **Comportamiento:** definido por sus métodos.
* **Identidad:** cada objeto es único en la memoria.

---

## Conceptos Clave

### Clase

Una **clase** es una plantilla o molde que define las características (atributos) y comportamientos (métodos) comunes a un conjunto de objetos.

### Objeto

Un **objeto** es una instancia de una clase. Tiene valores específicos para sus atributos y puede ejecutar métodos.

---

## Atributos y Métodos

| Elemento                  | Descripción                                                                    |
| ------------------------- | ------------------------------------------------------------------------------ |
| **Atributo de instancia** | Variable que pertenece a cada objeto creado.                                   |
| **Atributo de clase**     | Variable compartida entre todos los objetos de la clase (`static`).            |
| **Método de instancia**   | Opera sobre atributos del objeto y requiere una instancia.                     |
| **Método de clase**       | Pertenece a la clase, se declara `static`, no accede a atributos individuales. |

## Ejemplo 
```java
public class Car {
    String brand;
    int speed;

    void accelerate() {
        speed += 10;
        System.out.println(brand + " aceleró a " + speed + " km/h");
    }

    void brake() {
        speed -= 10;
        System.out.println(brand + " frenó a " + speed + " km/h");
    }
}
```

```java
// Programa principal
public class TestCar {

    public static void main(String[] args) {
        Car car1 = new Car();
        car1.brand = "Toyota";
        car1.speed = 0;

        car1.accelerate(); // Toyota aceleró a 10 km/h
        car1.brake();      // Toyota frenó a 0 km/h
    }
}
```



