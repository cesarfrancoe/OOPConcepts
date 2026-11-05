# Interfaces: contratos y capacidades

[Documento principal](README.md) · Anterior: [Herencia](Inheritance.md) · Siguiente: [Composición](Composition.md)

## Propósito

Separar lo que un objeto puede hacer de su posición en una jerarquía. Una interfaz define un tipo y un contrato; una clase puede implementar varias interfaces aunque solo pueda extender una clase.

## Del oficio a la capacidad

`Farmable` expresa la capacidad de cultivar y `Fishable` la de pescar. El contrato del ejemplo consiste en devolver una descripción no nula de la actividad. No se simulan recursos, inventarios ni efectos sobre un mundo externo.

Ejemplo completo e independiente de la etapa anterior. Cada bloque corresponde a un archivo.

**Archivo: `Farmable.java`**

```java
public interface Farmable {
    // Devuelve una descripción no nula de la actividad de cultivo.
    public abstract String farm();
}
```

**Archivo: `Fishable.java`**

```java
public interface Fishable {
    // Devuelve una descripción no nula de la actividad de pesca.
    String fish();
}
```

**Archivo: `Huntable.java`**

```java
public interface Huntable {
    // Devuelve una descripción no nula de la actividad de caza.
    String hunt();
}
```

**Archivo: `Villager.java`**

```java
import java.util.Objects;

public final class Villager implements Farmable, Fishable {
    private final String name;

    public Villager(String name) {
        this.name = Objects.requireNonNull(name, "name");
        if (name.isBlank()) {
            throw new IllegalArgumentException("El nombre no puede estar vacío");
        }
    }

    @Override
    public String farm() {
        return name + " cultiva";
    }

    @Override
    public String fish() {
        return name + " pesca";
    }
}
```

**Archivo: `Main.java`**

```java
public class Main {
    private static void performFarming(Farmable worker) {
        System.out.println(worker.farm());
    }

    public static void main(String[] args) {
        Villager villager = new Villager("Ana");
        performFarming(villager);
        Fishable fisher = villager;
        System.out.println(fisher.fish());
    }
}
```

Salida esperada:

```text
Ana cultiva
Ana pesca
```

El cliente `performFarming` depende de `Farmable`: no necesita conocer la clase del objeto ni sus demás capacidades. `Villager` cumple dos contratos y no implementa `Huntable`; declarar una interfaz no obliga a todas las clases a implementarla.

Esta variante representa aldeanos que siempre cultivan y pescan. No pretende modelar todavía una combinación distinta para cada instancia: las interfaces implementadas son una propiedad del tipo, no una lista modificable durante la ejecución.

## Qué cambia y qué sigue pendiente

| Aspecto | Resultado |
| --- | --- |
| Múltiples capacidades | Una clase puede cumplir varios contratos |
| Dependencias del cliente | Puede pedir únicamente la capacidad necesaria |
| Reutilización del algoritmo | Sigue pendiente: cada clase debe aportar su implementación |
| Variación entre instancias | Requiere otra decisión de diseño si las capacidades cambian por objeto |

Copiar `farm()` en varias clases no deja de ser duplicación por usar interfaces. La siguiente etapa separa esas implementaciones en colaboradores reutilizables.

## Contratos pequeños y explícitos

Un contrato incluye significado, entradas válidas, resultados y errores, además de la firma. El compilador verifica parte de su estructura; no garantiza que una implementación respete todas sus promesas semánticas.

No hace falta introducir una interfaz padre `Skill` si ningún cliente necesita una operación común. Una interfaz vacía puede tener usos específicos, pero no proporciona por sí sola una operación para ejecutar cualquier oficio.

Java también permite métodos `default` con implementación. Pueden servir para un comportamiento común coherente con el contrato, pero no reemplazan una decisión sobre quién posee el estado o cómo se comparten algoritmos. Si dos interfaces aportan implementaciones `default` incompatibles de la misma operación, la clase debe resolver el conflicto.

## Comprobación conceptual

- ¿Puede el cliente de `Farmable` utilizar un objeto que no sea un aldeano?
- ¿Qué promete `farm()` más allá de devolver un `String`?
- ¿Por qué implementar dos interfaces no permite cambiar los oficios de una instancia en ejecución?

Continuar con [composición](Composition.md) para separar las capacidades de sus implementaciones reutilizables.
