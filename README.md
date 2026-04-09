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

## Encapsulamiento

El **encapsulamiento** es un principio que consiste en proteger el acceso directo a los atributos de un objeto, exponiendo solo aquellos métodos necesarios para interactuar con ellos. Esto permite:

* Evitar modificaciones incorrectas.
* Controlar el acceso con condiciones.
* Ocultar detalles internos de implementación.

Sin embargo, es importante precisar:

> Encapsular no es simplemente hacer atributos `private` y generar getters y setters automáticamente.

El encapsulamiento **real** implica:

* Definir **reglas** sobre cómo puede cambiar el estado.
* Evitar que el objeto almacene **valores inválidos**.
* Controlar **cómo** y **cuándo** se modifica la información.

---

### Ejemplo 1: Clase `Car` con Encapsulamiento

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

---

## Limitación de los setters simples

Muchos entornos de desarrollo permiten generar automáticamente métodos `get` y `set`. Por ejemplo:

```java
public void setEmail(String email) {
    this.email = email;
}
```

Este enfoque es **insuficiente**, porque:

* No valida la información.
* Permite estados inválidos.
* Convierte el atributo en “público disfrazado”.

---

## 📖 Ejemplo 2: Encapsulamiento con validación (Email)

Supongamos que queremos almacenar el correo electrónico de un usuario.

### Versión incorrecta (setter simple)

```java
public class User {
    private String email;

    public void setEmail(String email) {
        this.email = email;
    }

    public String getEmail() {
        return email;
    }
}
```

Problema:

```java
user.setEmail("abc");
user.setEmail("@@@");
user.setEmail(null);
```

Todos estos valores serían aceptados, aunque son inválidos.

---

### Versión con validación (`boolean`)

```java
public class User {
    private String email;

    public boolean setEmail(String email) {
        if (isValidEmail(email)) {
            this.email = email;
            return true;
        }
        return false;
    }

    public String getEmail() {
        return email;
    }

    private boolean isValidEmail(String email) {
        return email != null && email.matches("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$");
    }
}
```

Aquí:

* Se valida el formato.
* Se evita almacenar información incorrecta.
* El método indica si la operación fue exitosa.

---

### Versión con resultado tipado (`enum`)

```java
public enum Result {
    OK,
    WARNING,
    ERROR
}
```

```java
public class User {
    private String email;

    public Result setEmail(String email) {
        if (email == null || email.isBlank()) {
            return Result.ERROR;
        }

        String normalizedEmail = email.trim().toLowerCase();

        if (!isValidEmail(normalizedEmail)) {
            return Result.ERROR;
        }

        this.email = normalizedEmail;

        if (!email.equals(normalizedEmail)) {
            return Result.WARNING;
        }

        return Result.OK;
    }

    public String getEmail() {
        return email;
    }

    private boolean isValidEmail(String email) {
        return email.matches("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$");
    }
}
```

Interpretación:

* `OK` → email válido sin cambios
* `WARNING` → email válido pero ajustado (normalización)
* `ERROR` → email inválido

---

### Versión fluida (method chaining)

```java
public class User {
    private String email;

    public User setEmail(String email) {
        if (email == null || !email.matches("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$")) {
            throw new IllegalArgumentException("Invalid email");
        }
        this.email = email;
        return this;
    }

    public String getEmail() {
        return email;
    }
}
```

Uso:

```java
user.setEmail("user@mail.com");
```

O encadenado:

```java
user.setEmail("user@mail.com");
```

> En setters fluidos, es recomendable usar excepciones para evitar errores silenciosos.

---

## Conclusión

* Un setter simple (`void`) es el **menos adecuado**.
* Un buen encapsulamiento implica **validar, controlar y proteger el estado**.
* No todos los setters son iguales: su diseño depende del nivel de control requerido.

> Un objeto bien encapsulado no almacena datos inválidos, aunque el mundo exterior intente proporcionarlos.


