# Proyecto Final — Programación Orientada a Objetos

## Objetivo general

Diseñar e implementar una aplicación orientada a objetos en Java que modele un sistema de gestión del mundo real desde la perspectiva de una aplicación de uso interno, orientada al trabajo de un empleado, operador o administrador, aplicando correctamente los principios de abstracción, encapsulamiento, herencia y polimorfismo, junto con el manejo de colecciones y persistencia de objetos mediante archivos serializados.

---
## Requisitos del proyecto

### Requisitos técnicos

1. El proyecto debe desarrollarse utilizando Java 25 LTS (OpenJDK 25).

2. El código debe compilar y ejecutarse correctamente desde Visual Studio Code (VS Code) o desde la consola.

3. No se permite el uso de bases de datos, frameworks ni librerías externas.

4. El proyecto debe manejar los objetos en memoria usando únicamente una de las siguientes colecciones:

   * `ArrayList<T>`
   * `LinkedList<T>`

### Requisitos de arquitectura y diseño orientado a objetos

1. La estructura mínima de paquetes será:

   ```
   ui/       → interfaz de usuario (consola o Swing)
   domain/   → clases del modelo (entidades, lógica de negocio)
   data/     → clases para persistencia e intercambio de datos
   ```

2. Cada proyecto debe incluir como mínimo 9 clases pertenecientes a la capa `domain`, relacionadas con el modelo y la lógica de negocio del sistema. Estas clases deben participar activamente en el funcionamiento de la aplicación y mantener relaciones coherentes entre sí.

   No se tendrán en cuenta clases utilitarias, clases de interfaz (`ui`), clases de persistencia (`data`) ni excepciones personalizadas para cumplir este requisito mínimo.

3. El proyecto debe implementar al menos una jerarquía de herencia entre clases de la capa `domain`, justificada por una relación de especialización (“es un”) y por los comportamientos del sistema. Debe demostrar polimorfismo mediante la invocación de métodos sobrescritos a través de referencias del tipo base; no basta con declarar `extends`. No se exige una jerarquía específica ni el uso de clases o métodos abstractos: estos deben utilizarse únicamente cuando el diseño lo justifique.

4. Las clases del dominio deben incluir constructores, métodos accesores, métodos mutadores y métodos adicionales de negocio, de acuerdo con sus responsabilidades:

   * Los constructores deben inicializar los objetos en un estado válido y recibir los datos necesarios para su creación.
   * Los accesores (`get...` y `is...`, según corresponda) deben permitir consultar la información que sea necesario exponer, preservando el encapsulamiento.
   * Los mutadores (`set...` u operaciones específicas de modificación) deben validar los cambios y mantener las reglas del negocio. No se deben crear mutadores para atributos que no deban modificarse ni permitir cambios que produzcan estados inválidos.
   * Los métodos adicionales deben implementar comportamientos propios del dominio, como cálculos, validaciones, cambios de estado o gestión de relaciones. El modelo no debe limitarse a almacenar atributos con getters y setters.

   No se exige un accesor y un mutador para cada atributo ni todas las categorías de métodos en cada clase; su inclusión debe responder al diseño y a las responsabilidades de cada clase.

### Requisitos funcionales y reglas del negocio

1. Enfoque del sistema:
    El proyecto debe desarrollarse como una aplicación de uso interno, orientada al personal del sistema (empleado, operador o administrador).
    No debe plantearse como una aplicación para el cliente final ni como un sistema de autoservicio.

2. Se deben implementar funciones de registro, búsqueda, listado, modificación y eliminación (CRUD) para las entidades administrables del sistema, de acuerdo con las reglas del negocio. No se exige permitir todas estas operaciones sobre cada clase del dominio.

   * Las modificaciones y eliminaciones deben preservar la consistencia de los datos y sus relaciones; no se deben dejar referencias a objetos eliminados ni permitir estados inválidos.
   * Cuando un objeto esté asociado a operaciones o registros históricos, se debe restringir su eliminación o utilizar desactivación, cancelación o anulación, según corresponda, conservando la información necesaria.
   * Los registros históricos, como ventas, pagos o alquileres, no deben modificarse ni eliminarse libremente. Las correcciones deben seguir las reglas del negocio y conservar la trazabilidad.
   * Cada equipo debe documentar en el `README.md` las entidades que permiten CRUD, las restricciones aplicadas y las alternativas utilizadas cuando una operación no corresponda.

3. El sistema debe incluir un componente básico de apoyo a decisiones que realice una tarea de recomendación, clasificación o predicción mediante reglas o algoritmos implementados sin librerías externas. Debe utilizar los datos del sistema y estar disponible desde la interfaz de usuario.

### Requisitos de interfaz de usuario

1. La interacción con el usuario debe organizarse mediante una o varias clases de la capa `ui`, responsables de recibir los datos ingresados y presentar información, resultados y mensajes. Estas clases deben gestionar la entrada y salida de datos de acuerdo con la interfaz elegida (consola o Swing), manteniendo separada la interacción con el usuario de la lógica de negocio y la persistencia. Los nombres de las clases y sus métodos serán definidos por cada equipo según su diseño.

2. La interfaz de usuario puede implementarse de una de las siguientes maneras:
    a) mediante un menú de texto en consola (requisito mínimo obligatorio), o
    b) mediante una interfaz gráfica desarrollada con Java Swing, la cual puede reemplazar completamente la interfaz en consola, siempre que:

    * mantenga la arquitectura por capas (`ui`, `domain`, `data`),
    * implemente todas las funcionalidades requeridas, y
    * permita guardar y cargar datos correctamente.

### Requisitos de persistencia e intercambio de datos

1. Persistencia de datos (obligatoria):
   El sistema debe guardar y cargar la información utilizando archivos serializados mediante `ObjectOutputStream` y `ObjectInputStream`.
   Este mecanismo corresponde a la persistencia principal del sistema y debe permitir conservar el estado completo de la aplicación entre ejecuciones.

2. Exportación de datos a CSV (obligatoria) e importación (opcional):

    * El sistema debe permitir exportar datos del sistema o reportes a archivos `.csv` desde la interfaz de usuario. El archivo debe incluir encabezados de columnas y los datos correspondientes, utilizando una estructura tabular coherente.
    * La importación de datos desde archivos `.csv` es opcional y puede utilizarse para la carga inicial de información.

    La exportación y la importación son independientes de la persistencia principal mediante archivos serializados y no la reemplazan. Deben implementarse sin librerías externas.

### Requisitos de estilo y documentación del código

1. El código fuente debe escribirse completamente en inglés, incluyendo nombres de variables, métodos, clases y comentarios.

2. Se deben aplicar las convenciones oficiales de estilo de Java:
   * UpperCamelCase para nombres de clases (por ejemplo, `StudentRecord`, `ParkingSystem`).
   * camelCase para nombres de variables y métodos (por ejemplo, `studentName`, `calculateTotal`).
   * UPPER_SNAKE_CASE para constantes (por ejemplo, `MAX_SIZE`, `DEFAULT_PATH`).

3. Todo el código debe incluir comentarios en inglés que expliquen el propósito de las clases y métodos.

### Condiciones de trabajo, repositorio y documentación de entrega

1. El proyecto puede desarrollarse de forma individual o, de manera opcional, en un grupo de hasta 2 estudiantes.

2. El proyecto debe subirse a un repositorio en GitHub cumpliendo las siguientes condiciones:

    * El repositorio debe ser público.
    * Nombre del repositorio:
      ```
      POO_FinalProject_Lastname1_Lastname2
      ```
      Para entregas individuales, utilizar `POO_FinalProject_Lastname1`.
    * Debe contener:

      * Carpeta `src/` con todo el código fuente.
      * Archivo `README.md` con:
        * Título del proyecto.
        * Integrantes (nombres y códigos).
        * Descripción general del sistema.
        * Instrucciones para ejecutar.
        * Ejemplo de entrada/salida.
        * Diagrama de clases incluido directamente en el `README.md` mediante un bloque de código `mermaid` de tipo `classDiagram`. Debe representar las clases del dominio, sus atributos y métodos relevantes, las relaciones de herencia, asociación y composición que correspondan, y las multiplicidades aplicables. El diagrama debe ser coherente con el código implementado.
      * Al menos 5 commits significativos. En trabajos de dos estudiantes, deben existir commits significativos de ambos desarrolladores en el historial del repositorio, identificados con sus respectivas cuentas de GitHub. No se aceptará que todos los commits correspondan a un solo integrante. En trabajos individuales, los commits corresponden al único autor.

---
## Criterios de evaluación

- **Proyecto entregado: 40%.**
- **Sustentación compartida: 30%.**
- **Sustentación individual: 30%.**

En trabajos en pareja, las notas del proyecto entregado y de la sustentación compartida serán comunes a ambos integrantes; la sustentación individual se calificará por separado para cada estudiante. En trabajos individuales, el único autor realizará ambos componentes de la sustentación y conservará los mismos porcentajes.

La rúbrica detallada de cada componente se definirá posteriormente.

---
## Propuestas de proyectos

Cada estudiante o grupo de dos estudiantes deberá seleccionar una de las siguientes opciones (previa aprobación del docente).

La clase central del dominio sugerida en cada propuesta es un punto de partida para el análisis; no corresponde necesariamente a la clase que contiene el método `main` ni prescribe el diseño completo. Cada equipo debe identificar las demás clases, distribuir sus responsabilidades y definir sus relaciones, evitando concentrar toda la lógica del sistema en una sola clase.

---
### 1. Smart Parking System

Aplicación para el personal de un parqueadero que necesita conocer la ocupación durante la jornada y cobrar al finalizar cada estancia. El sistema vincula cada ingreso con su salida para que el operador pueda consultar los cupos disponibles y revisar la actividad del parqueadero.

Clase central del dominio sugerida: `ParkingLot`.

[Tareas del sistema](Proposals/01-smart-parking-system.md)

---
### 2. ~~Hotel Management System~~

Aplicación para el personal de recepción y administración de un hotel. Reúne la información de huéspedes, habitaciones, reservas y pagos para que recepción pueda planificar las llegadas y salidas, confirmar la disponibilidad por fechas y dar seguimiento a la ocupación.

Clase central del dominio sugerida: `Hotel`.

[Tareas del sistema](Proposals/02-hotel-management-system.md)

---
### 3. Video Game Store

Aplicación para los empleados de una tienda de videojuegos que relaciona el catálogo, el inventario y las ventas. Permite al personal responder consultas sobre títulos disponibles y revisar qué productos se venden y qué ingresos generan.

Clase central del dominio sugerida: `Store`.

[Tareas del sistema](Proposals/03-video-game-store.md)

---
### 4. Veterinary Clinic System

Aplicación para el personal de una clínica veterinaria que organiza la atención desde la programación de citas hasta la consulta del historial de cada mascota. Reúne la información de propietarios, veterinarios y tratamientos registrados para facilitar la coordinación entre recepción y el personal clínico.

Clase central del dominio sugerida: `VeterinaryClinic`.

[Tareas del sistema](Proposals/04-veterinary-clinic-system.md)

---
### 5. Movie Rental System

Aplicación para los empleados de un negocio de alquiler de películas que permite distinguir el catálogo de los ejemplares físicamente disponibles. El personal puede seguir cada préstamo desde su entrega hasta la devolución y consultar la fecha prevista de regreso y el valor del alquiler.

Clase central del dominio sugerida: `Store`.

[Tareas del sistema](Proposals/05-movie-rental-system.md)

---
### 6. Event Ticketing System

Aplicación para el personal que organiza eventos y atiende la venta de entradas. Relaciona los eventos con sus sedes y registra las ventas para que la taquilla pueda informar cuántas entradas quedan y operar dentro del aforo previsto.

Clase central del dominio sugerida: `TicketOffice`.

[Tareas del sistema](Proposals/06-event-ticketing-system.md)

---
### 7. Restaurant Order Management

Aplicación para el personal de un restaurante que organiza la atención por mesas. Relaciona los pedidos con el menú y permite seguir su avance hasta el cierre de la cuenta, de modo que el personal pueda consultar qué mesas están ocupadas y qué pedidos siguen abiertos.

Clase central del dominio sugerida: `Restaurant`.

[Tareas del sistema](Proposals/07-restaurant-order-management.md)

---
### 8. Delivery Service System

Aplicación para el personal que coordina un servicio de domicilios. Reúne los pedidos y la disponibilidad de los repartidores para facilitar la asignación de entregas, consultar su avance y calcular el costo del servicio.

Clase central del dominio sugerida: `DeliveryService`.

[Tareas del sistema](Proposals/08-delivery-service-system.md)

---
### 9. Gym Membership Management System

Aplicación para el personal de un gimnasio que administra la relación entre los miembros y los planes contratados. Facilita el seguimiento de renovaciones y pagos, la comprobación de la vigencia al momento del ingreso y la consulta de entrenadores asignados.

Clase central del dominio sugerida: `Gym`.

[Tareas del sistema](Proposals/09-gym-membership-management-system.md)

---
### 10. Pharmacy Inventory System

Aplicación para el personal de una farmacia que reúne los datos de medicamentos, proveedores y movimientos de inventario. Permite consultar existencias al atender una venta y revisar las entradas y salidas de productos para orientar la reposición.

Clase central del dominio sugerida: `Pharmacy`.

[Tareas del sistema](Proposals/10-pharmacy-inventory-system.md)

---
### 11. Clothing Store Management System

Aplicación para el personal de una tienda de ropa que distingue cada artículo de sus variantes por talla y color. Relaciona el catálogo, las existencias y las ventas para que el personal pueda confirmar la disponibilidad de una variante concreta y revisar su movimiento.

Clase central del dominio sugerida: `ClothingStore`.

[Tareas del sistema](Proposals/11-clothing-store-management-system.md)

---
## Entrega final

* Subir al repositorio GitHub el proyecto completo y funcional.
* Incluir en el `README.md` la explicación del proyecto y el diagrama de clases en Mermaid (`classDiagram`), actualizado y coherente con la implementación.
