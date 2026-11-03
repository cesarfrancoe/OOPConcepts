# Proyecto Final — Programación Orientada a Objetos

## Objetivo general

Diseñar e implementar una aplicación orientada a objetos en Java que modele un sistema de gestión del mundo real desde la perspectiva de una aplicación de uso interno, orientada al trabajo de un empleado, operador o administrador, aplicando correctamente los principios de abstracción, encapsulamiento, herencia y polimorfismo, junto con el manejo de colecciones y persistencia de objetos mediante archivos serializados.

---
## Requisitos generales

1. El proyecto debe desarrollarse utilizando Java 25 LTS (OpenJDK 25).

2. El proyecto puede desarrollarse de forma individual o, de manera opcional, en un grupo de hasta 2 estudiantes.

3. El código fuente debe escribirse completamente en inglés, incluyendo nombres de variables, métodos, clases y comentarios.

4. Se deben aplicar las convenciones oficiales de estilo de Java:
   * UpperCamelCase para nombres de clases (por ejemplo, `StudentRecord`, `ParkingSystem`).
   * camelCase para nombres de variables y métodos (por ejemplo, `studentName`, `calculateTotal`).
   * UPPER_SNAKE_CASE para constantes (por ejemplo, `MAX_SIZE`, `DEFAULT_PATH`).

5. La estructura mínima de paquetes será:

   ```
   ui/       → interfaz de usuario (consola o Swing)
   domain/   → clases del modelo (entidades, lógica de negocio)
   data/     → clases para persistencia e intercambio de datos
   ```
6. La interacción con el usuario debe organizarse mediante una o varias clases de la capa `ui`, responsables de recibir los datos ingresados y presentar información, resultados y mensajes. Estas clases deben gestionar la entrada y salida de datos de acuerdo con la interfaz elegida (consola o Swing), manteniendo separada la interacción con el usuario de la lógica de negocio y la persistencia. Los nombres de las clases y sus métodos serán definidos por cada equipo según su diseño.

7. Persistencia de datos (obligatoria):
   El sistema debe guardar y cargar la información utilizando archivos serializados mediante `ObjectOutputStream` y `ObjectInputStream`.
   Este mecanismo corresponde a la persistencia principal del sistema y debe permitir conservar el estado completo de la aplicación entre ejecuciones.

8. El proyecto debe manejar los objetos en memoria usando únicamente una de las siguientes colecciones:

   * `ArrayList<T>`
   * `LinkedList<T>`
9. Se deben implementar funciones de registro, búsqueda, listado, modificación y eliminación (CRUD) para las entidades administrables del sistema, de acuerdo con las reglas del negocio. No se exige permitir todas estas operaciones sobre cada clase del dominio.

   * Las modificaciones y eliminaciones deben preservar la consistencia de los datos y sus relaciones; no se deben dejar referencias a objetos eliminados ni permitir estados inválidos.
   * Cuando un objeto esté asociado a operaciones o registros históricos, se debe restringir su eliminación o utilizar desactivación, cancelación o anulación, según corresponda, conservando la información necesaria.
   * Los registros históricos, como ventas, pagos o alquileres, no deben modificarse ni eliminarse libremente. Las correcciones deben seguir las reglas del negocio y conservar la trazabilidad.
   * Cada equipo debe documentar en el `README.md` las entidades que permiten CRUD, las restricciones aplicadas y las alternativas utilizadas cuando una operación no corresponda.

10. Exportación de datos a CSV (obligatoria) e importación (opcional):

    * El sistema debe permitir exportar datos del sistema o reportes a archivos `.csv` desde la interfaz de usuario. El archivo debe incluir encabezados de columnas y los datos correspondientes, utilizando una estructura tabular coherente.
    * La importación de datos desde archivos `.csv` es opcional y puede utilizarse para la carga inicial de información.

    La exportación y la importación son independientes de la persistencia principal mediante archivos serializados y no la reemplazan. Deben implementarse sin librerías externas.

11. La interfaz de usuario puede implementarse de una de las siguientes maneras:
    a) mediante un menú de texto en consola (requisito mínimo obligatorio), o
    b) mediante una interfaz gráfica desarrollada con Java Swing, la cual puede reemplazar completamente la interfaz en consola, siempre que:

    * mantenga la arquitectura por capas (`ui`, `domain`, `data`),
    * implemente todas las funcionalidades requeridas, y
    * permita guardar y cargar datos correctamente.
12. Enfoque del sistema:
    El proyecto debe desarrollarse como una aplicación de uso interno, orientada al personal del sistema (empleado, operador o administrador).
    No debe plantearse como una aplicación para el cliente final ni como un sistema de autoservicio.

13. El proyecto debe subirse a un repositorio en GitHub cumpliendo las siguientes condiciones:

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

14. El código debe compilar y ejecutarse correctamente desde Visual Studio Code (VS Code) o desde la consola.
15. No se permite el uso de bases de datos, frameworks ni librerías externas.

16. Todo el código debe incluir comentarios en inglés que expliquen el propósito de las clases y métodos.

17. El sistema debe incluir un componente básico de apoyo a decisiones que realice una tarea de recomendación, clasificación o predicción mediante reglas o algoritmos implementados sin librerías externas. Debe utilizar los datos del sistema y estar disponible desde la interfaz de usuario.

18. El proyecto debe implementar al menos una jerarquía de herencia entre clases de la capa `domain`, justificada por una relación de especialización (“es un”) y por los comportamientos del sistema. Debe demostrar polimorfismo mediante la invocación de métodos sobrescritos a través de referencias del tipo base; no basta con declarar `extends`. No se exige una jerarquía específica ni el uso de clases o métodos abstractos: estos deben utilizarse únicamente cuando el diseño lo justifique.

19. Las clases del dominio deben incluir constructores, métodos accesores, métodos mutadores y métodos adicionales de negocio, de acuerdo con sus responsabilidades:

   * Los constructores deben inicializar los objetos en un estado válido y recibir los datos necesarios para su creación.
   * Los accesores (`get...` y `is...`, según corresponda) deben permitir consultar la información que sea necesario exponer, preservando el encapsulamiento.
   * Los mutadores (`set...` u operaciones específicas de modificación) deben validar los cambios y mantener las reglas del negocio. No se deben crear mutadores para atributos que no deban modificarse ni permitir cambios que produzcan estados inválidos.
   * Los métodos adicionales deben implementar comportamientos propios del dominio, como cálculos, validaciones, cambios de estado o gestión de relaciones. El modelo no debe limitarse a almacenar atributos con getters y setters.

   No se exige un accesor y un mutador para cada atributo ni todas las categorías de métodos en cada clase; su inclusión debe responder al diseño y a las responsabilidades de cada clase.

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

Todos los proyectos deben enfocarse en procesos administrativos u operativos internos y no en aplicaciones orientadas al cliente final.
Además, cada proyecto debe incluir como mínimo 6 clases pertenecientes a la capa `domain`, relacionadas con el modelo y la lógica de negocio del sistema. Estas clases deben participar activamente en el funcionamiento de la aplicación y mantener relaciones coherentes entre sí.

No se tendrán en cuenta clases utilitarias, clases de interfaz (`ui`), clases de persistencia (`data`) ni excepciones personalizadas para cumplir este requisito mínimo.

La clase central del dominio sugerida en cada propuesta es un punto de partida para el análisis; no corresponde necesariamente a la clase que contiene el método `main` ni prescribe el diseño completo. Cada equipo debe identificar las demás clases, distribuir sus responsabilidades y definir sus relaciones, evitando concentrar toda la lógica del sistema en una sola clase.

---
### 1. Smart Parking System

Sistema utilizado por el personal de un parqueadero para registrar la entrada y salida de vehículos, controlar la ocupación y calcular el valor a pagar.

Clase central del dominio sugerida: `ParkingLot`.

Funciones clave:

* Registro de ingreso y salida de vehículos.
* Cálculo automático de tarifas.
* Consulta de cupos disponibles.
* Control de ocupación del parqueadero.
* Generación de reportes básicos.

---
### 2. ~~Hotel Management System~~

Sistema utilizado por el personal de recepción o administración para gestionar habitaciones, huéspedes y reservas.

Clase central del dominio sugerida: `Hotel`.

Funciones clave:

* Registro de huéspedes y habitaciones.
* Gestión de reservas.
* Registro de pagos.
* Consulta de disponibilidad.
* Control de ocupación.
* Generación de reportes básicos.

---
### 3. Video Game Store

Sistema utilizado por empleados de una tienda para gestionar el inventario de videojuegos y registrar ventas.

Clase central del dominio sugerida: `Store`.

Funciones clave:

* Registro de videojuegos.
* Clasificación por categorías.
* Registro de ventas.
* Consulta de inventario.
* Cálculo de ingresos.
* Generación de reportes básicos.

---
### 4. Veterinary Clinic System

Sistema utilizado por el personal de una clínica veterinaria para gestionar mascotas, dueños y citas.

Clase central del dominio sugerida: `VeterinaryClinic`.

Funciones clave:

* Registro de mascotas y propietarios.
* Agendamiento de citas.
* Registro de tratamientos.
* Consulta de historial médico.
* Gestión de veterinarios.
* Generación de reportes básicos.

---
### 5. Movie Rental System

Sistema utilizado por empleados para gestionar el alquiler y devolución de películas.

Clase central del dominio sugerida: `Store`.

Funciones clave:

* Registro de películas.
* Gestión de alquileres y devoluciones.
* Consulta de disponibilidad.
* Clasificación por categorías.
* Cálculo de tarifas.
* Generación de reportes básicos.

---
### 6. Event Ticketing System

Sistema utilizado por el personal organizador para gestionar eventos y la venta de entradas.

Clase central del dominio sugerida: `TicketOffice`.

Funciones clave:

* Registro de eventos.
* Venta de entradas.
* Control de aforo.
* Gestión de escenarios o sedes.
* Consulta de disponibilidad.
* Generación de reportes básicos.

---
### 7. Restaurant Order Management

Sistema utilizado por el personal de un restaurante para registrar pedidos, calcular cuentas y gestionar mesas.

Clase central del dominio sugerida: `Restaurant`.

Funciones clave:

* Registro de pedidos.
* Gestión de mesas.
* Cálculo de cuentas.
* Consulta de órdenes activas.
* Administración del menú.
* Generación de reportes básicos.

---
### 8. Delivery Service System

Sistema utilizado por el personal de un servicio de domicilios para registrar pedidos y asignar repartidores.

Clase central del dominio sugerida: `DeliveryService`.

Funciones clave:

* Registro de pedidos.
* Gestión de repartidores.
* Asignación de entregas.
* Seguimiento de estados.
* Cálculo de costos.
* Generación de reportes básicos.

---
### 9. Gym Membership Management System

Sistema utilizado por el personal de un gimnasio para gestionar miembros, planes, pagos y control de acceso.

Clase central del dominio sugerida: `Gym`.

Funciones clave:

* Registro de miembros.
* Gestión de planes de membresía.
* Registro de pagos.
* Control de acceso al gimnasio.
* Asignación de entrenadores.
* Generación de reportes básicos.

---
### 10. Pharmacy Inventory System

Sistema utilizado por el personal de una farmacia para gestionar medicamentos, proveedores y ventas.

Clase central del dominio sugerida: `Pharmacy`.

Funciones clave:

* Registro de medicamentos.
* Control de inventario.
* Gestión de proveedores.
* Registro de ventas.
* Consulta de disponibilidad.
* Generación de reportes básicos.

---
### 11. Clothing Store Management System

Sistema utilizado por el personal de una tienda de ropa para administrar artículos de vestir, controlar el inventario y registrar ventas, considerando características como tallas, colores, categorías y precios.

Clase central del dominio sugerida: `ClothingStore`.

Funciones clave:

* Registro de artículos de vestir.
* Clasificación de artículos por categorías.
* Gestión de tallas y colores disponibles.
* Control de inventario por talla y color.
* Registro de ventas y actualización de existencias.
* Consulta de disponibilidad de artículos.
* Generación de reportes básicos.

---
## Entrega final

* Subir al repositorio GitHub el proyecto completo y funcional.
* Incluir en el `README.md` la explicación del proyecto y el diagrama de clases en Mermaid (`classDiagram`), actualizado y coherente con la implementación.
