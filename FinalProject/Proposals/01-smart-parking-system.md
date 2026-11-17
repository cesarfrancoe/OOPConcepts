# 1. Smart Parking System

Aplicación para el personal de un parqueadero que necesita conocer la ocupación durante la jornada y cobrar al finalizar cada estancia. El sistema vincula cada ingreso con su salida para que el operador pueda consultar los cupos disponibles y revisar la actividad del parqueadero.

Esta ficha describe las funcionalidades generales requeridas para el proyecto. El equipo de desarrollo deberá identificar y definir las funcionalidades específicas adicionales que se deriven del diseño que plantee.

## Tareas del sistema

- Registrar el ingreso de cada vehículo, con su identificación y la hora de entrada. Verificar que haya cupos y que el vehículo no tenga otro ingreso activo.
- Consultar los vehículos dentro del parqueadero y los cupos libres y ocupados.
- Registrar la salida, calcular el valor a pagar según el tiempo de permanencia y las tarifas vigentes, y liberar el cupo.
- Consultar el historial de entradas y salidas y generar reportes de ocupación e ingresos por período.

## Administración de registros (CRUD)

Para los registros administrables, el sistema debe permitir crear, consultar, listar, modificar y eliminar según las reglas del negocio. El listado permite recorrer los registros disponibles y la búsqueda permite localizar registros que coincidan con un criterio.

- Vehículos y tarifas. Registrar, listar y modificar los datos del vehículo y las tarifas aplicables. Eliminar registros sin movimientos asociados y desactivar los que tengan historial. Aplicar los cambios de tarifa a las operaciones según las reglas definidas por el equipo.

## Búsquedas y filtros obligatorios

Estas consultas deben estar disponibles desde la interfaz. La búsqueda exacta debe localizar el registro correspondiente y la búsqueda parcial o por filtros debe listar todas las coincidencias. Si no hay resultados, el sistema debe indicarlo.

- Buscar un vehículo mediante coincidencia exacta de placa y mostrar si tiene un ingreso activo.
- Filtrar los movimientos por intervalo de fechas y por estado (activo o cerrado). Consultar cupos libres y ocupados.

## Ejemplo para verificar el funcionamiento

Con el último cupo ocupado, intentar registrar otro ingreso. El sistema debe rechazarlo y permitir un ingreso después de registrar una salida válida.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es avisar al personal cuando la ocupación se acerque a la capacidad del parqueadero.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
