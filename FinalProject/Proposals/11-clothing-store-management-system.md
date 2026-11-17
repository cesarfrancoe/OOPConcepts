# 11. Clothing Store Management System

Aplicación para el personal de una tienda de ropa que distingue cada artículo de sus variantes por talla y color. Relaciona el catálogo, las existencias y las ventas para que el personal pueda confirmar la disponibilidad de una variante concreta y revisar su movimiento.

Esta ficha describe las funcionalidades generales requeridas para el proyecto. El equipo de desarrollo deberá identificar y definir las funcionalidades específicas adicionales que se deriven del diseño que plantee.

## Tareas del sistema

- Registrar artículos de vestir con su categoría y precio y administrar sus variantes por talla y color.
- Registrar entradas y ajustes de inventario por variante y consultar la disponibilidad por categoría, talla o color.
- Registrar ventas con las variantes y cantidades exactas, calcular su importe y descontar las unidades del inventario tras comprobar la disponibilidad.
- Generar reportes de ventas y existencias que permitan distinguir las variantes de cada artículo.

## Administración de registros (CRUD)

Para los registros administrables, el sistema debe permitir crear, consultar, listar, modificar y eliminar según las reglas del negocio. El listado permite recorrer los registros disponibles y la búsqueda permite localizar registros que coincidan con un criterio.

- Artículos, categorías y variantes. Registrar, listar y actualizar artículos y sus combinaciones de talla y color. Evitar variantes duplicadas para un mismo artículo. Eliminar registros sin referencias y desactivar los que tengan ventas o movimientos.
- Inventario y ventas. Registrar existencias y movimientos por variante. Conservar en cada venta las variantes, cantidades e importes registrados.

## Búsquedas y filtros obligatorios

Estas consultas deben estar disponibles desde la interfaz. La búsqueda exacta debe localizar el registro correspondiente y la búsqueda parcial o por filtros debe listar todas las coincidencias. Si no hay resultados, el sistema debe indicarlo.

- Buscar artículos por código exacto o por coincidencia parcial de nombre.
- Combinar filtros de categoría, talla, color y disponibilidad. Consultar ventas o movimientos por variante y por intervalo de fechas.

## Ejemplo para verificar el funcionamiento

Vender una prenda disponible en dos tallas y comprobar que solo disminuyan las existencias de la talla y el color vendidos.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es sugerir qué variantes conviene reponer según sus existencias y ventas recientes.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
