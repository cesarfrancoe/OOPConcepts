# 9. Gym Membership Management System

Aplicación para el personal de un gimnasio que administra la relación entre los miembros y los planes contratados. Facilita el seguimiento de renovaciones y pagos, la comprobación de la vigencia al momento del ingreso y la consulta de entrenadores asignados.

Esta ficha describe las funcionalidades generales requeridas para el proyecto. El equipo de desarrollo deberá identificar y definir las funcionalidades específicas adicionales que se deriven del diseño que plantee.

## Tareas del sistema

- Registrar miembros y administrar los planes de membresía con sus precios, duración y condiciones.
- Registrar altas, renovaciones y pagos, y consultar la vigencia de cada membresía.
- Comprobar si el miembro cumple las condiciones de acceso y registrar su ingreso cuando corresponda.
- Asignar entrenadores y consultar qué miembros atiende cada uno.
- Generar reportes de membresías, pagos y accesos por período.

## Administración de registros (CRUD)

Para los registros administrables, el sistema debe permitir crear, consultar, listar, modificar y eliminar según las reglas del negocio. El listado permite recorrer los registros disponibles y la búsqueda permite localizar registros que coincidan con un criterio.

- Miembros, planes y entrenadores. Registrar, listar y editar sus datos. Eliminar registros sin referencias y desactivar los que tengan historial de membresías, pagos o asignaciones.
- Membresías y pagos. Registrar altas, renovaciones y pagos, consultar su historial y comprobar la vigencia antes de admitir un ingreso.

## Búsquedas y filtros obligatorios

Estas consultas deben estar disponibles desde la interfaz. La búsqueda exacta debe localizar el registro correspondiente y la búsqueda parcial o por filtros debe listar todas las coincidencias. Si no hay resultados, el sistema debe indicarlo.

- Buscar miembros por identificación exacta o por coincidencia parcial de nombre. Consultar miembros asignados a un entrenador.
- Filtrar membresías por plan, estado o fecha de vencimiento y consultar los pagos de un miembro por período.

## Ejemplo para verificar el funcionamiento

Consultar el acceso de un miembro con la membresía vencida. Registrar la renovación y comprobar el nuevo estado y el historial de pagos.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es identificar membresías próximas a vencer para facilitar su seguimiento.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
