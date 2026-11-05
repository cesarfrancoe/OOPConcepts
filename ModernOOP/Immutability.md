# Inmutabilidad: controlar los cambios en el estado

[Documento principal](README.md) · Anterior: [Delegación](Delegation.md)

## Propósito

Comprender la mutabilidad y la inmutabilidad como decisiones de diseño. Primero se presenta una clase mutable, después una clase convencional inmutable y finalmente un `record` como alternativa para expresar ciertos valores con menos código.

## Mutabilidad e inmutabilidad

Un objeto es **mutable** si su estado observable puede cambiar después de construirse. Un mutador modifica el mismo objeto; todas las referencias a ese objeto permiten observar el cambio. Los setters son una forma de mutador, pero también lo son otras operaciones que alteran el estado.

Un objeto es **inmutable** si su estado observable permanece estable durante toda su vida. Puede ofrecer operaciones: cuando estas representan un cambio, pueden devolver otro objeto sin modificar el original.

Reemplazar una referencia no es modificar el objeto al que apuntaba. Una figura puede cambiar su posición asignándose otro punto, mientras el punto anterior permanece intacto. Así, una entidad mutable puede contener valores inmutables.

La inmutabilidad no depende de `record`. Una clase convencional puede diseñarse como mutable o inmutable. El `record` es una herramienta de Java para expresar valores mediante componentes; sus garantías deben analizarse según los datos que contiene.

## Primera versión: un punto mutable dentro de una figura

`Point` (Punto) permite modificar sus coordenadas. `Shape` (Figura) guarda un punto como centro y lo devuelve mediante un getter. Para modificar ambas coordenadas usamos `setPosition()` (establecer posición), en lugar de un setter de una sola coordenada.

**Archivo: `Point.java`**

```java
public class Point {
    private int x;
    private int y;

    public Point() {
        this(0, 0);
    }

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() {
        return x;
    }

    public int getY() {
        return y;
    }

    public void setPosition(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

**Archivo: `Shape.java`**

```java
public class Shape {
    private Point center;

    public Shape() {
        this(new Point());
    }

    public Shape(Point center) {
        this.center = center;
    }

    public Point getCenter() {
        return center;
    }

    public void setCenter(Point center) {
        this.center = center;
    }

    public void moveTo(int x, int y) {
        center.setPosition(x, y);
    }
}
```

El siguiente recorrido es válido y desplaza el centro hasta la posición `(99, 99)`:

```java
Shape shape = new Shape();
for (int step = 0; step < 100; step += 1) {
    shape.getCenter().setPosition(step, step);
}
```

El desplazamiento funciona. El problema aparece si el punto se comparte y sus cambios no deberían afectar a otros objetos.

## El problema aparece al compartir el punto

El campo privado no basta para proteger el centro: `getCenter()` (obtener centro) devuelve la misma referencia mutable. El cliente puede modificar la figura sin llamar a una operación de la propia figura.

Además, dos figuras pueden recibir el mismo punto. Desplazar una modifica también el centro de la otra. Una referencia guardada como «posición anterior» tampoco conserva una instantánea: sigue apuntando al objeto que cambia.

Esto es un problema si las figuras deben moverse independientemente o si necesitamos conservar posiciones anteriores. Si compartir deliberadamente una posición móvil fuera el requisito, ese mismo comportamiento podría ser correcto.

## Segunda versión: una clase convencional inmutable

`ImmutablePoint` (Punto inmutable) representa las mismas coordenadas sin permitir modificaciones posteriores.

**Archivo: `ImmutablePoint.java`**

```java
public final class ImmutablePoint {
    private final int x;
    private final int y;

    public ImmutablePoint(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() {
        return x;
    }

    public int getY() {
        return y;
    }
}
```

La inmutabilidad se obtiene mediante decisiones que actúan juntas:

- Los campos privados impiden que el cliente los modifique directamente.
- Los campos finales no pueden reasignarse después de su inicialización.
- No hay setters ni otras operaciones que modifiquen el punto.
- La clase final impide introducir subclases que alteren estas garantías.
- Sus componentes son enteros; no hay referencias internas a objetos mutables que puedan escapar.

### Una figura mutable con un centro inmutable

`ShapeWithValue` (Figura con valor) conserva un punto inmutable. Para desplazarla reemplaza su referencia al centro por otro punto.

**Archivo: `ShapeWithValue.java`**

```java
public class ShapeWithValue {
    private ImmutablePoint center;

    public ShapeWithValue() {
        this(new ImmutablePoint(0, 0));
    }

    public ShapeWithValue(ImmutablePoint center) {
        this.center = center;
    }

    public ImmutablePoint getCenter() {
        return center;
    }

    public void moveTo(int x, int y) {
        center = new ImmutablePoint(x, y);
    }
}
```

La figura sigue siendo mutable: su centro actual cambia. El punto permanece inmutable. Podemos devolverlo sin permitir que el cliente altere sus coordenadas; para cambiar la posición de la figura hay que utilizar su operación `moveTo()` (mover a).

```java
ShapeWithValue shape = new ShapeWithValue();
for (int step = 0; step < 100; step += 1) {
    shape.moveTo(step, step);
}
```

Cada iteración crea otro valor. Los puntos anteriores permanecen intactos si alguien conserva sus referencias.

## Demostración: dos figuras y una posición anterior

**Archivo: `Test.java`**

```java
public class Test {
    public static void main(String[] args) {
        Point sharedPoint = new Point(0, 0);
        Shape first = new Shape(sharedPoint);
        Shape second = new Shape(sharedPoint);
        Point previous = first.getCenter();

        first.getCenter().setPosition(10, 20);

        System.out.println("Mutable second: "
                + second.getCenter().getX() + ", " + second.getCenter().getY());
        System.out.println("Mutable previous: "
                + previous.getX() + ", " + previous.getY());

        ImmutablePoint sharedValue = new ImmutablePoint(0, 0);
        ShapeWithValue firstValue = new ShapeWithValue(sharedValue);
        ShapeWithValue secondValue = new ShapeWithValue(sharedValue);
        ImmutablePoint previousValue = firstValue.getCenter();

        firstValue.moveTo(10, 20);

        System.out.println("Value first: " + firstValue.getCenter().getX()
                + ", " + firstValue.getCenter().getY());
        System.out.println("Value second: " + secondValue.getCenter().getX()
                + ", " + secondValue.getCenter().getY());
        System.out.println("Value previous: " + previousValue.getX()
                + ", " + previousValue.getY());
    }
}
```

Salida esperada:

```text
Mutable second: 10, 20
Mutable previous: 10, 20
Value first: 10, 20
Value second: 0, 0
Value previous: 0, 0
```

En la primera versión, se modificó un objeto compartido: cambió la otra figura y se perdió la supuesta posición anterior. En la segunda, solo se reemplazó la referencia de la primera figura. La otra figura y el punto anterior conservaron sus valores.

### Diagrama de clases

```mermaid
classDiagram
    class Point {
        -int x
        -int y
        +getX() int
        +getY() int
        +setPosition(int x, int y) void
    }
    class Shape {
        +getCenter() Point
        +setCenter(Point center) void
        +moveTo(int x, int y) void
    }
    class ImmutablePoint {
        -int x
        -int y
        +getX() int
        +getY() int
    }
    class ShapeWithValue {
        +getCenter() ImmutablePoint
        +moveTo(int x, int y) void
    }
    Shape --> "1" Point : center
    ShapeWithValue --> "1" ImmutablePoint : center
```

## Encapsulamiento y mutadores

Encapsular significa controlar cómo se consulta y modifica el estado, no solo declarar campos privados. En la primera versión, el getter deja escapar una referencia mutable y permite evitar la API de movimiento de la figura. Cualquier validación o actualización adicional situada en esa API podría omitirse.

También puede protegerse una figura **sin usar un `record`**: copiar el punto recibido, devolver copias defensivas y ofrecer operaciones controladas para moverla. Hay que proteger tanto las referencias de entrada como las de salida. La segunda versión muestra precisamente la alternativa de una clase convencional inmutable.

Un mutador es cualquier método que cambia un objeto existente, no únicamente un setter. En estos ejemplos, `setPosition()` (establecer posición), `setCenter()` (establecer centro) y ambos métodos `moveTo()` (mover a) son mutadores de sus respectivos objetos. Reemplazar un centro inmutable no vuelve inmutable a la figura.

La segunda versión elimina los mutadores del **valor punto**, no los de la entidad figura. Esa combinación permite que una entidad evolucione mientras los valores compartidos o conservados como historial permanecen estables.

## Tercera versión: record como alternativa más breve

La clase convencional ya resolvió el problema de los valores compartidos. Ahora podemos evaluar un `record` para reducir el código necesario al representar el mismo valor.

**Archivo: `PointRecord.java`**

```java
public record PointRecord(int x, int y) {
}
```

El `record` genera el constructor, los campos privados y finales y los accesores `x()` (coordenada x) e `y()` (coordenada y). Para este punto, reemplaza la clase anterior por una declaración de dos líneas.

Ambas versiones mantienen estables las coordenadas. El beneficio del `record` es necesitar menos código para expresar ese valor.

La figura podría guardar `PointRecord` (Registro de punto) y construir uno nuevo en cada movimiento. La estrategia sería la misma: reemplazar el centro sin modificar el punto anterior.

### Diagrama de las dos alternativas inmutables

```mermaid
classDiagram
    class ImmutablePoint {
        -int x
        -int y
        +getX() int
        +getY() int
    }
    class PointRecord {
        <<record>>
        -int x
        -int y
        +x() int
        +y() int
    }
```

Son alternativas independientes, sin relación de herencia entre ellas.

### Comparación de las tres versiones

| Alternativa | Ventaja | Costo o límite |
| --- | --- | --- |
| Punto mutable | Permite actualizar el mismo objeto. | Las referencias compartidas observan los cambios; exige controlar quién puede modificarlo. |
| Clase convencional inmutable | Valores estables con control de representación y API. | Requiere escribir constructor y accesores. |
| Record con coordenadas enteras | Las mismas garantías de estabilidad con menos código. | Sus componentes determinan su API pública y restringe la representación y la herencia. |

Crear nuevos valores al cambiar de posición es una consecuencia del diseño inmutable, tanto con una clase como con un `record`. La clase convencional ofrece más libertad para ocultar la representación y diseñar su API. El `record` resulta adecuado cuando el valor se describe naturalmente mediante sus componentes.

## Ventajas y límites

Los puntos inmutables permiten compartir una posición sin cambios inesperados y conservar posiciones anteriores. La figura sigue siendo mutable y controla sus movimientos mediante su propia API.

Cada movimiento crea otro punto. Ese costo debe evaluarse cuando hay muchas actualizaciones; una clase mutable con acceso controlado también puede ser adecuada.

Un `record` con una lista mutable no sería automáticamente inmutable: habría que proteger esa lista. En este ejemplo, las coordenadas son enteros y no presentan ese problema.

## Comprobación conceptual

- ¿Por qué cambia el centro de la segunda figura en la primera versión?
- ¿Por qué una referencia al punto mutable no conserva una posición anterior?
- ¿Cómo protegerías la figura manteniendo una clase de punto mutable?
- ¿Por qué la figura que utiliza un punto inmutable sigue siendo mutable?
- ¿Qué decisiones hacen inmutable a la clase convencional y qué código permite omitir el `record`?
