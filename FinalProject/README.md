# Proyecto Final — Programación Orientada a Objetos

## Objetivo general

Diseñar e implementar una aplicación orientada a objetos en Java que simule un sistema del mundo real, aplicando correctamente los principios de abstracción, encapsulamiento, herencia y polimorfismo, junto con el manejo de colecciones y persistencia de objetos mediante archivos serializados.

---

## Requisitos generales

1. El proyecto debe desarrollarse en Java 17 o Java 21 (solo versiones LTS).
2. Trabajo en parejas (máximo 2 estudiantes).
3. El código fuente debe escribirse completamente en inglés, incluyendo nombres de variables, métodos, clases y comentarios.
4. Se deben aplicar las convenciones oficiales de estilo de Java:

   * UpperCamelCase para nombres de clases (por ejemplo, `StudentRecord`, `ParkingSystem`).
   * camelCase para nombres de variables y métodos (por ejemplo, `studentName`, `calculateTotal`).
   * UPPER_SNAKE_CASE para constantes (por ejemplo, `MAX_SIZE`, `DEFAULT_PATH`).
5. La estructura mínima de paquetes será:

   ```
   ui/       → interfaz de usuario (consola o Swing)
   domain/   → clases del modelo (entidades, lógica de negocio)
   data/     → clases para lectura/escritura de archivos serializados y archivos .csv
   ```
6. Si la interfaz de usuario es por consola, debe incluir una clase auxiliar llamada `Console` con los métodos:

   ```java
   public static void writeLine(Object message)
   public static String readLine(String prompt)
   ```

   Si la interfaz se desarrolla con Swing, esta clase no es necesaria.
7. El almacenamiento de datos debe realizarse en archivos serializados, utilizando `ObjectOutputStream` y `ObjectInputStream`.
8. El proyecto debe manejar los objetos en memoria usando únicamente una de las siguientes colecciones:

   * `ArrayList<T>`
   * `LinkedList<T>`
9. Se deben implementar funciones de registro, búsqueda, listado, modificación y eliminación de objetos.
10. El sistema debe permitir, de forma opcional, importar datos desde tablas en archivos `.csv`.
11. La interfaz de usuario puede implementarse de una de las siguientes maneras:
    a) mediante un menú de texto en consola (requisito mínimo obligatorio), o
    b) mediante una interfaz gráfica desarrollada con Java Swing, la cual puede reemplazar completamente la interfaz en consola, siempre que:

    * mantenga la arquitectura por capas (`ui`, `domain`, `data`),
    * implemente todas las funcionalidades requeridas, y
    * permita guardar y cargar datos correctamente.
12. El proyecto debe subirse a un repositorio en GitHub cumpliendo las siguientes condiciones:

    * El repositorio debe ser público.
    * Nombre del repositorio:

      ```
      POO_FinalProject_Lastname1_Lastname2
      ```
    * Debe contener:

      * Carpeta `src/` con todo el código fuente.
      * Archivo `README.md` con:

        * Título del proyecto.
        * Integrantes (nombres y códigos).
        * Descripción general del sistema (objetivo, alcance y breve explicación del funcionamiento).
        * Instrucciones para ejecutar el programa.
        * Ejemplo de entrada/salida.
        * Enlace al diagrama de clases del modelo de datos (`ModelDiagram.gif`) ubicado en la raíz del repositorio.
      * Archivo `ModelDiagram.gif` en la raíz del repositorio.
      * Al menos 5 commits significativos distribuidos entre los dos miembros.
13. El código debe compilar y ejecutarse correctamente desde Visual Studio Code (VS Code) o desde la consola.
14. No se permite el uso de bases de datos, frameworks ni librerías externas.
15. Todo el código debe incluir comentarios en inglés que expliquen el propósito de las clases y métodos.

---

## Criterios de evaluación (100%)

| Criterio                                                                                                                                                                                                                                                          | Peso |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- |
| Diseño orientado a objetos (herencia, composición, polimorfismo)                                                                                                                                                                                                  | 20%  |
| Organización del código y estructura por paquetes                                                                                                                                                                                                                 | 10%  |
| Convenciones de escritura y documentación en inglés                                                                                                                                                                                                               | 10%  |
| Uso correcto de ArrayList o LinkedList                                                                                                                                                                                                                            | 10%  |
| Persistencia mediante archivos serializados                                                                                                                                                                                                                       | 15%  |
| Interfaz de usuario (consola o Swing): usabilidad, flujo, validaciones, manejo de errores                                                                                                                                                                         | 10%  |
| Uso de GitHub (commits, README, diagrama de clases)                                                                                                                                                                                                               | 10%  |
| Extensiones opcionales no relacionadas con UI (por ejemplo: importación desde .csv, búsquedas/filtrados avanzados, reportes, `Comparable`/`Comparator`, excepciones personalizadas, pruebas unitarias, logging, empaquetado ejecutable, archivo de configuración) | 15%  |

Nota: implementar Swing no otorga puntos adicionales en el criterio 8; la UI (ya sea consola o Swing) se evalúa exclusivamente en el criterio 6.

---

## Propuestas de proyectos

Cada pareja deberá seleccionar una de las siguientes opciones (previa aprobación del docente).

### 1. Smart Parking System

Simula un sistema para administrar un parqueadero inteligente, controlando vehículos, plazas disponibles y tarifas por tipo de vehículo.
Clases sugeridas: `Vehicle`, `Car`, `Motorcycle`, `ParkingSpot`, `Ticket`, `ParkingLot`.
Funciones clave: entrada y salida de vehículos, cálculo de tarifa, búsqueda de cupos y listado de ocupación.

### 2. Hotel Management System

Administra habitaciones, huéspedes y reservas.
Clases sugeridas: `Room`, `Guest`, `Reservation`, `Hotel`.
Funciones clave: registro de habitaciones y clientes, reservas, cancelaciones y listado de disponibilidad.

### 3. Video Game Store

Registra videojuegos, clientes y ventas.
Clases sugeridas: `VideoGame`, `Customer`, `Sale`, `Store`.
Funciones clave: registro de juegos, búsqueda por género o título, registro de ventas y reporte de ingresos.

### 4. Veterinary Clinic System

Gestiona mascotas, dueños y citas médicas.
Clases sugeridas: `Pet`, `Owner`, `Appointment`, `VeterinaryClinic`.
Funciones clave: registro de dueños y mascotas, agendamiento de citas y consulta de historial médico.

### 5. Movie Rental System

Administra una tienda de alquiler de películas.
Clases sugeridas: `Movie`, `Customer`, `Rental`, `Store`.
Funciones clave: registro de películas, alquiler y devolución, cálculo de tarifas y listado de películas disponibles.

### 6. Event Ticketing System

Gestiona la venta de entradas para conciertos o eventos.
Clases sugeridas: `Event`, `Customer`, `Ticket`, `Venue`, `TicketOffice`.
Funciones clave: registro de eventos, venta de boletos, control de aforo y generación de reportes.

### 7. Restaurant Order Management

Simula el sistema de pedidos de un restaurante.
Clases sugeridas: `MenuItem`, `Order`, `Customer`, `Table`, `Restaurant`.
Funciones clave: creación de pedidos, cálculo de total, listado de órdenes activas y cierre de cuenta.

### 8. Delivery Service System

Administra pedidos y entregas de un servicio de domicilios.
Clases sugeridas: `Customer`, `DeliveryPerson`, `Order`, `Product`, `DeliveryService`.
Funciones clave: registro de clientes y repartidores, asignación de entregas, seguimiento de estado y cálculo de costos.

---

## Entrega final

* Subir al repositorio GitHub el proyecto completo y funcional.
* Incluir en el `README.md` la explicación del proyecto y el enlace al archivo `ModelDiagram.gif`.

