## Introducción

La Programación Orientada a Objetos (POO) es un paradigma que modela el software a partir de **objetos**, los cuales representan entidades del mundo real o abstracto. Cada objeto posee:

* **Estado:** representado por sus atributos.
* **Comportamiento:** definido por sus métodos.
* **Identidad:** cada objeto es único en la memoria.

## Conceptos Clave

### Clase

Una **clase** es una plantilla o molde que define las características (atributos) y comportamientos (métodos) comunes a un conjunto de objetos.

### Objeto

Un **objeto** es una instancia de una clase. Tiene valores específicos para sus atributos y puede ejecutar métodos.

## Atributos y Métodos

| Elemento                  | Descripción                                                                    |
| ------------------------- | ------------------------------------------------------------------------------ |
| **Atributo de instancia** | Variable que pertenece a cada objeto creado.                                   |
| **Atributo de clase**     | Variable compartida entre todos los objetos de la clase (`static`).            |
| **Método de instancia**   | Opera sobre atributos del objeto y requiere una instancia.                     |
| **Método de clase**       | Pertenece a la clase, se declara `static`, no accede a atributos individuales. |

## Ejemplo 

**Archivo: `Car.java`**

```java
public class Car {
    String brand;
    int speed;

    void accelerate() {
        speed += 10;
    }

    void brake() {
        speed -= 10;
    }
}
```

**Archivo: `TestCar.java`**

```java
// Programa principal
public class TestCar {

    public static void main(String[] args) {
        Car car1 = new Car();
        car1.brand = "Toyota";
        car1.speed = 0;

        car1.accelerate();
        System.out.println(car1.brand + " aceleró a " + car1.speed + " km/h");

        car1.brake();
        System.out.println(car1.brand + " frenó a " + car1.speed + " km/h");
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

### Ejemplo 1: Clase `Car` con Encapsulamiento

**Archivo: `Car.java`**

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

**Archivo: `TestCar.java`**

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

## Ejemplo 2: Encapsulamiento con validación (Email)

Supongamos que queremos almacenar el correo electrónico de un usuario.

### Versión 1: Setter simple

Esta es la implementación más básica y la menos recomendable, ya que el setter permite modificar el atributo sin aplicar ninguna restricción.

**Archivo: `User.java`**

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

**Archivo: `TestUser.java`**

```java
public class TestUser {

    public static void main(String[] args) {
        User user = new User();

        user.setEmail("jane.doe@mail.com");
        System.out.println(user.getEmail());

        user.setEmail("invalid-email");
        System.out.println(user.getEmail());
    }
}
```

Salida:

```text
jane.doe@mail.com
invalid-email
```

El objeto acepta `"invalid-email"` porque el mutador realiza una asignación directa sin comprobar el valor recibido.

> Un setter simple proporciona acceso indirecto al atributo, pero no necesariamente protege la integridad de la información. Por esta razón, siempre que existan restricciones sobre los valores permitidos, es recomendable incorporarlas en el mutador.

### Versión 2: Setter con validación y retorno `boolean`

Podemos mejorar el mutador haciendo que valide el valor antes de modificar el atributo.

**Archivo: `User.java`**

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
        return email != null
                && email.matches("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$");
    }
}
```

**Archivo: `TestUser.java`**

```java
public class TestUser {

    public static void main(String[] args) {
        User user = new User();

        if (user.setEmail("jane.doe@mail.com")) {
            System.out.println("Email actualizado: " + user.getEmail());
        } else {
            System.out.println("No fue posible actualizar el email.");
        }

        if (user.setEmail("invalid-email")) {
            System.out.println("Email actualizado: " + user.getEmail());
        } else {
            System.out.println("No fue posible actualizar el email.");
        }
    }
}
```

Salida:

```text
Email actualizado: jane.doe@mail.com
No fue posible actualizar el email.
```

Observa un aspecto fundamental: después de intentar asignar `"invalid-email"`, el atributo conserva `"jane.doe@mail.com"`.

El objeto **rechaza la modificación y conserva un estado válido**.

### Versión 3: Setter con múltiples estados

En algunas situaciones, `true` y `false` no son suficientes para describir el resultado de una operación. Un mutador podría retornar un entero para representar diferentes estados:

* `0`: operación correcta.
* Valores positivos: operación correcta, pero con advertencias.
* Valores negativos: error; la modificación fue rechazada.

Por ejemplo, podemos aceptar un correo escrito con mayúsculas o espacios adicionales, pero normalizarlo antes de almacenarlo.

**Archivo: `User.java`**

```java
public class User {
    private String email;

    public int setEmail(String email) {
        if (email == null || email.isBlank()) {
            return -1;
        }

        String normalizedEmail = email.trim().toLowerCase();

        if (!isValidEmail(normalizedEmail)) {
            return -2;
        }

        email = email.trim();

        if (!email.equals(normalizedEmail)) {
            this.email = normalizedEmail;
            return 1;
        }

        this.email = email;
        return 0;
    }

    public String getEmail() {
        return email;
    }

    private boolean isValidEmail(String email) {
        return email.matches(
                "^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$"
        );
    }
}
```

**Archivo: `TestUser.java`**

```java
public class TestUser {

    public static void main(String[] args) {
        User user = new User();

        int result = user.setEmail("jane.doe@mail.com");

        if (result == 0) {
            System.out.println("Email actualizado: " + user.getEmail());
        } else if (result > 0) {
            System.out.println("Email actualizado con advertencias: " + user.getEmail());
        } else {
            System.out.println("Error al actualizar el email.");
        }

        result = user.setEmail("JANE.DOE@MAIL.COM");

        if (result == 0) {
            System.out.println("Email actualizado: " + user.getEmail());
        } else if (result > 0) {
            System.out.println("Email actualizado con advertencias: " + user.getEmail());
        } else {
            System.out.println("Error al actualizar el email.");
        }

        result = user.setEmail("invalid-email");

        if (result == 0) {
            System.out.println("Email actualizado: " + user.getEmail());
        } else if (result > 0) {
            System.out.println("Email actualizado con advertencias: " + user.getEmail());
        } else {
            System.out.println("Error al actualizar el email.");
        }
    }
}
```

Salida:

```text
Email actualizado: jane.doe@mail.com
Email actualizado con advertencias: jane.doe@mail.com
Error al actualizar el email.
```

En este caso:

* `0` indica que el dato fue aceptado sin modificaciones.
* `1` indica que fue aceptado, pero se realizó una normalización.
* `-2` indica que fue rechazado.

> **Nota:** Los códigos numéricos son válidos, pero obligan a conocer el significado de cada número. En diseños más expresivos pueden reemplazarse por una enumeración.

Por ejemplo:

**Archivo: `Result.java`**

```java
public enum Result {
    OK,
    WARNING,
    ERROR
}
```

Esto permite retornar `Result.OK`, `Result.WARNING` o `Result.ERROR` en lugar de códigos numéricos.

### Versión 4: Setter fluido

Un setter también puede retornar el propio objeto. Esto permite encadenar varias operaciones.

Para que el ejemplo muestre realmente el encadenamiento, necesitamos otro atributo.

**Archivo: `User.java`**

```java
public class User {
    private String name;
    private String email;

    public User setName(String name) {
        this.name = name;
        return this;
    }

    public User setEmail(String email) {
        if (email == null || !email.matches("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$")) {
            throw new IllegalArgumentException("Invalid email");
        }

        this.email = email;
        return this;
    }

    public String getName() {
        return name;
    }

    public String getEmail() {
        return email;
    }
}
```

**Archivo: `TestUser.java`**

```java
public class TestUser {

    public static void main(String[] args) {
        User user = new User();

        try {
            user.setName("Jane Doe")
                .setEmail("jane.doe@mail.com");

            System.out.println(user.getName());
            System.out.println(user.getEmail());

        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }

        try {
            user.setName("Jane Doe")
                .setEmail("invalid-email");

            System.out.println(user.getName());
            System.out.println(user.getEmail());

        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

Salida:

```text
Jane Doe
jane.doe@mail.com
Error: Invalid email
```

En un setter fluido, retornar `this` permite utilizar el objeto inmediatamente para realizar otra operación.

### Nota sobre el uso de excepciones

Las excepciones **no constituyen otro tipo de setter**. Son un mecanismo para comunicar que una modificación no pudo realizarse y pueden utilizarse con diferentes tipos de mutadores.

Por ejemplo:

```java
if (!isValidEmail(email)) {
    throw new IllegalArgumentException("Invalid email");
}
```

Son especialmente útiles en setters fluidos. Consideremos:

```java
user.setName("Jane Doe")
    .setEmail("invalid-email")
    .setAddress("Manizales");
```

Si `setEmail()` simplemente ignorara el valor inválido y retornara `this`, el encadenamiento continuaría y el error podría pasar inadvertido. Al lanzar una excepción, la ejecución del encadenamiento se interrumpe inmediatamente.

### Idea fundamental

El setter simple:

```java
public void setEmail(String email) {
    this.email = email;
}
```

debe entenderse como la alternativa **más básica y generalmente menos adecuada cuando existen reglas sobre el atributo**.

El objetivo del encapsulamiento no es reemplazar:

```java
user.email = value;
```

por:

```java
user.setEmail(value);
```

El verdadero objetivo es establecer una frontera de control que permita **proteger la integridad del estado del objeto**.

Por eso, generar automáticamente getters y setters desde un IDE puede ahorrar escritura de código, pero **no resuelve por sí mismo el problema del encapsulamiento**. El programador debe determinar qué atributos deben exponerse, cuáles pueden modificarse y qué restricciones deben cumplirse antes de aceptar una modificación.

## Conclusión

* Un setter simple (`void`) es el **menos adecuado**.
* Un buen encapsulamiento implica **validar, controlar y proteger el estado**.
* No todos los setters son iguales: su diseño depende del nivel de control requerido.

> Un objeto bien encapsulado no almacena datos inválidos, aunque el mundo exterior intente proporcionarlos.
