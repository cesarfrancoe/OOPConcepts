# 3. Video Game Store

Aplicación para los empleados de una tienda de videojuegos que relaciona el catálogo, el inventario y las ventas. Permite al personal responder consultas sobre títulos disponibles y revisar qué productos se venden y qué ingresos generan.

Esta ficha describe las funcionalidades generales requeridas para el proyecto. El equipo de desarrollo deberá identificar y definir las funcionalidades específicas adicionales que se deriven del diseño que plantee.

## Tareas del sistema

- Registrar videojuegos con la información necesaria para la venta y organizarlos por categorías.
- Buscar títulos y consultar sus precios y existencias. Registrar las entradas de mercancía y los ajustes de inventario.
- Registrar ventas, calcular su importe y descontar las unidades vendidas, verificando que haya existencias suficientes.
- Consultar el historial de ventas y generar reportes de ingresos y unidades vendidas por período.

## Administración de registros (CRUD)

Para los registros administrables, el sistema debe permitir crear, consultar, listar, modificar y eliminar según las reglas del negocio. El listado permite recorrer los registros disponibles y la búsqueda permite localizar registros que coincidan con un criterio.

- Videojuegos y categorías. Registrar y listar títulos y categorías, editar sus datos y eliminar los que carezcan de referencias. Retirar del catálogo los títulos con historial de ventas y conservar su información.
- Existencias y ventas. Registrar entradas y ajustes de inventario. Conservar en cada venta los importes registrados aunque cambie el precio del catálogo.

## Búsquedas y filtros obligatorios

Estas consultas deben estar disponibles desde la interfaz. La búsqueda exacta debe localizar el registro correspondiente y la búsqueda parcial o por filtros debe listar todas las coincidencias. Si no hay resultados, el sistema debe indicarlo.

- Buscar un videojuego por código exacto o por coincidencia parcial de título.
- Filtrar el catálogo por categoría y disponibilidad. Consultar ventas por intervalo de fechas y por título.

## Ejemplo para verificar el funcionamiento

Registrar una venta con las últimas unidades disponibles. Una segunda venta del mismo título debe rechazarse si no hay existencias.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es sugerir títulos para reposición según las existencias y las ventas recientes.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
