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

    Person person = new Person();

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
