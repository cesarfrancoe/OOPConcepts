# Interfaces: contratos y capacidades

[Documento principal](README.md) · Anterior: [Herencia](Inheritance.md) · Siguiente: [Composición](Composition.md)

## Propósito

Separar lo que un objeto puede hacer de su posición en una jerarquía. Una interfaz define un tipo y un contrato; una clase puede implementar varias interfaces aunque solo pueda extender una clase.

## De la herencia a los contratos de capacidad

Conservamos `Villager` (Aldeano) como base de la identidad común. `Farmer` (Agricultor), `Fisherman` (Pescador) y `Hunter` (Cazador) siguen siendo especializaciones, pero ahora declaran los contratos de las actividades que pueden realizar. Se mantiene el nombre `Fisherman` (Pescador) del capítulo anterior.

`Farmable` (Capaz de cultivar), `Fishable` (Capaz de pescar) y `Huntable` (Capaz de cazar) permiten que los clientes soliciten una capacidad sin exigir una clase de oficio concreta. Sus operaciones devuelven descripciones no nulas de las actividades; no simulan inventarios ni recursos.

Los siguientes archivos forman el ejemplo de esta etapa.

**Archivo: `Farmable.java`**

```java
public interface Farmable {
    // Returns a non-null description of the farming activity.
    public abstract String farm();
}
```

**Archivo: `Fishable.java`**

```java
public interface Fishable {
    // Returns a non-null description of the fishing activity.
    public abstract String fish();
}
```

**Archivo: `Huntable.java`**

```java
public interface Huntable {
    // Returns a non-null description of the hunting activity.
    public abstract String hunt();
}
```

**Archivo: `Villager.java`**

```java
public class Villager {
    private final String name;

    public Villager(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public String describe() {
        return "Aldeano: " + name;
    }
}
```

**Archivo: `Farmer.java`**

```java
public class Farmer extends Villager implements Farmable {
    public Farmer(String name) {
        super(name);
    }

    @Override
    public String farm() {
        return getName() + " cultiva";
    }

    @Override
    public String describe() {
        return super.describe() + " (agricultura)";
    }
}
```

**Archivo: `Fisherman.java`**

```java
public class Fisherman extends Villager implements Fishable {
    public Fisherman(String name) {
        super(name);
    }

    @Override
    public String fish() {
        return getName() + " pesca";
    }
}
```

**Archivo: `Hunter.java`**

```java
public class Hunter extends Villager implements Huntable {
    public Hunter(String name) {
        super(name);
    }

    @Override
    public String hunt() {
        return getName() + " caza";
    }
}
```

La herencia conserva el estado y comportamiento común del aldeano; las interfaces expresan sus capacidades. Implementar un contrato no obliga a abandonar la superclase. En particular, un cliente de `Fishable` (Capaz de pescar) puede recibir cualquier implementación válida, aunque no herede de `Fisherman` (Pescador).

## Un aldeano que cultiva y pesca

`FarmerFisher` (AgricultorPescador) extiende únicamente `Villager` (Aldeano) e implementa los dos contratos. Ya no necesitamos elegir un oficio como superclase para que los clientes reconozcan ambas capacidades.

**Archivo: `FarmerFisher.java`**

```java
public class FarmerFisher extends Villager implements Farmable, Fishable {
    public FarmerFisher(String name) {
        super(name);
    }

    @Override
    public String farm() {
        return getName() + " cultiva";
    }

    @Override
    public String fish() {
        return getName() + " pesca";
    }
}
```

**Archivo: `Test.java`**

```java
public class Test {
    private static void performFarming(Farmable worker) {
        System.out.println(worker.farm());
    }

    private static void performFishing(Fishable worker) {
        System.out.println(worker.fish());
    }

    public static void main(String[] args) {
        Farmer farmer = new Farmer("Luis");
        Fisherman fisherman = new Fisherman("Elena");
        Hunter hunter = new Hunter("Sara");
        FarmerFisher farmerFisher = new FarmerFisher("Ana");

        performFarming(farmer);
        performFishing(fisherman);
        System.out.println(hunter.hunt());
        System.out.println(farmerFisher.describe());
        performFarming(farmerFisher);
        performFishing(farmerFisher);
    }
}
```

Salida esperada:

```text
Luis cultiva
Elena pesca
Sara caza
Aldeano: Ana
Ana cultiva
Ana pesca
```

El mismo objeto `farmerFisher` (agricultor pescador) puede utilizarse como `Villager` (Aldeano), `Farmable` (Capaz de cultivar) o `Fishable` (Capaz de pescar). No es un subtipo de las clases de oficio: sus capacidades se reconocen por los contratos que implementa.

Las interfaces implementadas son una propiedad del tipo. Este ejemplo no permite agregar o retirar oficios de una instancia durante la ejecución.

### ¿Cuándo implementar todas las capacidades en la clase base?

Fragmento de la declaración de esta variante; se omiten los métodos requeridos por los contratos:

```java
public class Villager implements Farmable, Fishable, Huntable {
    // Implement farm(), fish(), and hunt().
}
```

Declarar `Villager` (Aldeano) con los tres contratos significaría que todos sus objetos y subtipos ofrecen cultivo, pesca y caza. Es una variante válida si el dominio exige esa garantía para todos los aldeanos. No representa una etapa más avanzada ni el requisito actual, donde las combinaciones de oficios son diferentes.

## Qué cambia y qué sigue pendiente

| Aspecto | Resultado |
| --- | --- |
| Múltiples capacidades | Una clase puede cumplir varios contratos |
| Dependencias del cliente | Puede pedir únicamente la capacidad necesaria |
| Reutilización del algoritmo | Sigue pendiente: cada clase debe aportar su implementación |
| Variación entre instancias | Requiere otra decisión de diseño si las capacidades cambian por objeto |

En este ejemplo, `farm()` (cultivar) está duplicado entre `Farmer` (Agricultor) y `FarmerFisher` (AgricultorPescador), y `fish()` (pescar), entre `Fisherman` (Pescador) y la clase combinada. Las interfaces resuelven los contratos, pero no esa duplicación. La siguiente etapa separa esas implementaciones en colaboradores reutilizables.

## Nombres de interfaces: capacidades y roles

Cuando una interfaz representa una capacidad, su nombre debe ayudar a responder: **¿qué puede hacer este objeto?** En inglés son habituales los adjetivos terminados en `-able` o `-ible`:

| Nombre | Capacidad que expresa |
| --- | --- |
| `Runnable` (Ejecutable) | Puede ejecutarse. |
| `Comparable` (Comparable) | Puede compararse con otro objeto para establecer un orden. |
| `Serializable` (Serializable) | Puede representarse mediante serialización. |

No todas las interfaces representan capacidades de esta forma. Cuando expresan un **rol**, suele resultar más natural un sustantivo que responda: **¿qué papel cumple este objeto?**

| Nombre | Rol que expresa |
| --- | --- |
| `Comparator` (Comparador) | Compara dos objetos según un criterio. |
| `Iterator` (Iterador) | Permite recorrer una secuencia de elementos. |
| `Repository` (Repositorio) | Ofrece acceso a objetos del dominio. |

La diferencia entre `Comparable` (Comparable) y `Comparator` (Comparador) resulta ilustrativa: el primero describe un objeto que puede compararse con otro; el segundo describe al colaborador encargado de compararlos. La terminación es una convención de nombres, no una regla del lenguaje ni una garantía de buen diseño.

También hay que revisar el sentido del adjetivo: «puede realizar una acción» y «puede recibir esa acción» no significan lo mismo. En este ejemplo, `Farmable` (Capaz de cultivar), `Fishable` (Capaz de pescar) y `Huntable` (Capaz de cazar) nombran las capacidades del aldeano por convención del modelo. Sin ese contexto, los términos ingleses pueden sugerir algo cultivable, pescable o cazable. El sufijo por sí solo no elimina la ambigüedad; el nombre y el contrato deben comunicar quién realiza la actividad.

## Contratos pequeños y explícitos

Un contrato incluye significado, entradas válidas, resultados y errores, además de la firma. El compilador verifica parte de su estructura; no garantiza que una implementación respete todas sus promesas semánticas.

No hace falta introducir una interfaz padre `Skill` si ningún cliente necesita una operación común. Una interfaz vacía puede tener usos específicos, pero no proporciona por sí sola una operación para ejecutar cualquier oficio.

Java también permite métodos `default` con implementación. Pueden servir para un comportamiento común coherente con el contrato, pero no reemplazan una decisión sobre quién posee el estado o cómo se comparten algoritmos. Si dos interfaces aportan implementaciones `default` incompatibles de la misma operación, la clase debe resolver el conflicto.

## Comprobación conceptual

- ¿Puede el cliente de `Farmable` utilizar un objeto que no sea un aldeano?
- ¿Qué promete `farm()` más allá de devolver un `String`?
- ¿Por qué implementar dos interfaces no permite cambiar los oficios de una instancia en ejecución?

Continuar con [composición](Composition.md) para separar las capacidades de sus implementaciones reutilizables.
