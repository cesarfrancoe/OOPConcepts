# Comparación de asociación, agregación y composición

La asociación, la agregación y la composición describen vínculos entre objetos. La agregación y la composición son formas de asociación que expresan una relación todo-parte. Esta guía retoma las comparaciones de [Relations.md](../Relations.md) y distingue el significado del modelo de las decisiones de implementación.

## La duda principal: asociación o agregación

**Que cada objeto pueda existir independientemente no distingue estas dos relaciones:** esa independencia es compatible con ambas. La pregunta que las separa es si el modelo expresa únicamente un vínculo o también una relación todo-parte.

* **Asociación simple:** cada estudiante se inscribe en cursos. El vínculo representa una inscripción; cada curso no es una parte del estudiante.
* **Agregación:** cada equipo agrupa jugadores como integrantes del conjunto. Cada jugador puede seguir existiendo al abandonar el equipo.

La expresión «tiene» tampoco basta: cada estudiante «tiene cursos», pero eso no obliga a modelar agregación. Debe existir una interpretación todo-parte relevante para el problema. Incluso el mismo par de clases puede modelarse de manera diferente según lo que se quiera expresar.

> El rombo blanco añade intención de modelado, pero no impone una sintaxis especial en Java. UML deja las reglas precisas de la agregación compartida al dominio y al modelador; por eso deben explicarse. Si no hay una relación todo-parte clara, la asociación simple es suficiente.

## Comparación conceptual

En esta tabla, **asociación simple** se refiere a la asociación sin agregación ni composición.

| Criterio | Asociación simple | Agregación | Composición |
| --- | --- | --- | --- |
| Significado | Vínculo entre objetos | Relación todo-parte con independencia de las partes | Relación todo-parte con pertenencia exclusiva |
| Pertenencia | No establece pertenencia todo-parte | Agrupa partes; las reglas concretas dependen del modelo | Cada parte pertenece como máximo a un todo compuesto a la vez |
| Ciclo de vida | El vínculo no impone dependencia | Cada parte puede seguir existiendo sin el todo | Al eliminar el todo, se eliminan las partes que aún lo componen |
| Compartición | Según las reglas del modelo | Puede permitirse según las reglas del modelo | Cada parte no puede pertenecer simultáneamente a varios todos compuestos |
| Símbolo UML | Línea sin rombo | Rombo blanco junto al todo | Rombo negro junto al todo |
| Ejemplo | Estudiante–Curso | Equipo–Jugador | Documento–Página |

El rombo blanco expresa una agrupación todo-parte, pero no define por sí solo reglas universales de propiedad o compartición. Estas deben precisarse en el modelo.

## Comparación de implementación

Las tres relaciones pueden representarse mediante referencias o colecciones. La diferencia está en las reglas de pertenencia y ciclo de vida que la implementación debe respetar.

| Pregunta | Asociación simple | Agregación | Composición |
| --- | --- | --- | --- |
| ¿Quién crea el objeto relacionado? | El tipo de relación no lo determina | El tipo de relación no lo determina | Puede crearlo el todo o recibirlo; debe respetarse la pertenencia exclusiva |
| ¿Puede recibirse por constructor o método? | Sí | Sí | Sí, siempre que se controle su incorporación y pertenencia |
| ¿Puede compartirse la misma instancia? | Si el modelo lo permite | Si el modelo lo permite | No como parte de varios todos compuestos a la vez; otras referencias no implican pertenencia |
| ¿Puede faltar el objeto relacionado? | Según la multiplicidad | Según la multiplicidad | Según la multiplicidad |
| ¿Qué debe controlar la implementación? | Los vínculos y sus multiplicidades | La agrupación y la independencia de las partes | La exclusividad y el ciclo de vida de las partes |

Recibir el objeto por constructor, usar `new`, declarar un atributo `final` o utilizar una colección no basta para identificar la relación. Tampoco una validación de `null` convierte una asociación en agregación.

## Del diagrama al código

Cada extremo navegable puede representarse mediante una referencia o una colección. Después se implementan las multiplicidades y las reglas del modelo: valores obligatorios, límites, duplicados, coherencia bidireccional y, cuando corresponda, pertenencia y ciclo de vida.

### Asociación y agregación pueden tener la misma estructura

Estos fragmentos muestran solo el almacenamiento de los vínculos; no implementan todas las restricciones de un diagrama.

**Asociación simple: cada estudiante conoce los cursos en los que está inscrito.**

```java
import java.util.ArrayList;
import java.util.List;

public class Student {
    private final List<Course> courses = new ArrayList<>();

    public void enroll(Course course) {
        courses.add(course);
    }
}
```

**Agregación: cada equipo agrupa jugadores como integrantes.**

```java
import java.util.ArrayList;
import java.util.List;

public class Team {
    private final List<Player> players = new ArrayList<>();

    public void addPlayer(Player player) {
        players.add(player);
    }
}
```

En ambos casos se almacenan referencias a objetos recibidos desde fuera. La colección y el método de incorporación tienen la misma estructura; la diferencia es el significado de inscripción frente al de pertenencia a un conjunto. `Course` y `Player` representan clases definidas por separado.

Pueden existir diferencias de implementación si las reglas del problema las exigen. Por ejemplo, impedir que cada jugador pertenezca a varios equipos requiere validar su pertenencia. Esa restricción no surge automáticamente del rombo blanco: debe constar en el modelo. Del mismo modo, cada asociación simple puede necesitar validaciones propias.

## Del código al diagrama

**Sí, se puede reconstruir un diagrama a partir del código, pero no recuperar siempre toda la intención del modelo.** Este proceso se conoce como ingeniería inversa.

| Lo que se observa en el código | Lo que permite proponer | Lo que todavía debe confirmarse |
| --- | --- | --- |
| Un atributo de tipo `B` en `A` | Un vínculo navegable desde `A` hacia `B` | Si es asociación simple, agregación o composición; si el valor es obligatorio |
| Una colección de `B` en `A` | Un extremo que admite varios objetos | El mínimo, el máximo y las reglas de pertenencia |
| Referencias en ambas clases | Posible navegabilidad bidireccional | Que las referencias representen la misma relación y se mantengan coherentes |
| Creación de `B` dentro de `A` | Que `A` participa en la creación de `B` | Si existe pertenencia exclusiva y dependencia del ciclo de vida |

Estos indicios requieren interpretar los atributos en su contexto. Una variable local o un parámetro usado temporalmente puede representar una dependencia de uso, sin establecer una asociación almacenada.

Para decidir entre asociación y agregación, hay que consultar además los requisitos, la documentación y el significado de los objetos. Si solo se encuentra `List<Player>`, no se puede concluir que existe agregación. Tampoco `new Player()` demuestra composición.

La traducción no es única: distintos diagramas pueden dar lugar a estructuras de código similares, y cada diagrama puede admitir varias implementaciones correctas. En Java, además, la recolección de basura no implementa por sí sola las reglas de eliminación del modelo.

## Cómo elegir la relación

1. Si solo se necesita representar un vínculo entre objetos, usar **asociación simple**.
2. Si existe una relación todo-parte y cada parte conserva su independencia, considerar **agregación** y explicitar sus reglas.
3. Si cada parte pertenece de manera exclusiva al todo y su eliminación está ligada a él, usar **composición**.

La elección depende de lo que representan los objetos en el problema. Por ejemplo, cada jugador puede seguir existiendo al desaparecer su equipo; cada página de un documento se elimina con él, según ese modelo. En composición, una parte puede separarse o transferirse antes de eliminar el todo, si las reglas del modelo lo permiten.

## Multiplicidad y navegabilidad

La multiplicidad indica **cuántos objetos** pueden participar y la navegabilidad indica **desde qué extremo se puede acceder al otro**. Ninguna de estas características determina por sí sola si la relación es asociación simple, agregación o composición.

## Lecturas relacionadas

* [Asociación](Association.md)
* [Agregación](Aggregation.md)
* [Composición](Composition.md)
* [Relaciones en un diagrama de clases UML](UMLClassRelationships.md)

## Referencia UML

[Especificación UML 2.5.1 de OMG](https://www.omg.org/spec/UML/2.5.1/PDF), sección 9.5.3: semántica de agregación compartida y composición.
