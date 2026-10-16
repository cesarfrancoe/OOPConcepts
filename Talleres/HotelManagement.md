# Taller: Diseño e Implementación de un Sistema de Gestión Hotelera

## Objetivo

Aplicar los conceptos de **herencia, polimorfismo, asociación, agregación y composición** mediante el análisis, diseño e implementación de un sistema de gestión hotelera, identificando las responsabilidades de las clases, sus atributos, comportamientos y relaciones.

El taller se desarrollará en dos partes:

- **Parte I. Análisis y diseño orientado a objetos:** elaboración y sustentación de un diagrama de clases UML.
- **Parte II. Implementación en Java:** desarrollo del modelo (`model`) y construcción de una interfaz gráfica (`view`) utilizando Java Swing.

La actividad principal será el diseño orientado a objetos. La implementación deberá realizarse a partir del diagrama de clases aprobado.

## Prerrequisitos

- **Herencia:** generalización y especialización de clases, reutilización de atributos y comportamientos, y construcción de jerarquías.
- **Polimorfismo:** utilización de tipos comunes para representar objetos de diferentes clases y ejecutar comportamientos especializados.
- **Relaciones entre clases:** asociación, agregación y composición, considerando multiplicidades, navegabilidad y ciclos de vida de los objetos.
- **Diagramas de clases UML:** representación de clases, atributos, métodos, visibilidad y relaciones.
- **Manejo de excepciones:** lanzamiento y manejo de excepciones para comunicar y controlar situaciones excepcionales.

---

## Enunciado del Taller

Un hotel necesita desarrollar un sistema orientado a objetos que permita administrar sus habitaciones, huéspedes y reservas.

El sistema debe representar las características particulares de las habitaciones, los servicios disponibles y las operaciones relacionadas con el alojamiento.

### 1. Habitaciones

El hotel dispone de cuatro tipos de habitaciones:

**Habitación individual (Single Room)**

Está diseñada para alojar una persona y dispone de una cama individual. Su valor de alojamiento se calcula multiplicando la tarifa básica por noche por la cantidad de noches reservadas.

**Habitación doble (Double Room)**

Permite alojar una o dos personas y dispone de una cama doble. Su tarifa básica cubre la ocupación de una persona; cuando se alojan dos, se aplica un cargo adicional por noche.

**Habitación familiar (Family Room)**

Permite alojar hasta seis personas y dispone de varias camas. Su tarifa básica incluye el alojamiento de cuatro personas. Por cada huésped adicional se aplica un cargo por persona y por noche.

**Suite**

Es una habitación de categoría superior que dispone de una sala privada. Su valor de alojamiento corresponde a la tarifa básica por noche más un cargo fijo por noche asociado a sus características especiales.

Todas las habitaciones deben tener:

- Número único.
- Capacidad máxima de ocupación.
- Tarifa básica por noche.
- Estado operativo que permita identificar si la habitación se encuentra habilitada o fuera de servicio por mantenimiento.

La disponibilidad para realizar reservas deberá determinarse a partir de las reservas existentes y no mediante un atributo adicional de disponibilidad.

Adicionalmente, las habitaciones pueden ofrecer diferentes servicios, como televisión, aire acondicionado, minibar o acceso a internet.

Cada servicio debe contar con un identificador, nombre y descripción. Un mismo servicio puede estar disponible en varias habitaciones y una habitación puede ofrecer múltiples servicios.

### 2. Huéspedes

El hotel mantiene un registro de huéspedes.

De cada huésped se debe almacenar:

- Identificador único.
- Nombre completo.
- Documento de identificación.
- Número de teléfono.
- Correo electrónico.

Un huésped puede realizar diferentes reservas a lo largo del tiempo.

### 3. Reservas

Cada reserva debe registrar:

- Identificador único.
- Huésped responsable.
- Habitación asignada.
- Cantidad de huéspedes.
- Cantidad de noches.
- Estado de la reserva.

El sistema debe calcular el valor total del alojamiento considerando el tipo de habitación, la cantidad de huéspedes y las noches reservadas.

Una reserva puede encontrarse en uno de los siguientes estados:

- **Pendiente:** registrada, pero todavía no confirmada.
- **Confirmada:** aprobada y con la habitación asignada.
- **Cancelada:** anulada.

Para simplificar el problema:

- Una habitación solo podrá tener una reserva pendiente o confirmada a la vez.
- Una reserva cancelada no bloquea la habitación.
- No será necesario administrar fechas de entrada y salida.
- No se podrán crear reservas para habitaciones fuera de servicio.
- La cantidad de huéspedes no podrá superar la capacidad máxima de la habitación.

### 4. Comprobantes

Cuando una reserva sea confirmada, el sistema deberá generar un comprobante que contenga:

- Número único del comprobante.
- Identificador de la reserva.
- Nombre del huésped responsable.
- Número de habitación.
- Cantidad de noches.
- Valor total del alojamiento.

El comprobante pertenece exclusivamente a la reserva que lo originó. No puede compartirse entre reservas ni existir independientemente de ella.

Una reserva pendiente no debe tener comprobante. Si una reserva confirmada se cancela posteriormente, su comprobante deberá conservarse como constancia de la confirmación realizada.

### 5. Administración del hotel

El hotel debe contar con:

- Identificador único.
- Nombre comercial.
- Dirección.

El sistema debe permitir administrar las habitaciones, los huéspedes y las reservas correspondientes.

Las habitaciones tienen identidad propia y pueden ser trasladadas administrativamente a otro hotel sin perder su información. Los huéspedes también conservan su identidad independientemente del hotel donde se registren.

---

# Parte I. Análisis y Diseño Orientado a Objetos

**Esta es la parte principal del taller.**

Su propósito es construir un modelo de clases que represente adecuadamente el problema, identificando responsabilidades, atributos, comportamientos y relaciones antes de iniciar la programación.

## 1. Identificación de clases

A partir del enunciado, identifique las clases necesarias para representar el sistema hotelero.

El diseño deberá contener **aproximadamente diez clases de dominio**, sin incluir las clases correspondientes a la interfaz gráfica.

Para cada clase determine:

- Nombre y responsabilidad principal.
- Atributos y tipos de datos.
- Métodos y tipos de retorno.
- Constructores necesarios.
- Visibilidad de atributos y métodos.

Evite duplicar atributos o comportamientos que puedan ubicarse adecuadamente en una clase más general.

## 2. Identificación de relaciones

Analice las relaciones entre las clases y determine cuáles corresponden a:

- **Herencia:** relaciones de generalización y especialización.
- **Asociación:** vínculos entre objetos que mantienen identidades independientes.
- **Agregación:** relaciones entre un todo y sus partes cuando estas pueden existir independientemente.
- **Composición:** relaciones en las que una parte pertenece exclusivamente a un todo y su ciclo de vida depende de este.

Para las relaciones estructurales, identifique las multiplicidades y la navegabilidad cuando corresponda.

Las relaciones deberán seleccionarse de acuerdo con el significado del problema y no únicamente para utilizar una determinada notación UML.

## 3. Elaboración del diagrama de clases UML

Elabore en papel un diagrama de clases que contenga:

1. Las clases identificadas.
2. Los atributos con sus tipos de datos y visibilidad.
3. Los métodos principales con parámetros, tipos de retorno y visibilidad.
4. Los constructores.
5. Las relaciones de herencia y las relaciones estructurales correspondientes.
6. Las multiplicidades y la navegabilidad.
7. Las clases y métodos abstractos, cuando se consideren necesarios.

El diagrama deberá reflejar las decisiones de diseño del estudiante.

## 4. Sustentación del diseño

Cada estudiante deberá presentar su diagrama de clases al **jefe de proyectos (profesor)**.

Durante la sustentación deberá explicar:

- Por qué identificó las clases propuestas.
- Qué atributos y comportamientos corresponden a cada clase.
- Qué elementos pueden generalizarse mediante herencia.
- Cómo se aplicará el polimorfismo.
- Por qué seleccionó cada relación estructural.
- Qué significan las multiplicidades utilizadas.
- Cómo se garantiza la coherencia entre las responsabilidades de los objetos.

**Se admitirán diferentes soluciones siempre que sean coherentes con el problema y estén debidamente justificadas.**

El diagrama deberá ser revisado y aprobado por el profesor.

**Solo después de recibir la aprobación podrá iniciarse la Parte II.**

---

# Parte II. Implementación en Java

La implementación deberá corresponder al diagrama de clases aprobado y se desarrollará en dos etapas.

## A. Implementación del modelo (`model`)

### 1. Organización

Implemente las clases del sistema hotelero dentro del paquete `model`.

Cada clase deberá contener los atributos, constructores y métodos definidos en el diagrama.

### 2. Requisitos

- Aplicar encapsulamiento mediante métodos accesores y mutadores cuando corresponda.
- Implementar las relaciones de herencia y aprovechar el polimorfismo.
- Implementar las relaciones estructurales respetando sus multiplicidades.
- Calcular correctamente el valor del alojamiento según el tipo de habitación.
- Validar la capacidad máxima de las habitaciones.
- Evitar reservas activas simultáneas sobre una misma habitación.
- Impedir la creación de reservas para habitaciones fuera de servicio.
- Garantizar que los comprobantes se generen únicamente al confirmar una reserva.
- Validar los valores de los atributos y lanzar excepciones ante situaciones no válidas.
- Evitar dependencias de Java Swing y cualquier interacción directa con el usuario.

Antes de desarrollar la interfaz gráfica, el estudiante deberá comprobar el funcionamiento del modelo mediante clases de prueba.

## B. Implementación de la vista (`view`)

Una vez implementado y probado el modelo, construya una interfaz gráfica utilizando **Java Swing**.

### 1. Funcionalidades

La interfaz deberá permitir:

1. Registrar habitaciones de diferentes tipos.
2. Registrar huéspedes.
3. Crear reservas.
4. Confirmar y cancelar reservas.
5. Consultar las habitaciones registradas.
6. Consultar los huéspedes.
7. Consultar las reservas de un huésped.
8. Mostrar una reserva y su comprobante.
9. Consultar los servicios disponibles en una habitación.
10. Calcular el valor total de las reservas confirmadas.

### 2. Uso de inteligencia artificial

Para desarrollar la interfaz gráfica, **se permite y recomienda utilizar herramientas de inteligencia artificial generativa**.

Estas herramientas podrán utilizarse para:

- Diseñar ventanas, formularios y tablas.
- Generar componentes gráficos de Java Swing.
- Implementar mecanismos de navegación e interacción.
- Mejorar la presentación visual de la aplicación.

Sin embargo, deberán respetarse las siguientes condiciones:

- La interfaz debe utilizar las clases y métodos del modelo aprobado.
- La IA no debe modificar arbitrariamente el diseño del modelo.
- Los cálculos y las reglas de negocio deben permanecer en `model`.
- Las excepciones lanzadas desde `model` deben manejarse desde `view`.
- El estudiante debe comprender y poder explicar el funcionamiento de la interfaz generada.

El propósito del uso de IA es facilitar la construcción de la interfaz gráfica, permitiendo concentrar el esfuerzo académico en el diseño orientado a objetos.

## Restricciones generales

- Todos los identificadores del código fuente deben escribirse en inglés.
- Los nombres de clases deben utilizar **Upper Camel Case**.
- Los nombres de atributos, variables y métodos deben utilizar **Camel Case**.
- Los mensajes de la interfaz pueden escribirse en español o en inglés.
- No se requiere utilizar bases de datos ni mecanismos de persistencia.
- Las clases del modelo no deben depender de las clases de la vista.
- La implementación debe respetar el diagrama UML aprobado. Cualquier modificación estructural deberá justificarse.

---

## Entregables

### Parte I. Diseño

- Diagrama de clases UML elaborado en papel.
- Sustentación individual del diseño.
- Aprobación del profesor.

### Parte II. Implementación

- Proyecto Java organizado en los paquetes `model` y `view`.
- Implementación funcional del modelo.
- Clases de prueba del modelo.
- Interfaz gráfica desarrollada con Java Swing.
- Código fuente consistente con el diagrama aprobado.
