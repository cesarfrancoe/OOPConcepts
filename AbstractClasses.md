# Clases abstractas

Una **clase abstracta** es una clase que representa un concepto general dentro de una jerarquía de clases, pero que **no está diseñada para crear objetos directamente**.

Su propósito es definir características y comportamientos comunes que serán heredados y especializados por clases más concretas.

Por ejemplo, en un sistema empresarial podemos representar diferentes tipos de empleados:

```text
               Employee
              /        \
       Teacher          Manager
```

`Employee` representa el concepto general de empleado, mientras que `Teacher` y `Manager` representan tipos concretos de empleados.

## 1. Clases abstractas en Java

En Java, una clase se declara abstracta mediante la palabra reservada `abstract`:

```java
public abstract class Employee {
    private String id;
    private String name;

    public Employee(String id, String name) {
        this.id = id;
        this.name = name;
    }

    public String getId() {
        return id;
    }

    public String getName() {
        return name;
    }
}
```

Una característica fundamental de una clase abstracta es que **no puede instanciarse directamente**:

```java
Employee employee = new Employee("123", "Ana"); // Error
```

Sin embargo, puede utilizarse como tipo de referencia:

```java
Employee employee = new Teacher("123", "Ana");
```

Esto permite tratar objetos de diferentes clases derivadas mediante un tipo común, aprovechando el **polimorfismo**.

## 2. ¿Por qué una clase puede ser abstracta?

Una clase puede declararse abstracta simplemente porque representa un concepto demasiado general para que existan objetos directamente de ese tipo.

Por ejemplo, supongamos que en nuestro modelo todo empleado necesariamente debe pertenecer a una categoría concreta:

```text
               Employee
              /        \
       Teacher          Manager
```

Puede tener sentido definir en `Employee` todos los atributos y comportamientos comunes:

```java
public abstract class Employee {
    private String id;
    private String name;

    public Employee(String id, String name) {
        this.id = id;
        this.name = name;
    }

    public String getInformation() {
        return id + " - " + name;
    }
}
```

Esta clase **no contiene ningún método abstracto** y, aun así, es una clase abstracta.

Declararla abstracta establece una restricción importante en el modelo: no pueden existir objetos que sean simplemente `Employee`; deben ser objetos de alguna clase concreta derivada.

Por tanto, una clase abstracta **no está obligada a contener métodos abstractos**.

## 3. Métodos abstractos

Además de impedir la creación directa de objetos, una clase abstracta puede establecer comportamientos que deben existir en sus clases derivadas, pero cuya implementación depende de cada una.

Para ello se utilizan los **métodos abstractos**.

Por ejemplo, todo empleado puede tener un salario, pero su forma de cálculo puede depender del tipo de empleado:

```java
public abstract class Employee {
    private String id;
    private String name;

    public Employee(String id, String name) {
        this.id = id;
        this.name = name;
    }

    public abstract double calculateSalary();
}
```

El método:

```java
public abstract double calculateSalary();
```

declara una operación, pero **no proporciona su implementación**.

Una clase concreta derivada debe proporcionar dicha implementación:

```java
public class Teacher extends Employee {
    private double baseSalary;

    public Teacher(String id, String name, double baseSalary) {
        super(id, name);
        this.baseSalary = baseSalary;
    }

    @Override
    public double calculateSalary() {
        return baseSalary;
    }
}
```

Otra clase puede implementar el mismo comportamiento de manera diferente:

```java
public class Manager extends Employee {
    private double baseSalary;
    private double bonus;

    public Manager(
            String id,
            String name,
            double baseSalary,
            double bonus) {

        super(id, name);
        this.baseSalary = baseSalary;
        this.bonus = bonus;
    }

    @Override
    public double calculateSalary() {
        return baseSalary + bonus;
    }
}
```

De esta manera, `Employee` establece que todos los empleados deben permitir calcular su salario, pero deja a cada clase concreta la responsabilidad de determinar **cómo** hacerlo.

## 4. Clases abstractas y métodos abstractos

Es importante diferenciar ambos conceptos.

Una **clase abstracta** es una clase que no puede instanciarse directamente.

Un **método abstracto** es un método que se declara sin proporcionar una implementación.

Por tanto:

```text
Método abstracto → la clase debe ser abstracta

Clase abstracta  → no necesariamente tiene métodos abstractos
```

Si una clase contiene al menos un método abstracto, debe declararse abstracta. Sin embargo, una clase puede declararse abstracta aunque todos sus métodos tengan implementación.

Esto permite utilizar la abstracción con dos propósitos:

- **Abstracción del concepto:** impedir la creación de objetos de una clase demasiado general.
- **Abstracción del comportamiento:** establecer operaciones cuya implementación debe ser proporcionada por las clases derivadas.

## 5. Una clase abstracta puede contener elementos concretos

Una clase abstracta puede combinar:

- atributos;
- constructores;
- métodos concretos;
- métodos abstractos.

Por ejemplo:

```java
public abstract class Employee {
    private String id;
    private String name;

    public Employee(String id, String name) {
        this.id = id;
        this.name = name;
    }

    public String getInformation() {
        return id + " - " + name;
    }

    public abstract double calculateSalary();
}
```

En este caso, todos los empleados comparten la implementación de `getInformation()`, mientras que cada tipo de empleado proporciona su propia implementación de `calculateSalary()`.

## 6. Clases abstractas y herencia

Las clases abstractas son especialmente útiles en relaciones de **generalización y especialización**:

```text
Employee
    ↑
 Teacher
```

Podemos afirmar que:

> Un `Teacher` **es un** `Employee`.

La clase abstracta define aquello que es común a la jerarquía, mientras que las clases derivadas representan conceptos más específicos.

## 7. Idea fundamental

Una clase abstracta permite representar un concepto válido dentro del modelo que **no debe producir objetos directamente**.

Además, puede establecer comportamientos que todas las clases derivadas deben proporcionar mediante métodos abstractos.

Por tanto, no debemos confundir ambos conceptos:

**Una clase abstracta define un concepto no instanciable. Un método abstracto define un comportamiento cuya implementación queda pendiente para las clases derivadas.**
