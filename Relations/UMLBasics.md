# Estructura de una relación en un diagrama de clases UML
En un diagrama de clases UML, las relaciones permiten representar cómo interactúan las clases dentro de un sistema.
Para definir correctamente una relación, es necesario comprender sus elementos fundamentales y cómo se interpretan.
Una relación entre dos clases se compone de tres elementos principales:

* Las clases
* La línea de conexión y, si aplica, el símbolo que indica el tipo de relación
* La cardinalidad (multiplicidad)

## Representación básica

```text
[ClassA] --------> [ClassB]
      1              0..*
```

## Clases

Las clases se representan como **rectángulos (cajas)**.

Cada caja corresponde a una clase del sistema:

```text
[Person]        [Passport]
```

## Línea de relación

Las clases se conectan mediante una **línea**, que representa la existencia de una relación.

En este documento, siempre se utilizará una **línea con flecha** para indicar direccionalidad:

```text
Person --------> Passport
```

Interpretación:

* `Person` conoce a `Passport`
* `Person` tiene una referencia hacia `Passport`

Adicionalmente, según el tipo de relación, la línea puede incluir un símbolo en uno de sus extremos:

* **Sin símbolo** → [Asociación](Association.md)
* **Rombo negro (◆)** → [Composición](Composition.md)
* **Rombo blanco (◇)** → [Agregación](Aggregation.md)

El símbolo siempre se ubica en el lado de la clase que representa el **todo** en una relación todo-parte.

## Cardinalidad (multiplicidad)

La cardinalidad se ubica en **cada extremo de la línea**, no en el centro.

Indica cuántas instancias de una clase pueden relacionarse con instancias de la clase del otro extremo.

```text
Person --------> Passport
   1               0..1
```

Interpretación:

* El `0..1` cerca de `Passport` indica cuántos pasaportes puede tener una persona
* El `1` cerca de `Person` indica a cuántas personas puede estar asociado un pasaporte (por ejemplo: `1`, `0..1`, `0..*`, etc., según el modelo)

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
[School] --------> [Teacher]
     1                0..*
```

Interpretación:

* Una escuela puede tener muchos docentes
* Un docente está asociado a una escuela (según este modelo)
* Solo `School` conoce a `Teacher`

---

## Conclusión

Una relación en UML se define mediante:

* Dos clases (cajas)
* Una línea con dirección (flecha) y el tipo (rombo) si es requerido.
* Una cardinalidad en cada extremo
