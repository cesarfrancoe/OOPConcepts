# 6. Event Ticketing System

Aplicación para el personal que organiza eventos y atiende la venta de entradas. Relaciona los eventos con sus sedes y registra las ventas para que la taquilla pueda informar cuántas entradas quedan y operar dentro del aforo previsto.

Esta ficha describe las funcionalidades generales requeridas para el proyecto. El equipo de desarrollo deberá identificar y definir las funcionalidades específicas adicionales que se deriven del diseño que plantee.

## Tareas del sistema

- Registrar sedes y eventos con su fecha y aforo. Consultar los eventos programados y sus datos principales.
- Consultar cuántas entradas se han vendido y cuántas quedan disponibles por evento.
- Registrar ventas, calcular su importe y actualizar la disponibilidad. Validar que una venta no supere el aforo.
- Generar reportes de entradas vendidas, disponibilidad e ingresos por evento o período.

## Administración de registros (CRUD)

Para los registros administrables, el sistema debe permitir crear, consultar, listar, modificar y eliminar según las reglas del negocio. El listado permite recorrer los registros disponibles y la búsqueda permite localizar registros que coincidan con un criterio.

- Sedes y eventos. Registrar, listar y editar sus datos. Eliminar registros sin operaciones asociadas y conservar los que tengan ventas. Validar que los cambios de aforo admitan las entradas ya vendidas.
- Ventas. Registrar la cantidad, el evento y el importe de cada operación. Consultar el historial y aplicar las restricciones del negocio a las correcciones.

## Búsquedas y filtros obligatorios

Estas consultas deben estar disponibles desde la interfaz. La búsqueda exacta debe localizar el registro correspondiente y la búsqueda parcial o por filtros debe listar todas las coincidencias. Si no hay resultados, el sistema debe indicarlo.

- Buscar eventos por código exacto o por coincidencia parcial de nombre. Filtrar por sede, fecha o disponibilidad de entradas.
- Consultar ventas por identificador y listar las de un evento en un período.

## Ejemplo para verificar el funcionamiento

Intentar vender más entradas de las que quedan. El sistema debe rechazar la venta y conservar la disponibilidad anterior.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es identificar los eventos cercanos a agotar sus entradas según la disponibilidad registrada.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
