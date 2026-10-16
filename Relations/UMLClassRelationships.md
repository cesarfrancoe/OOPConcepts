# Relaciones en un diagrama de clases UML
En un diagrama de clases UML, las relaciones permiten representar cómo interactúan las clases dentro de un sistema.
Para definir correctamente una relación, es necesario comprender sus elementos fundamentales y cómo se interpretan.
En una asociación (incluidas la agregación y la composición), se distinguen tres elementos principales:

* Las clases
* La línea de conexión y, si aplica, el símbolo que indica el tipo de relación
* La multiplicidad (también llamada cardinalidad en contextos pedagógicos)

## Representación básica

```text
+--------+          +--------+
| ClassA |--------->| ClassB |
+--------+          +--------+
    1                  0..*
```

## Clases

Las clases se representan como **rectángulos (cajas)**.

Cada caja corresponde a una clase del sistema:

```text
+--------+        +----------+
| Person |        | Passport |
+--------+        +----------+
```

## Línea de relación

Las clases se conectan mediante una **línea**, que representa la existencia de una relación.

En las asociaciones, las flechas indican la **navegabilidad**: desde qué clase se puede acceder a la otra. En estos ejemplos se utiliza la siguiente convención simplificada.

### Unidireccional

```text
+--------+          +----------+
| Person |--------->| Passport |
+--------+          +----------+
```

Interpretación:

* `Person` conoce a `Passport`
* `Person` tiene una referencia hacia `Passport`

### Bidireccional

```text
+--------+          +----------+
| Person |<-------->| Passport |
+--------+          +----------+
```

Ambas clases se conocen: `Person` tiene una referencia a `Passport` y `Passport` tiene una referencia a `Person`.

> En UML, una punta de flecha abierta indica un extremo navegable; una `x` indica uno no navegable. La ausencia de estos indicadores puede dejar la navegabilidad sin especificar: una línea sin flechas no implica por sí sola bidireccionalidad. En este material, una sola flecha se interpreta como unidireccional y dos flechas como bidireccional.

Adicionalmente, según el tipo de relación, la línea puede incluir un símbolo en uno de sus extremos:

* **Sin símbolo** → [Asociación](Association.md)
* **Rombo blanco (◇)** → [Agregación](Aggregation.md)
* **Rombo negro (◆)** → [Composición](Composition.md)


El rombo siempre se ubica en el lado de la clase que representa el **todo** en una relación todo-parte.

## Herencia (generalización)

La **herencia** expresa una relación **«es un»**: una subclase es una especialización de una superclase. En UML se representa mediante una **generalización**, con una línea continua y un **triángulo hueco que apunta a la superclase**.

```text
        +--------+
        | Animal |
        +--------+
            △
            |
        +--------+
        |  Dog   |
        +--------+
```

Interpretación:

* `Dog` es la subclase y `Animal` es la superclase
* Cada instancia de `Dog` es también una instancia de `Animal`; `Dog` hereda sus características y comportamientos, según las reglas del lenguaje
* El triángulo indica generalización; no representa navegabilidad
* La generalización no lleva multiplicidades: no cuenta objetos relacionados, sino que expresa una relación entre tipos

Más detalles en [Herencia](../Inheritance.md).

## Cardinalidad (multiplicidad)

El término formal de UML es **multiplicidad**; **cardinalidad** es una denominación común en contextos pedagógicos. En este documento se usan ambos términos para referirse a los valores permitidos en cada extremo.

La multiplicidad se ubica en **cada extremo de la línea**, no en el centro.

Indica cuántas instancias de una clase pueden relacionarse con instancias de la clase del otro extremo.

```text
+--------+          +----------+
| Person |--------->| Passport |
+--------+          +----------+
    1                   0..1
```

Interpretación:

* El `0..1` cerca de `Passport` indica que cada persona puede tener cero o un pasaporte
* El `1` cerca de `Person` indica que cada pasaporte está asociado exactamente a una persona

> La cardinalidad siempre se interpreta desde el extremo opuesto de la relación.

## Tipos de cardinalidad

La cardinalidad puede expresarse de dos formas:

### Valor único

Cuando se muestra un solo número (por ejemplo, `1`):

* Indica una **cantidad exacta**
* No hay variación posible

Ejemplo:

* `1` → exactamente una instancia

### Rango (mínimo..máximo)

Cuando se expresa como un rango:

* El primer valor indica el **mínimo**
* El segundo valor indica el **máximo**

Ejemplos:

* `0..1` → cero o una instancia (opcional)
* `1..*` → una o muchas instancias
* `0..*` → cero o muchas instancias

## Nota importante

> El símbolo `*` representa “muchos”, es decir, un número no limitado de instancias.
> En UML es común utilizar `*` como abreviación de `0..*`. Sin embargo, en este documento se utilizará siempre `0..*` para hacer explícito que la relación permite desde cero hasta muchas instancias.

## Ejemplo completo

```text
+--------+          +---------+
| School |--------->| Teacher |
+--------+          +---------+
    1                  0..*
```

Interpretación:

* Cada escuela puede tener cero o muchos docentes
* Cada docente está asociado a una escuela (según este modelo)
* Solo `School` conoce a `Teacher`

---

## Conclusión

Las relaciones se representan mediante clases (cajas) y líneas con los símbolos correspondientes:

* En las asociaciones, se indican las multiplicidades y, cuando corresponda, la navegabilidad y el rombo de agregación o composición
* En la herencia, se utiliza un triángulo hueco que apunta a la superclase, sin multiplicidades
