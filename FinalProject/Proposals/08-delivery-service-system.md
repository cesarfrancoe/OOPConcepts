# 8. Delivery Service System

Aplicación para el personal que coordina un servicio de domicilios. Reúne los pedidos y la disponibilidad de los repartidores para facilitar la asignación de entregas, consultar su avance y calcular el costo del servicio.

Esta ficha describe las funcionalidades generales requeridas para el proyecto. El equipo de desarrollo deberá identificar y definir las funcionalidades específicas adicionales que se deriven del diseño que plantee.

## Tareas del sistema

- Registrar pedidos de entrega con la información necesaria para su atención y seguimiento.
- Administrar los datos de los repartidores y consultar su disponibilidad.
- Asignar pedidos a repartidores disponibles y actualizar el estado de cada entrega a medida que avanza.
- Calcular el costo de entrega según las condiciones del servicio y consultar el historial del pedido.
- Generar reportes de entregas por estado, repartidor o período.

## Administración de registros (CRUD)

Para los registros administrables, el sistema debe permitir crear, consultar, listar, modificar y eliminar según las reglas del negocio. El listado permite recorrer los registros disponibles y la búsqueda permite localizar registros que coincidan con un criterio.

- Repartidores. Registrar, listar y actualizar sus datos y disponibilidad. Eliminar registros sin entregas asociadas y desactivar los que tengan historial.
- Pedidos. Registrar pedidos y corregir sus datos mientras su estado lo permita. Gestionar su asignación y conservar el historial de entregas completadas o canceladas.

## Búsquedas y filtros obligatorios

Estas consultas deben estar disponibles desde la interfaz. La búsqueda exacta debe localizar el registro correspondiente y la búsqueda parcial o por filtros debe listar todas las coincidencias. Si no hay resultados, el sistema debe indicarlo.

- Buscar pedidos por número exacto y filtrarlos por estado, repartidor o fecha.
- Buscar repartidores por identificación o por coincidencia parcial de nombre, y consultar cuáles están disponibles.

## Ejemplo para verificar el funcionamiento

Intentar asignar un pedido a un repartidor no disponible y comprobar el rechazo. Asignarlo a uno disponible y verificar que el pedido aparezca en su listado.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es sugerir un repartidor según su disponibilidad y la cantidad de entregas activas.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
