# Taller: Herencia y Polimorfismo con Servicios de Transporte

## Objetivo

Aplicar los conceptos de **herencia y polimorfismo** mediante el diseño e implementación en Java de una jerarquía de clases para representar diferentes servicios de transporte de pasajeros, identificando atributos y comportamientos comunes, especializando las clases derivadas y utilizando un tipo base para almacenar y procesar objetos de diferentes tipos.

## Prerequisitos

Para desarrollar el taller, el estudiante debe comprender y aplicar los siguientes conceptos:

- **Herencia:** generalización y especialización de clases, reutilización de atributos y comportamientos, y construcción de jerarquías de clases.
- **Polimorfismo:** tratamiento de objetos de diferentes clases especializadas mediante un tipo común y ejecución del comportamiento correspondiente al tipo de objeto.
- **Manejo de excepciones:** diferenciación entre el lanzamiento y el manejo de excepciones para comunicar y controlar situaciones excepcionales durante la ejecución del programa.

## Enunciado del Taller

En este taller se propone construir un sistema orientado a objetos en Java que permita representar diferentes servicios de transporte de pasajeros. Todos los servicios deben poseer un identificador único (`id`) que permita consultarlos de manera individual y deben contener la información necesaria para calcular el valor de la tarifa correspondiente.

La forma en que se determina la tarifa varía según el servicio de transporte:

- El taxi (**Taxi**) cobra una tarifa base más un valor por kilómetro recorrido.
- El bus (**Bus**) cobra un valor fijo por pasajero transportado.
- El tren (**Train**) cobra un valor por kilómetro recorrido más un cargo fijo por el servicio ferroviario.
- El avión (**Airplane**) cobra una tarifa base más un valor por kilogramo de equipaje transportado.
- El barco (**Boat**) cobra una tarifa base más un valor por kilómetro recorrido y un cargo fijo de embarque.

Independientemente del tipo de transporte, el sistema debe ser capaz de calcular la tarifa de cada servicio. Para lograr una solución adecuada, el estudiante debe identificar qué elementos son comunes a todos los servicios de transporte y cuáles son específicos de cada caso, de manera que pueda aprovechar la **herencia** para evitar la duplicación de código y construir una jerarquía clara y coherente.

Además, el sistema debe aprovechar el **polimorfismo** para almacenar y procesar objetos de diferentes tipos mediante una **colección de servicios de transporte**.

Finalmente, se deberá construir un menú de opciones en consola que permita al usuario:

1. Crear un nuevo servicio de transporte (`Taxi`, `Bus`, `Train`, `Airplane` o `Boat`) y almacenarlo en la colección.
2. Mostrar todos los servicios almacenados, junto con su `id`, tipo, información correspondiente y tarifa calculada.
3. Consultar y mostrar la información de un servicio específico a partir de su `id`.
4. Calcular y mostrar el valor total de las tarifas de todos los servicios almacenados.
5. Salir del programa.

## Requisitos

### Organización del proyecto

La solución debe cuidar la separación de responsabilidades, organizando el proyecto en **dos carpetas (paquetes)**:

- **`domain`** → contiene las clases que representan los servicios de transporte: `TransportService`, `Taxi`, `Bus`, `Train`, `Airplane` y `Boat`.
- **`view`** → contiene la clase `Main`, responsable del menú de opciones y de la interacción con el usuario.

El arreglo utilizado para almacenar los servicios de transporte debe declararse y administrarse desde `Main`. Este arreglo debe utilizar `TransportService` como tipo base:

```java
TransportService[] services;
```

De esta manera, el sistema podrá almacenar en una misma estructura objetos pertenecientes a cualquiera de las clases derivadas de `TransportService` y procesarlos mediante polimorfismo.

### Requisitos adicionales

- En la **fase de análisis**, cada estudiante debe elaborar en papel un **diagrama de clases** que muestre la jerarquía de herencia, los atributos y los métodos principales de los servicios de transporte.
- El diagrama debe ser revisado y aprobado por el **jefe de proyectos** (el profesor). **Solo después de recibir la confirmación** se podrá pasar a la etapa de implementación en Java.
- Todas las clases deben incluir **constructores** que inicialicen los atributos más relevantes.
- Se deben implementar **métodos accesores (getters) y mutadores (setters)** para los atributos.
- Los **setters deben validar** que los valores asignados sean correctos; por ejemplo, las distancias, tarifas, cargos y pesos no pueden tener valores negativos, y el número de pasajeros debe ser mayor que cero.
- Si se recibe un valor no válido, una clase del dominio **no debe imprimir mensajes ni interactuar directamente con el usuario**. Debe lanzar una excepción que será manejada desde la capa `view`, responsable de la interacción y de mostrar los mensajes correspondientes al usuario.
- Las clases especializadas deben sobrescribir los métodos necesarios para calcular la **tarifa** de acuerdo con las características particulares de cada servicio de transporte.
- Al recorrer el arreglo `TransportService[]`, se deben aprovechar las referencias de tipo `TransportService` para invocar los métodos correspondientes de cada objeto mediante **polimorfismo**.

### Restricciones de estilo

Todos los identificadores deben seguir las convenciones de Java:

- **Upper Camel Case** para los nombres de clases (`TransportService`, `Taxi`, `Bus`).
- **Camel Case** para atributos y métodos (`distance`, `calculateFare()`).
- El **código fuente completo debe escribirse en inglés**: nombres de clases, atributos, variables y métodos.
- Los mensajes mostrados al usuario desde la capa `view` pueden escribirse en español o en inglés.
