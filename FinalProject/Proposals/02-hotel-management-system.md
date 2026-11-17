# 2. Hotel Management System

Aplicación para el personal de recepción y administración de un hotel. Reúne la información de huéspedes, habitaciones, reservas y pagos para que recepción pueda planificar las llegadas y salidas, confirmar la disponibilidad por fechas y dar seguimiento a la ocupación.

Esta propuesta figura tachada en el listado general del proyecto final.

Esta ficha describe las funcionalidades generales requeridas para el proyecto. El equipo de desarrollo deberá identificar y definir las funcionalidades específicas adicionales que se deriven del diseño que plantee.

## Tareas del sistema

- Registrar huéspedes y habitaciones y mantener actualizada la información necesaria para atender reservas.
- Consultar qué habitaciones están disponibles para un intervalo de fechas y evitar reservas que se superpongan para la misma habitación.
- Registrar, modificar o cancelar reservas según su estado y consultar las llegadas y salidas previstas.
- Registrar los pagos asociados a las reservas y consultar los importes pagados o pendientes.
- Controlar la ocupación y generar reportes de reservas, habitaciones y pagos por período.

## Administración de registros (CRUD)

Para los registros administrables, el sistema debe permitir crear, consultar, listar, modificar y eliminar según las reglas del negocio. El listado permite recorrer los registros disponibles y la búsqueda permite localizar registros que coincidan con un criterio.

- Huéspedes y habitaciones. Registrar, listar y actualizar sus datos. Eliminar registros sin reservas asociadas y conservar el historial cuando existan reservas o pagos.
- Reservas. Registrar y consultar reservas, modificar las que admitan cambios y cancelar según su estado. Conservar los pagos registrados.

## Búsquedas y filtros obligatorios

Estas consultas deben estar disponibles desde la interfaz. La búsqueda exacta debe localizar el registro correspondiente y la búsqueda parcial o por filtros debe listar todas las coincidencias. Si no hay resultados, el sistema debe indicarlo.

- Buscar huéspedes por identificación exacta o por coincidencia parcial de nombre.
- Buscar habitaciones por número y filtrar las disponibles por intervalo de fechas. Consultar reservas por huésped, estado o fecha de llegada.

## Ejemplo para verificar el funcionamiento

Registrar una reserva e intentar asignar la misma habitación a otra reserva con fechas superpuestas. El sistema debe rechazar el cruce y permitir una opción disponible.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es sugerir habitaciones disponibles según las fechas y la cantidad de huéspedes.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
