# Proyecto Final — Programación Orientada a Objetos

## Objetivo general

Diseñar e implementar una aplicación orientada a objetos en Java que modele un sistema de gestión del mundo real desde la perspectiva de una aplicación de uso interno, orientada al trabajo de un empleado, operador o administrador, aplicando correctamente los principios de abstracción, encapsulamiento, herencia y polimorfismo, junto con el manejo de colecciones y persistencia de objetos mediante archivos serializados.

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
   data/     → clases para persistencia e intercambio de datos
   ```

6. Si la interfaz de usuario es por consola, debe incluir una clase auxiliar llamada `Console` con los métodos:

   ```java
   public static void writeLine(Object message)
   public static String readLine(String prompt)
   ```

   Si la interfaz se desarrolla con Swing, esta clase no es necesaria.

7. Persistencia de datos (obligatoria):
   El sistema debe guardar y cargar la información utilizando archivos serializados mediante `ObjectOutputStream` y `ObjectInputStream`.
   Este mecanismo corresponde a la persistencia principal del sistema y debe permitir conservar el estado completo de la aplicación entre ejecuciones.

8. El proyecto debe manejar los objetos en memoria usando únicamente una de las siguientes colecciones:

   * `ArrayList<T>`
   * `LinkedList<T>`

9. Se deben implementar funciones de registro, búsqueda, listado, modificación y eliminación de objetos.

10. Importación y exportación de datos (opcional):
    El sistema podrá incluir funcionalidades para:

    * importar datos desde archivos `.csv`,
    * exportar datos del sistema a archivos `.csv`.

    Estas funcionalidades son independientes del mecanismo de persistencia y se utilizarán para carga inicial de datos o generación de reportes.

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
    * Debe contener:

      * Carpeta `src/` con todo el código fuente.
      * Archivo `README.md` con:

        * Título del proyecto.
        * Integrantes (nombres y códigos).
        * Descripción general del sistema.
        * Instrucciones para ejecutar.
        * Ejemplo de entrada/salida.
        * Enlace al diagrama de clases (`ModelDiagram.gif`).
      * Archivo `ModelDiagram.gif` en la raíz del repositorio.
      * Al menos 5 commits significativos distribuidos entre los dos miembros.

14. El código debe compilar y ejecutarse correctamente desde Visual Studio Code (VS Code) o desde la consola.

15. No se permite el uso de bases de datos, frameworks ni librerías externas.

16. Todo el código debe incluir comentarios en inglés que expliquen el propósito de las clases y métodos.

17. El sistema debe incluir un componente básico de IA orientado a una de las siguientes tareas: recomendación, clasificación o predicción, implementado sin librerías externas. Este componente debe integrarse con los datos del sistema y exponerse desde la interfaz de usuario.

---

## Criterios de evaluación (100%)

| Criterio                                                                                                                                                                                        | Peso |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- |
| Diseño orientado a objetos (herencia, composición, polimorfismo)                                                                                                                                | 20%  |
| Organización del código y estructura por paquetes                                                                                                                                               | 10%  |
| Convenciones de escritura y documentación en inglés                                                                                                                                             | 10%  |
| Uso correcto de ArrayList o LinkedList                                                                                                                                                          | 10%  |
| Persistencia mediante archivos serializados                                                                                                                                                     | 15%  |
| Interfaz de usuario (consola o Swing): usabilidad, flujo, validaciones, manejo de errores                                                                                                       | 10%  |
| Uso de GitHub (commits, README, diagrama de clases)                                                                                                                                             | 10%  |
| Extensiones opcionales (por ejemplo: importación/exportación `.csv`, componente básico de IA, búsquedas o filtrados avanzados, reportes, `Comparable`/`Comparator`, excepciones personalizadas) | 15%  |

Nota: la interfaz de usuario se evalúa únicamente en el criterio correspondiente. La implementación con Swing no otorga puntaje adicional por sí misma.

---

## Propuestas de proyectos

Cada pareja deberá seleccionar una de las siguientes opciones (previa aprobación del docente).

Todos los proyectos deben enfocarse en procesos administrativos u operativos internos y no en aplicaciones orientadas al cliente final.

Además, cada proyecto debe incluir como mínimo 6 clases pertenecientes a la capa `domain`, relacionadas con el modelo y la lógica de negocio del sistema. Estas clases deben participar activamente en el funcionamiento de la aplicación y mantener relaciones coherentes entre sí.

No se tendrán en cuenta clases utilitarias, clases de interfaz (`ui`), clases de persistencia (`data`) ni excepciones personalizadas para cumplir este requisito mínimo.

---

### 1. Smart Parking System

Sistema utilizado por el personal de un parqueadero para registrar la entrada y salida de vehículos, controlar la ocupación y calcular el valor a pagar.

Clases sugeridas:
`Vehicle`, `Car`, `Motorcycle`, `ParkingSpot`, `Ticket`, `ParkingLot`.

Funciones clave:

* Registro de ingreso y salida de vehículos.
* Cálculo automático de tarifas.
* Consulta de cupos disponibles.
* Control de ocupación del parqueadero.
* Generación de reportes básicos.

---

### 2. Hotel Management System

Sistema utilizado por el personal de recepción o administración para gestionar habitaciones, huéspedes y reservas.

Clases sugeridas:
`Room`, `Guest`, `Reservation`, `Employee`, `Payment`, `Hotel`.

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

Clases sugeridas:
`VideoGame`, `Category`, `Customer`, `Sale`, `Employee`, `Store`.

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

Clases sugeridas:
`Pet`, `Owner`, `Appointment`, `Veterinarian`, `Treatment`, `VeterinaryClinic`.

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

Clases sugeridas:
`Movie`, `Category`, `Customer`, `Rental`, `Employee`, `Store`.

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

Clases sugeridas:
`Event`, `Customer`, `Ticket`, `Venue`, `Employee`, `TicketOffice`.

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

Clases sugeridas:
`MenuItem`, `Order`, `Customer`, `Table`, `Employee`, `Restaurant`.

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

Clases sugeridas:
`Customer`, `DeliveryPerson`, `Order`, `Product`, `Vehicle`, `DeliveryService`.

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

Clases sugeridas:
`Member`, `MembershipPlan`, `Payment`, `Trainer`, `AccessRecord`, `Gym`.

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

Clases sugeridas:
`Medicine`, `Category`, `Supplier`, `Sale`, `Employee`, `Pharmacy`.

Funciones clave:

* Registro de medicamentos.
* Control de inventario.
* Gestión de proveedores.
* Registro de ventas.
* Consulta de disponibilidad.
* Generación de reportes básicos.













---

## Entrega final

* Subir al repositorio GitHub el proyecto completo y funcional.
* Incluir en el `README.md` la explicación del proyecto y el enlace al archivo `ModelDiagram.gif`.

