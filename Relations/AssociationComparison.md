# Comparación de asociación, agregación y composición

La asociación, la agregación y la composición describen vínculos entre objetos. La agregación y la composición son formas de asociación que expresan una relación todo-parte. Esta guía retoma las comparaciones de [Relations.md](../Relations.md) y distingue el significado del modelo de las decisiones de implementación.

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
