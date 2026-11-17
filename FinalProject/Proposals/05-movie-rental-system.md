# 5. Movie Rental System

Aplicación para los empleados de un negocio de alquiler de películas que permite distinguir el catálogo de los ejemplares físicamente disponibles. El personal puede seguir cada préstamo desde su entrega hasta la devolución y consultar la fecha prevista de regreso y el valor del alquiler.

Esta ficha describe las funcionalidades generales requeridas para el proyecto. El equipo de desarrollo deberá identificar y definir las funcionalidades específicas adicionales que se deriven del diseño que plantee.

## Tareas del sistema

- Registrar las películas, clasificarlas por categorías y consultar los ejemplares disponibles de cada título.
- Registrar alquileres, asociarlos al cliente atendido e indicar la fecha prevista de devolución.
- Registrar devoluciones y actualizar la disponibilidad de los ejemplares.
- Calcular el importe del alquiler según las tarifas vigentes y las condiciones de devolución aplicables.
- Consultar alquileres activos y vencidos y generar reportes de alquileres y devoluciones por período.

## Administración de registros (CRUD)

Para los registros administrables, el sistema debe permitir crear, consultar, listar, modificar y eliminar según las reglas del negocio. El listado permite recorrer los registros disponibles y la búsqueda permite localizar registros que coincidan con un criterio.

- Películas, ejemplares y clientes. Registrar, listar y actualizar sus datos. Eliminar registros sin alquileres asociados y desactivar los que deban conservarse por su historial.
- Alquileres. Registrar la entrega y la devolución de cada ejemplar, aplicar las tarifas correspondientes y conservar el historial de esas operaciones.

## Búsquedas y filtros obligatorios

Estas consultas deben estar disponibles desde la interfaz. La búsqueda exacta debe localizar el registro correspondiente y la búsqueda parcial o por filtros debe listar todas las coincidencias. Si no hay resultados, el sistema debe indicarlo.

- Buscar películas por coincidencia parcial de título y filtrar por categoría o disponibilidad. Buscar un ejemplar por su código exacto.
- Consultar alquileres por cliente o identificador. Filtrar por estado o fecha prevista de devolución.

## Ejemplo para verificar el funcionamiento

Alquilar el único ejemplar disponible de un título. Comprobar que desaparezca del listado de disponibles y que vuelva a aparecer al devolverlo.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es identificar los alquileres activos cuya fecha de devolución está próxima o vencida.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
