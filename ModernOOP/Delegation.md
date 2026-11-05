# Delegación: distribuir la ejecución de responsabilidades

[Documento principal](README.md) · Anterior: [Composición](Composition.md) · Siguiente: [Inmutabilidad](Immutability.md)

## Propósito

Distinguir el objeto que recibe una solicitud del colaborador que realiza parte del trabajo. La delegación permite reutilizar una implementación y conservar una API adecuada para el cliente.

## Una API explícita para dos capacidades

En esta variante, cada `Villager` puede cultivar y pescar. El aldeano recibe los colaboradores por constructor, delega las actividades y añade su nombre al resultado. No necesita conocer la técnica concreta utilizada.

Ejemplo completo, independiente de las variantes anteriores.

**Archivo: `Farmable.java`**

```java
public interface Farmable {
    String farm();
}
```

**Archivo: `Fishable.java`**

```java
public interface Fishable {
    String fish();
}
```

**Archivo: `Farming.java`**

```java
public final class Farming implements Farmable {
    @Override
    public String farm() {
        return "cultiva con herramientas manuales";
    }
}
```

**Archivo: `IrrigatedFarming.java`**

```java
public final class IrrigatedFarming implements Farmable {
    @Override
    public String farm() {
        return "cultiva con un sistema de riego";
    }
}
```

**Archivo: `Fishing.java`**

```java
public final class Fishing implements Fishable {
    @Override
    public String fish() {
        return "pesca con una red";
    }
}
```

**Archivo: `Villager.java`**

```java
import java.util.Objects;

public final class Villager implements Farmable, Fishable {
    private final String name;
    private final Farmable farming;
    private final Fishable fishing;

    public Villager(String name, Farmable farming, Fishable fishing) {
        this.name = Objects.requireNonNull(name, "name");
        if (name.isBlank()) {
            throw new IllegalArgumentException("El nombre no puede estar vacío");
        }
        this.farming = Objects.requireNonNull(farming, "farming");
        this.fishing = Objects.requireNonNull(fishing, "fishing");
    }

    @Override
    public String farm() {
        return name + " " + farming.farm();
    }

    @Override
    public String fish() {
        return name + " " + fishing.fish();
    }
}
```

**Archivo: `Main.java`**

```java
public class Main {
    public static void main(String[] args) {
        Villager ana = new Villager("Ana", new Farming(), new Fishing());
        Farmable luis = new Villager("Luis", new IrrigatedFarming(), new Fishing());
        System.out.println(ana.farm());
        System.out.println(ana.fish());
        System.out.println(luis.farm());
    }
}
```

Compilación y ejecución:

```sh
javac --release 17 *.java
java Main
```

Salida esperada:

```text
Ana cultiva con herramientas manuales
Ana pesca con una red
Luis cultiva con un sistema de riego
```

La secuencia de `ana.farm()` es: el cliente solicita cultivar a `Villager`; el aldeano llama a `farming.farm()`; el colaborador devuelve la descripción de la técnica; el aldeano añade su nombre y devuelve el resultado. En este ejemplo las actividades solo producen texto.

El aldeano conserva la responsabilidad de validar su construcción y presentar el resultado. El colaborador define la técnica de trabajo. La delegación puede incorporar coordinación o validación: no tiene que limitarse a reenviar una llamada sin cambios.

## Configuración y sustitución

Ana y Luis utilizan distintas implementaciones de cultivo sin crear nuevas subclases de aldeano. La elección se realiza al construirlos. Las referencias `final` impiden cambiarlas posteriormente; variar entre instancias no equivale a sustituir comportamientos durante la ejecución.

Si un requisito futuro exige cambiar de técnica en un objeto ya existente, habrá que decidir cómo validar esa transición y qué ocurre con las operaciones en curso. No se incorpora un setter solo por anticipar esa posibilidad.

## Elegir quién expone las operaciones

| Alternativa | Ventaja | Costo |
| --- | --- | --- |
| El aldeano ofrece `farm()` y `fish()` | El cliente utiliza una API directa | Agregar otra capacidad pública exige revisar esa API |
| Un servicio, como `WorkAssignment`, coordina la actividad | Mantiene pequeño el modelo del aldeano | El cliente utiliza un objeto adicional |
| Un registro permite recuperar capacidades por tipo | Admite conjuntos variables de capacidades | Requiere definir ausencia, duplicados y recuperación segura |

El ejemplo utiliza la primera alternativa y garantiza ambas capacidades mediante dependencias obligatorias. No representa aldeanos con conjuntos arbitrarios de oficios. Introducir una colección genérica o búsquedas con `instanceof` sería otra decisión, con costos propios.

## Comprobación conceptual

- ¿Qué responsabilidad conserva `Villager` después de delegar?
- ¿Qué cambia para agregar otra técnica de cultivo? ¿Y para agregar una nueva capacidad pública?
- ¿Por qué el código no garantiza inmutabilidad profunda aunque todos los campos sean `final`?

La siguiente etapa aborda el [control del estado mediante inmutabilidad](Immutability.md).
