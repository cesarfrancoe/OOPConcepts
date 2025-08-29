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

---

## Encapsulamiento

El **encapsulamiento** es un principio que consiste en proteger el acceso directo a los atributos de un objeto, exponiendo solo aquellos métodos necesarios para interactuar con ellos. Esto permite:

* Evitar modificaciones incorrectas.
* Controlar el acceso con condiciones.
* Ocultar detalles internos de implementación.

### 📖 Ejemplo: Clase `Car` con Encapsulamiento

```java
public class Car {
    private String brand = "";
    private int speed = 0;

    void accelerate(){
        speed += 10;
    }

    void brake(){
        if (speed >= 10){
            speed -= 10;
        }
    }

    public int getSpeed(){
        return speed;
    }

    public String getBrand(){
        return brand;
    }

    public void setBrand(String newBrand){
        if (newBrand.equals("Toyota") || newBrand.equals("Ford") || newBrand.equals("Ferrari")){
            brand = newBrand;
        } else {
            brand = "";
        }
    }
}
```

```java
public class TestCar {
    public static void main(String[] args) {
        Car car1 = new Car();

        car1.setBrand("Xyz");
        car1.accelerate();
        car1.accelerate();
        System.out.println(car1.getBrand());
        System.out.println(car1.getSpeed());
        car1.brake();
        System.out.println(car1.getSpeed());
    }
}
```

> **Nota:** Gracias al encapsulamiento, evitamos asignar marcas no permitidas o valores de velocidad arbitrarios como `car1.speed = 200;`.
