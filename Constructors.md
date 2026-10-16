# Constructores y destructores en Programación Orientada a Objetos

## Introducción

En Programación Orientada a Objetos, una clase define la estructura y el comportamiento de los objetos que pueden crearse a partir de ella. Como se estudió anteriormente, los atributos representan el **estado** de un objeto y los métodos permiten consultar o modificar ese estado de manera controlada.

Sin embargo, antes de utilizar un objeto debemos considerar una pregunta importante:

> **¿Cuál debe ser el estado inicial de un objeto cuando es creado?**

Por ejemplo, consideremos una clase `Person`. Para que un objeto represente correctamente a una persona, podría ser necesario conocer desde el momento de su creación cierta información básica, como su nombre y apellido.

Los **constructores** permiten controlar este proceso de inicialización.

En este documento estudiaremos cómo se construyen e inicializan objetos, cómo pueden existir diferentes formas de construcción y cómo podemos reutilizar la lógica entre constructores. Finalmente, estudiaremos de manera conceptual qué ocurre cuando un objeto llega al final de su ciclo de vida.

---

# Código base

Para desarrollar los conceptos relacionados con constructores utilizaremos los archivos `Person.java` y `Test.java`. A partir de este código inicial realizaremos modificaciones progresivas durante el desarrollo del tema.

## Archivo: `Person.java`

La clase `Person` representa una persona mediante dos nombres y dos apellidos. Sus atributos se encuentran encapsulados y se utilizan métodos accesores y mutadores para consultar y modificar sus valores. Para simplificar el ejemplo, cada componente del nombre debe contener una sola palabra formada únicamente por letras.

```java id="s8op81"
public class Person {

    private String firstName = "";
    private String secondName = "";
    private String firstFamilyName = "";
    private String secondFamilyName = "";

    public String getFirstName() {
        return firstName;
    }

    public boolean setFirstName(String newFirstName) {
        if (isValid(newFirstName)) {
            firstName = newFirstName;
            return true;
        }
        return false;
    }

    public String getSecondName() {
        return secondName;
    }

    public boolean setSecondName(String newSecondName) {
        if (isValid(newSecondName)) {
            secondName = newSecondName;
            return true;
        }
        return false;
    }

    public String getFirstFamilyName() {
        return firstFamilyName;
    }

    public boolean setFirstFamilyName(String newFirstFamilyName) {
        if (isValid(newFirstFamilyName)) {
            firstFamilyName = newFirstFamilyName;
            return true;
        }
        return false;
    }

    public String getSecondFamilyName() {
        return secondFamilyName;
    }

    public boolean setSecondFamilyName(String newSecondFamilyName) {
        if (isValid(newSecondFamilyName)) {
            secondFamilyName = newSecondFamilyName;
            return true;
        }
        return false;
    }

    private boolean isValid(String value) {
        return value != null
                && value.matches("^[A-Za-zÁÉÍÓÚÜÑáéíóúüñ]+$");
    }
}
```

## Archivo: `Test.java`

La clase `Person` será utilizada desde `Test.java`. Inicialmente crearemos un objeto sin proporcionar datos y posteriormente estableceremos sus atributos mediante los métodos mutadores. Este será el comportamiento que analizaremos y modificaremos al introducir los constructores.

```java id="2eabjf"
void main() {

    Person person = null;
    
    person = new Person();

    person.setFirstName("Juan");
    person.setSecondName("Carlos");
    person.setFirstFamilyName("García");
    person.setSecondFamilyName("Muñoz");

    System.out.println(person.getFirstName());
    System.out.println(person.getSecondName());
    System.out.println(person.getFirstFamilyName());
    System.out.println(person.getSecondFamilyName());
}
```

## ¿Qué ocurre al crear un objeto?

Analicemos la siguiente instrucción del programa anterior:

```java
Person person = new Person();
```

Aunque está escrita en una sola línea, combina la **declaración de una variable**, la **creación de un objeto** y la **asignación de una referencia**.

| Elemento | Significado |
| --- | --- |
| `Person` | Es el tipo de la variable: indica que puede almacenar una referencia a un objeto de tipo `Person`. |
| `person` | Es el nombre de la variable que utilizaremos para acceder al objeto. |
| `=` | Asigna a la variable la referencia obtenida al evaluar la expresión de la derecha. |
| `new Person()` | Crea una nueva instancia de `Person` e invoca su constructor sin argumentos. |
| `;` | Marca el final de la instrucción. |

### La variable y el objeto son diferentes

La variable `person` no contiene directamente el objeto: almacena una **referencia** que permite acceder a él. Por su parte, `Person` es la clase que define los atributos y métodos de ese objeto.

Podemos separar la instrucción en dos pasos:

```java
Person person;          // Declara una variable de referencia.
person = new Person();  // Crea el objeto y asigna su referencia.
```

La primera línea por sí sola **no crea ningún objeto**. Además, como `person` es una variable local, debemos asignarle un valor antes de utilizarla.

Después de la segunda línea podemos acceder a los métodos del objeto mediante la referencia:

```java
person.setFirstName("Juan");
System.out.println(person.getFirstName());
```

### ¿Qué representa `Person()`?

Dentro de la expresión `new Person()`, `Person()` indica la invocación del constructor. Los paréntesis vacíos significan que no estamos pasando argumentos para inicializar el objeto.

En el código base no hemos escrito ningún constructor. En este caso, **Java proporciona automáticamente un constructor por defecto sin parámetros**, lo que permite utilizar `new Person()`.

> Java proporciona este constructor por defecto únicamente cuando la clase no declara ningún constructor.

Al terminar la creación del objeto, sus cuatro atributos contienen `""`, porque ese es el valor que asignamos explícitamente en sus declaraciones:

```java
private String firstName = "";
private String secondName = "";
private String firstFamilyName = "";
private String secondFamilyName = "";
```

Por tanto, `new Person()` crea una persona cuyos nombres y apellidos todavía están vacíos. Los valores `"Juan"`, `"Carlos"`, `"García"` y `"Muñoz"` se asignan después mediante los setters.

### Una referencia nula y un objeto sin referencia guardada

Ahora analicemos estas dos instrucciones:

```java
Person person = null;
new Person();
```

En la primera línea declaramos la variable `person` y le asignamos `null`. Esto significa que **la variable no hace referencia a ningún objeto**. No se crea una instancia ni se invoca un constructor.

Asignar `null` es diferente de dejar una variable local sin inicializar: aquí la variable ya tiene un valor, pero ese valor no permite acceder a un objeto. Por ejemplo, intentar ejecutar `person.getFirstName()` en este punto provoca una `NullPointerException`.

La segunda línea, `new Person();`, **sí crea un objeto e invoca su constructor**, pero no guarda la referencia obtenida en ninguna variable. No existe una asignación que conecte ese objeto con `person`, por lo que **`person` continúa siendo `null`**.

En este ejemplo, el objeto recién creado queda sin una referencia que permita utilizarlo posteriormente y puede ser recuperado por el recolector de basura. Esto no significa que su memoria se libere inmediatamente.

> Crear un objeto y asignar su referencia a una variable son operaciones diferentes. Escribirlas una después de otra no las vincula automáticamente.

Para que `person` haga referencia al nuevo objeto, necesitamos la asignación:

```java
Person person = null;
person = new Person();

person.setFirstName("Juan");
System.out.println(person.getFirstName()); // Juan
```

Si vamos a crear el objeto desde el principio, podemos declarar e inicializar la variable en una sola instrucción, como en el código base:

```java
Person person = new Person();
```

Esto nos lleva al siguiente paso: **definir un constructor que permita proporcionar los datos necesarios desde el momento en que se crea el objeto**.
