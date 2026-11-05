# Evolución de la Programación Orientada a Objetos: de las jerarquías a la composición

Esta ruta propone pasar de un diseño centrado en jerarquías de herencia a decisiones que combinan interfaces, composición y delegación, junto con un control explícito de la mutabilidad. El propósito es comprender qué problema resuelve cada mecanismo y cuándo conviene utilizarlo, no acumular técnicas ni construir el sistema más flexible posible.

## Objetivos de aprendizaje

La ruta tiene los siguientes objetivos:

- Reconocer cuándo una jerarquía expresa una especialización válida y cuándo introduce rigidez o acoplamiento innecesario.
- Definir capacidades mediante interfaces y utilizar polimorfismo sin depender de una clase concreta.
- Reutilizar comportamiento mediante objetos colaboradores y distinguir composición de delegación.
- Decidir qué estado puede cambiar, quién puede modificarlo y cuándo conviene diseñar objetos inmutables.
- Justificar decisiones de diseño comparando claridad, cohesión, acoplamiento y costo del cambio.

## Alcance y conocimientos previos

Se parte del conocimiento de clases, objetos, constructores, encapsulamiento, herencia simple y sobrescritura de métodos en Java. Como referencia inicial puede consultarse el [documento general del repositorio](../README.md).

El documento principal organiza la ruta y establece criterios comunes. Las explicaciones detalladas, los ejemplos completos y las preguntas de revisión se encuentran en los subdocumentos; este índice presenta su organización. No se requiere introducir frameworks, sistemas de complementos ni catálogos completos de patrones de diseño.

Como hilo conductor se utiliza el problema de los aldeanos y sus oficios: una jerarquía con `Villager`, `Farmer`, `Fisherman` y `Hunter` permite explorar qué ocurre cuando un aldeano necesita varias capacidades. Los ejemplos Java se presentan dentro de los documentos y cada etapa se ejecuta en una carpeta independiente.

## POO clásica y moderna: énfasis pedagógicos

En esta ruta, **POO clásica** y **POO moderna** nombran énfasis de enseñanza, no paradigmas separados ni etapas que invaliden lo anterior. Las interfaces, la composición, la delegación y la inmutabilidad tienen una larga historia; su uso no depende de que una práctica sea reciente.

| Énfasis inicial | Énfasis que se incorpora |
| --- | --- |
| Organizar comportamientos mediante jerarquías de clases | Expresar capacidades mediante contratos |
| Reutilizar implementación mediante herencia | Evaluar la reutilización mediante colaboradores |
| Resolver variantes creando subclases | Combinar comportamientos cuando el problema lo justifique |
| Depender directamente de clases concretas | Depender de abstracciones útiles para el cliente |
| Modificar el estado mediante operaciones mutadoras | Decidir explícitamente qué estado debe ser mutable o inmutable |

La herencia sigue siendo apropiada cuando existe una especialización coherente y los subtipos respetan el contrato del tipo base. Favorecer la composición es un criterio de evaluación, no una prohibición de heredar. Del mismo modo, la inmutabilidad no exige convertir todos los objetos en valores inmutables.

## Secuencia de aprendizaje

1. **Examinar la herencia.** Partir de una jerarquía sencilla e introducir un requisito de múltiples oficios. Identificar si aparecen combinaciones de subclases, duplicación o responsabilidades mal ubicadas antes de cambiar el diseño.
2. **Separar capacidades con interfaces.** Describir qué puede hacer un objeto sin imponer una única ascendencia de clases. Distinguir el contrato de la implementación y reconocer que una interfaz, por sí sola, no elimina la duplicación de comportamiento.
3. **Introducir composición.** Explorar cómo un objeto puede recibir y utilizar colaboradores que aportan comportamiento. Comparar sus dependencias y posibilidades de cambio con las de la jerarquía inicial.
4. **Hacer explícita la delegación.** Identificar qué objeto recibe una solicitud, a cuál encarga su ejecución y qué responsabilidad conserva. Tener un colaborador no implica delegarle automáticamente todas las operaciones.
5. **Revisar el estado con inmutabilidad.** Evaluar qué datos pueden permanecer estables y cómo protegerlos. Esta etapa aborda la administración del estado, una dimensión transversal que complementa la organización del comportamiento.

En cada paso, la pregunta guía es: **¿qué requisito motiva el cambio y qué costo introduce la solución?** El resultado esperado es una decisión argumentada, no aplicar todos los mecanismos a todos los problemas.

## Mapa de documentos

Los siguientes enlaces son relativos a `ModernOOP/`. Cada documento desarrolla una etapa con conceptos, ejemplos ejecutables y preguntas de revisión.

| Orden | Documento | Foco en la ruta | Estado |
| --- | --- | --- | --- |
| 1 | [Herencia](Inheritance.md) | Evaluar jerarquías y sus limitaciones | Disponible |
| 2 | [Interfaces](Interfaces.md) | Expresar contratos y capacidades | Disponible |
| 3 | [Composición](Composition.md) | Organizar comportamiento mediante colaboradores | Disponible |
| 4 | [Delegación](Delegation.md) | Distribuir la ejecución de responsabilidades | Disponible |
| 5 | [Inmutabilidad](Immutability.md) | Controlar los cambios en el estado | Disponible |

## Principios transversales

- **Encapsulamiento e invariantes:** proteger las reglas que mantienen válido un objeto; proporcionar getters y setters no garantiza por sí solo un buen encapsulamiento.
- **Sustitución y contratos:** un subtipo o una implementación debe poder utilizarse respetando las expectativas del cliente, sin exigir que este conozca detalles internos.
- **Cohesión y bajo acoplamiento:** reunir responsabilidades relacionadas y limitar las dependencias necesarias para cumplirlas.
- **Abstracciones con propósito:** introducir interfaces cuando expresen un contrato útil; evitar crear una interfaz por cada clase de manera automática.
- **Composición y delegación:** la primera organiza colaboradores; la segunda encarga una operación a otro objeto. En esta ruta, composición se usa en el sentido de diseño por colaboración y no exige siempre la propiedad exclusiva y el ciclo de vida dependiente de la composición UML. Véase la [composición como relación UML](../Relationships/Composition.md).
- **Estado y efectos:** distinguir las decisiones sobre comportamiento de las decisiones sobre mutabilidad. Una referencia `final` no hace inmutable al objeto referenciado; cuando hay datos mutables compartidos, evaluar copias defensivas y control de acceso.
- **Simplicidad y verificación:** introducir cambios por requisitos concretos y comprobar que se conserva el comportamiento esperado. La flexibilidad adicional debe justificar su complejidad.

## Convenciones para los ejemplos en Java 17+

- Utilizar Java 17 como base, compatible con versiones posteriores, sin características de vista previa ni dependencias externas salvo justificación explícita.
- Redactar las explicaciones en español y mantener identificadores Java en inglés: `PascalCase` para tipos, `camelCase` para métodos y variables, y `UPPER_SNAKE_CASE` para constantes.
- Indicar el nombre de archivo de cada ejemplo completo y mantener un tipo público de nivel superior por archivo, con nombre coincidente. Señalar expresamente los fragmentos parciales y mantener las variantes de cada etapa separadas para evitar tipos duplicados.
- Usar campos `private`, constructores que establezcan un estado válido y `@Override` al implementar o sobrescribir métodos. Hacer explícitas las reglas sobre valores nulos cuando afecten al contrato.
- Recibir colaboradores por constructor cuando sean necesarios para el objeto y declarar las dependencias mediante interfaces cuando estas aporten un contrato útil. La configuración intercambiable es una decisión del ejemplo, no una obligación de permitir cambios en ejecución.
- Usar `final` cuando una referencia no deba reasignarse. Para objetos inmutables, revisar también los objetos alcanzables y las referencias que se reciben o exponen; una vista no modificable de una colección no equivale a una copia independiente.
- Utilizar `record` para representar datos con semántica de valor cuando corresponda. Sus componentes no pueden reasignarse, pero un `record` no garantiza inmutabilidad profunda si contiene objetos mutables.
- Mantener los ejemplos pequeños y centrados en el requisito de cada etapa. Cuando se presenten programas ejecutables, incluir un punto de entrada claro y el comportamiento esperado.
