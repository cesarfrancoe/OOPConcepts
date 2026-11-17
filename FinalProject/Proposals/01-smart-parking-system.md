# 1. Smart Parking System

Aplicación para el personal de un parqueadero que necesita conocer la ocupación durante la jornada y cobrar al finalizar cada estancia. El sistema vincula cada ingreso con su salida para que el operador pueda consultar los cupos disponibles y revisar la actividad del parqueadero.

## Tareas del sistema

- Registrar el ingreso de cada vehículo, con su identificación y la hora de entrada. Verificar que haya cupos y que el vehículo no tenga otro ingreso activo.
- Consultar los vehículos dentro del parqueadero y los cupos libres y ocupados.
- Registrar la salida, calcular el valor a pagar según el tiempo de permanencia y las tarifas vigentes, y liberar el cupo.
- Consultar el historial de entradas y salidas y generar reportes de ocupación e ingresos por período.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es avisar al personal cuando la ocupación se acerque a la capacidad del parqueadero.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
