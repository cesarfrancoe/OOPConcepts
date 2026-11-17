# 7. Restaurant Order Management

Aplicación para el personal de un restaurante que organiza la atención por mesas. Relaciona los pedidos con el menú y permite seguir su avance hasta el cierre de la cuenta, de modo que el personal pueda consultar qué mesas están ocupadas y qué pedidos siguen abiertos.

Esta ficha describe las funcionalidades generales requeridas para el proyecto. El equipo de desarrollo deberá identificar y definir las funcionalidades específicas adicionales que se deriven del diseño que plantee.

## Tareas del sistema

- Administrar el menú y consultar los precios y la disponibilidad de los platos.
- Registrar pedidos por mesa y actualizar los productos y cantidades mientras el pedido admita cambios.
- Consultar pedidos activos y actualizar su estado conforme avanza la atención.
- Calcular el total de la cuenta, registrar el cierre del pedido y actualizar la disponibilidad de la mesa.
- Generar reportes de pedidos atendidos y ventas por período.

## Administración de registros (CRUD)

Para los registros administrables, el sistema debe permitir crear, consultar, listar, modificar y eliminar según las reglas del negocio. El listado permite recorrer los registros disponibles y la búsqueda permite localizar registros que coincidan con un criterio.

- Menú y mesas. Registrar, listar y actualizar platos y mesas. Eliminar registros sin referencias y desactivar los que figuren en pedidos anteriores.
- Pedidos. Agregar, modificar o retirar productos mientras el pedido esté abierto. Conservar las cantidades y los importes de las cuentas cerradas.

## Búsquedas y filtros obligatorios

Estas consultas deben estar disponibles desde la interfaz. La búsqueda exacta debe localizar el registro correspondiente y la búsqueda parcial o por filtros debe listar todas las coincidencias. Si no hay resultados, el sistema debe indicarlo.

- Buscar platos por coincidencia parcial de nombre y filtrar los que estén disponibles.
- Buscar un pedido por número y consultar los pedidos por mesa, estado o fecha. Listar las mesas libres y ocupadas.

## Ejemplo para verificar el funcionamiento

Abrir un pedido, cambiar una cantidad y cerrar la cuenta. Verificar el importe, la liberación de la mesa y que el pedido cerrado permanezca en el historial.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es señalar los pedidos activos que llevan más tiempo pendientes de atención.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
