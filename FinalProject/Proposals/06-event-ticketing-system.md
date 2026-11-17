# 6. Event Ticketing System

Aplicación para el personal que organiza eventos y atiende la venta de entradas. Relaciona los eventos con sus sedes y registra las ventas para que la taquilla pueda informar cuántas entradas quedan y operar dentro del aforo previsto.

## Tareas del sistema

- Registrar sedes y eventos con su fecha y aforo. Consultar los eventos programados y sus datos principales.
- Consultar cuántas entradas se han vendido y cuántas quedan disponibles por evento.
- Registrar ventas, calcular su importe y actualizar la disponibilidad. Validar que una venta no supere el aforo.
- Generar reportes de entradas vendidas, disponibilidad e ingresos por evento o período.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es identificar los eventos cercanos a agotar sus entradas según la disponibilidad registrada.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
