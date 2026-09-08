# Taller 01 - Abstracción y Encapsulamiento

## Objetivo

Desarrollar la capacidad de abstraer, a partir de diferentes situaciones planteadas, los atributos y comportamientos necesarios para representar entidades mediante clases, aplicando los conceptos de encapsulamiento, métodos accesores y métodos mutadores estudiados previamente.

Antes de desarrollar el taller, estudie la documentación suministrada sobre **atributos, métodos y encapsulamiento**.

## Organización y entrega del taller

Todos los talleres desarrollados durante el curso deberán almacenarse en el repositorio de GitHub creado previamente utilizando el correo institucional.

El repositorio deberá tener el siguiente nombre:

```text
POO2026
```

Dentro del repositorio deberá crear una carpeta denominada `Talleres`. Cada taller deberá almacenarse en una carpeta independiente, utilizando numeración consecutiva.

Para este taller, la estructura deberá ser:

```text
POO2026/
└── Talleres/
    └── Taller01/
```

Todos los archivos correspondientes a la solución de este taller deberán almacenarse dentro de `Taller01`.

A medida que avance el curso, el repositorio tendrá una estructura similar a:

```text
POO2026/
└── Talleres/
    ├── Taller01/
    ├── Taller02/
    ├── Taller03/
    └── ...
```

Los estudiantes deberán realizar `commit` y `push` de sus soluciones para que los archivos queden disponibles en el repositorio remoto de GitHub.

## Escenario de desarrollo

Para cada ejercicio, suponga que participan dos desarrolladores:

**Desarrollador 1** implementa la clase que representa la entidad planteada en el problema. Es responsable de definir sus atributos, comportamientos y las reglas necesarias para conservar la integridad de su estado.

**Desarrollador 2** implementa la clase de prueba. Este desarrollador **no tiene acceso al código fuente de la clase implementada por el Desarrollador 1**. Solamente conoce la clase y puede utilizar los elementos que esta expone públicamente.

Por lo tanto, la clase de prueba debe interactuar con los objetos exclusivamente a través de los **métodos públicos definidos por la clase**.

Para cada problema, analice cuidadosamente qué información necesita mantener cada objeto y qué **métodos deberá ofrecer públicamente la clase** para que otro desarrollador pueda utilizarla correctamente sin conocer su implementación interna.

## Restricciones de implementación

Para el desarrollo de todos los ejercicios del taller se deberán cumplir las siguientes restricciones:

* Los nombres de los elementos implementados en el código fuente deberán escribirse en **inglés**. Esto incluye nombres de clases, atributos, métodos y variables.
* Los nombres utilizados deberán ser descriptivos y representar adecuadamente el elemento que modelan.
* Para cada ejercicio se deberán implementar dos clases: la clase correspondiente a la entidad del problema y su clase de prueba.
* La clase de prueba deberá nombrarse utilizando el prefijo `Test` seguido exactamente del nombre de la clase que se está probando. Por ejemplo, para la clase `Product`, la clase de prueba deberá llamarse `TestProduct`.
* Los mensajes mostrados al usuario desde las clases de prueba podrán escribirse en **español o en inglés**.
* Las clases de prueba deberán utilizar los objetos exclusivamente a través de los **métodos públicos definidos por sus clases**, considerando que el desarrollador de las pruebas no tiene acceso al código fuente de las clases que utiliza.

## Desarrollo y evaluación

El taller contiene **ocho ejercicios**, de los cuales cada estudiante deberá seleccionar y resolver **cinco**.

Cada ejercicio seleccionado tendrá una valoración máxima de **1.0**, para una calificación total máxima de **5.0**.

Los cinco ejercicios seleccionados deberán desarrollarse completamente, incluyendo tanto la clase que representa la entidad planteada como la clase de prueba correspondiente.

La selección de los ejercicios es libre. Sin embargo, cada solución deberá cumplir todas las restricciones de implementación establecidas en este taller.

Los ejercicios que no sean seleccionados no deberán implementarse.

## Ejercicio 1. Thermometer (Termómetro)

Se requiere representar un termómetro digital que mantiene la temperatura actual (temperature) expresada en grados Celsius. El dispositivo solamente puede registrar temperaturas entre **-50 °C y 100 °C**.

La temperatura puede ser consultada en cualquier momento. Cuando se intenta registrar una nueva temperatura, el dispositivo debe verificar que se encuentre dentro del rango permitido. Si el valor no es válido, la temperatura almacenada debe conservarse sin modificaciones.

Un segundo desarrollador deberá construir un programa que utilice el termómetro para registrar diferentes temperaturas y consultar la temperatura almacenada. Este desarrollador deberá poder determinar si cada intento de modificación fue aceptado o rechazado.

Pruebe la solución utilizando valores dentro y fuera del rango permitido.

## Ejercicio 2. Product (Producto)

Una tienda necesita representar los productos disponibles para la venta. De cada producto interesa conocer su nombre (name), precio (price) y cantidad disponible (stock).

El nombre de un producto no puede estar vacío. Su precio debe ser mayor que cero y la cantidad disponible no puede ser negativa.

La información del producto podrá modificarse cuando los nuevos valores cumplan las restricciones establecidas. Cuando una modificación no pueda realizarse, el estado anterior del objeto deberá conservarse.

Un segundo desarrollador deberá construir un programa que permita consultar la información del producto, intentar diferentes modificaciones y determinar cuáles fueron aceptadas o rechazadas.

Pruebe la solución utilizando diferentes valores válidos e inválidos.

## Ejercicio 3. Bank Account (Cuenta bancaria)

Una aplicación bancaria necesita representar una cuenta de la cual se conoce el número de cuenta (account number), el nombre de su titular (account holder) y el saldo disponible (balance).

El número de cuenta identifica la cuenta y no debe cambiar una vez establecido.

El saldo no puede modificarse arbitrariamente. Únicamente puede aumentar mediante depósitos (deposits) y disminuir mediante retiros (withdrawals).

Un depósito solamente puede realizarse cuando el valor es mayor que cero. Un retiro solamente puede realizarse cuando el valor solicitado es mayor que cero y existe saldo suficiente.

Un segundo desarrollador deberá construir un programa que utilice la cuenta para realizar depósitos y retiros, consultar el saldo resultante y determinar si cada operación solicitada pudo realizarse correctamente. Este desarrollador no tendrá acceso a la implementación interna de la cuenta.

Pruebe, como mínimo, depósitos válidos e inválidos, un retiro válido, un retiro por un valor superior al saldo disponible y un retiro con un valor no permitido.

## Ejercicio 4. Vehicle (Vehículo)

Se necesita representar un vehículo del cual se conoce su placa (license plate), marca (brand), velocidad actual (current speed) y velocidad máxima permitida (maximum speed).

Un vehículo inicialmente se encuentra detenido. Su velocidad puede aumentar o disminuir en incrementos de **10 km/h**, pero nunca puede ser negativa ni superar su velocidad máxima.

La placa debe almacenarse utilizando letras mayúsculas. Una placa válida debe estar formada exactamente por tres letras seguidas de tres dígitos.

Por ejemplo, si se proporciona:

```text
abc123
```

la información deberá almacenarse como:

```text
ABC123
```

El programa que utiliza el objeto debe poder diferenciar entre las siguientes situaciones:

* La información fue aceptada sin modificaciones.
* La información fue aceptada, pero fue necesario realizar alguna normalización.
* La información fue rechazada.

Un segundo desarrollador deberá construir un programa que utilice el vehículo, consulte su información, intente registrar diferentes placas y realice operaciones para aumentar y disminuir su velocidad.

Pruebe diferentes escenarios, incluyendo intentos de superar la velocidad máxima y disminuir la velocidad cuando el vehículo se encuentra detenido.

## Ejercicio 5. Room Reservation (Reserva de habitación)

Un hotel necesita representar la reserva de una habitación. De cada reserva interesa conocer el nombre del huésped (guest), el número de habitación (room number), la cantidad de noches (number of nights) y el valor por noche (price per night).

El nombre del huésped no puede estar vacío, la cantidad de noches debe ser mayor que cero y el valor por noche debe ser positivo.

El costo total (total cost) de la reserva depende de la cantidad de noches y del valor establecido para cada noche.

Un segundo desarrollador deberá construir un programa que permita consultar la información de la reserva, realizar las modificaciones permitidas y consultar su costo total.

La información disponible deberá mantenerse consistente cuando cambie la cantidad de noches o el valor por noche.

Pruebe la solución modificando diferentes valores y verificando el costo total después de cada modificación.

## Ejercicio 6. Media Player (Reproductor multimedia)

Se desea representar un reproductor multimedia que mantiene el nivel actual de volumen (volume) y su estado de reproducción (playback state).

El volumen debe mantenerse entre **0 y 100**. El reproductor debe permitir aumentar o disminuir el volumen en unidades de 5, sin superar estos límites.

Además, el reproductor puede encontrarse reproduciendo (playing) o detenido (stopped). Deben existir operaciones que permitan iniciar y detener la reproducción.

Un segundo desarrollador deberá construir un programa que utilice el reproductor, consulte su estado y realice diferentes operaciones sobre este.

El programa deberá comprobar qué ocurre cuando se intenta aumentar el volumen después de alcanzar 100 o disminuirlo cuando ya se encuentra en 0.

## Ejercicio 7. Student (Estudiante)

Una institución necesita representar un estudiante mediante su código (student ID), nombre (name) y las calificaciones (grades) obtenidas en tres evaluaciones.

Cada calificación debe encontrarse entre **0.0 y 5.0**.

El código identifica al estudiante y no debe modificarse posteriormente. El nombre puede actualizarse siempre que el nuevo nombre no esté vacío.

Las calificaciones pueden modificarse individualmente, pero solamente deben aceptarse valores dentro del rango establecido.

El sistema necesita conocer en cualquier momento el promedio académico (average) del estudiante a partir de sus calificaciones actuales.

Un segundo desarrollador deberá construir un programa que permita consultar la información del estudiante, intentar modificar su nombre y sus calificaciones y consultar el promedio resultante.

Pruebe modificaciones válidas e inválidas y compruebe cómo afectan al promedio académico.

## Ejercicio 8. Electronic Wallet (Billetera electrónica)

Una aplicación necesita representar una billetera electrónica que mantiene el nombre de su propietario (owner) y el dinero disponible (balance).

Una billetera nueva inicia con saldo cero. El dinero disponible solamente puede aumentar mediante recargas (top-ups) y disminuir mediante pagos (payments).

Las recargas deben realizarse por valores positivos.

Un pago solamente puede efectuarse cuando su valor es positivo y no supera el dinero disponible. Además, por razones de seguridad, ningún pago individual puede superar los **$500.000**.

Un segundo desarrollador deberá construir un programa que utilice la billetera para realizar recargas y pagos, consultar el dinero disponible y determinar si cada operación pudo realizarse correctamente.

Pruebe diferentes situaciones, incluyendo:

* Una recarga válida.
* Una recarga con un valor no permitido.
* Un pago válido.
* Un pago superior al dinero disponible.
* Un pago superior a $500.000.
* Un pago con un valor no permitido.

Después de cada operación, compruebe que el objeto conserva un estado válido.
