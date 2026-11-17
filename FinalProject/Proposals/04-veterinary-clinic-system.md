# 4. Veterinary Clinic System

Aplicación para el personal de una clínica veterinaria que organiza la atención desde la programación de citas hasta la consulta del historial de cada mascota. Reúne la información de propietarios, veterinarios y tratamientos registrados para facilitar la coordinación entre recepción y el personal clínico.

Esta ficha describe las funcionalidades generales requeridas para el proyecto. El equipo de desarrollo deberá identificar y definir las funcionalidades específicas adicionales que se deriven del diseño que plantee.

## Tareas del sistema

- Registrar mascotas y propietarios y consultar las mascotas asociadas a cada propietario.
- Gestionar la información y disponibilidad de los veterinarios para asignar citas.
- Agendar, reprogramar o cancelar citas y comprobar que los horarios sean compatibles con la disponibilidad del veterinario.
- Registrar los tratamientos indicados durante la atención y consultar el historial de cada mascota.
- Generar reportes de citas y atenciones por período o por veterinario.

## Administración de registros (CRUD)

Para los registros administrables, el sistema debe permitir crear, consultar, listar, modificar y eliminar según las reglas del negocio. El listado permite recorrer los registros disponibles y la búsqueda permite localizar registros que coincidan con un criterio.

- Mascotas, propietarios y veterinarios. Registrar, listar y actualizar sus datos. Eliminar registros sin citas ni atenciones asociadas y aplicar restricciones cuando exista historial.
- Citas y atenciones. Registrar, reprogramar o cancelar citas según su estado. Registrar las atenciones y conservar la relación entre la mascota, el veterinario y el tratamiento consignado.

## Búsquedas y filtros obligatorios

Estas consultas deben estar disponibles desde la interfaz. La búsqueda exacta debe localizar el registro correspondiente y la búsqueda parcial o por filtros debe listar todas las coincidencias. Si no hay resultados, el sistema debe indicarlo.

- Buscar propietarios por identificación exacta o por nombre parcial. Buscar mascotas por nombre y acotar los resultados por propietario.
- Filtrar citas por veterinario, fecha o estado. Consultar las atenciones de una mascota por intervalo de fechas.

## Ejemplo para verificar el funcionamiento

Agendar una cita e intentar asignar al mismo veterinario una segunda cita en un horario que se cruza. Tras cancelar la primera, comprobar que el horario vuelva a estar disponible.

## Requisitos comunes

El sistema debe recuperar sus datos entre ejecuciones y permitir exportar datos o reportes a CSV desde la interfaz. Debe incluir una función de apoyo a decisiones. Una aplicación posible es sugerir horarios disponibles para una cita según la disponibilidad registrada.

Consulta los demás [requisitos generales del proyecto final](../README.md#requisitos-del-proyecto).
