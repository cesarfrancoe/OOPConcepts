# 10. Pharmacy Inventory System

Aplicación para el personal de una farmacia que reúne los datos de medicamentos, proveedores y movimientos de inventario. Permite consultar existencias al atender una venta y revisar las entradas y salidas de productos para orientar la reposición.

Esta ficha describe las funcionalidades generales requeridas para el proyecto. El equipo de desarrollo deberá identificar y definir las funcionalidades específicas adicionales que se deriven del diseño que plantee.

## Tareas del sistema

- Registrar medicamentos y proveedores y consultar los productos asociados a cada proveedor.
- Registrar entradas de mercancía y ajustes de inventario, y consultar las existencias de cada medicamento.
- Registrar ventas, calcular su importe y descontar las unidades vendidas cuando haya existencias suficientes.
- Consultar los movimientos de inventario y generar reportes de ventas y disponibilidad por período.

## Administración de registros (CRUD)

Para los registros administrables, el sistema debe permitir crear, consultar, listar, modificar y eliminar según las reglas del negocio. El listado permite recorrer los registros disponibles y la búsqueda permite localizar registros que coincidan con un criterio.

- Medicamentos y proveedores. Registrar, listar y actualizar sus datos. Eliminar registros sin movimientos y desactivar los que tengan ventas o entradas asociadas.
- Inventario y ventas. Registrar entradas, ajustes y ventas. Validar cantidades, evitar existencias negativas y conservar el historial de movimientos.

## Búsquedas y filtros obligatorios

Estas consultas deben estar disponibles desde la interfaz. La búsqueda exacta debe localizar el registro correspondiente y la búsqueda parcial o por filtros debe listar todas las coincidencias. Si no hay resultados, el sistema debe indicarlo.

- Buscar medicamentos por código exacto o por coincidencia parcial de nombre y filtrar por proveedor o nivel de existencias.
- Buscar proveedores por nombre. Consultar movimientos de un medicamento y ventas por intervalo de fechas.

## Ejemplo para verificar el funcionamiento

Registrar una entrada y después una venta. Verificar el saldo en inventario y comprobar el rechazo de una venta que supere ese saldo.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es identificar medicamentos con existencias bajas para priorizar la reposición.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
