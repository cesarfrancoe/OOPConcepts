# Práctica: Representación y almacenamiento de datos en archivos

## 1. Introducción

Los archivos permiten almacenar información de manera persistente. Sin embargo, una misma información puede representarse de distintas formas, dependiendo de cómo se organicen los datos, qué codificación se utilice y cómo se almacenen físicamente cada uno de sus valores.

En esta práctica se explorarán las diferencias entre **datos estructurados, semiestructurados y no estructurados**, así como entre archivos de texto y archivos binarios. Para ello, se construirán manualmente seis archivos que contendrán información equivalente sobre tres personas.

Los archivos se examinarán mediante un editor de texto plano y un editor hexadecimal. Esto permitirá distinguir entre el contenido lógico de los datos, su organización y los bytes que realmente se almacenan.

### 1.1. Datos estructurados, semiestructurados y no estructurados

Los **datos estructurados** siguen un esquema definido que permite identificar campos, valores y relaciones. Por ejemplo, un registro de una persona puede contener una identificación, un nombre y un año de nacimiento.

Los **datos no estructurados** no siguen un esquema de campos predefinido. Por ejemplo, una narración en lenguaje natural puede contener información sobre varias personas sin utilizar posiciones ni delimitadores específicos para identificar cada dato.

Los **datos semiestructurados** presentan una organización reconocible mediante propiedades, etiquetas o elementos, pero no requieren necesariamente que todos los registros tengan exactamente los mismos atributos. JSON y XML son formatos habituales para representar esta clase de información, aunque también pueden contener datos con una estructura uniforme.

La clasificación de los datos no depende exclusivamente de la extensión del archivo. Un archivo de texto puede contener información estructurada o no estructurada.

## 2. Objetivos

### Objetivo general

Comprender las diferencias entre diversas formas de representación y almacenamiento de datos mediante la construcción, inspección y comparación de archivos de texto y binarios.

### Objetivos específicos

1. Diferenciar datos estructurados, semiestructurados y no estructurados.
2. Identificar y organizar información a partir de una narración en lenguaje natural.
3. Reconocer la representación física de los datos mediante bytes y valores hexadecimales.
4. Construir registros de longitud fija utilizando representaciones textuales y binarias.
5. Aplicar conceptos básicos de codificación ASCII, UTF-8 y orden de bytes.
6. Construir archivos utilizando CSV, JSON y XML.
7. Comparar el tamaño, la organización y la facilidad de interpretación de diferentes representaciones de almacenamiento.

## 3. Herramientas y condiciones generales

Para desarrollar la práctica se necesitan un editor de texto plano, como Bloc de notas, TextEdit configurado en modo texto plano o una herramienta equivalente; un editor hexadecimal que permita crear, modificar y guardar archivos byte a byte; y una calculadora que permita convertir números entre los sistemas decimal y hexadecimal.

Como material de consulta se utilizará el documento complementario `Endianness.md`.

No se requiere desarrollar programas ni utilizar un lenguaje de programación. Los archivos deberán construirse manualmente.

Se aplicarán las siguientes condiciones generales:

- Los archivos de texto utilizarán codificación UTF-8 sin BOM.
- Los nombres de las personas se escribirán utilizando caracteres ASCII y letras mayúsculas.
- Los archivos de registros fijos no incluirán encabezados, separadores ni saltos de línea.
- Los campos numéricos binarios se almacenarán en big-endian.
- Los archivos CSV, JSON y XML podrán utilizar saltos de línea e indentación para facilitar su lectura.
- Los archivos binarios podrán abrirse en editores de texto únicamente para observar su representación, sin guardar modificaciones desde estos editores.

## 4. Actividad 1: Construcción de un archivo de texto libre

**Archivo:** `persons_free.txt`

**Herramienta de creación:** editor de texto plano.

Crear un archivo que contenga exactamente el siguiente párrafo:

> Ana, identificada con la cédula 1001234567, nació en el año 2001. Por otra parte, Luis nació en 1998 y su número de identificación es 1002345678. Finalmente, tenemos a Maria, cuyo documento es 1003456789 y que nació en 2003.

Guardar el archivo utilizando UTF-8 sin BOM.

### Verificación

1. Abrir el archivo en un editor de texto y comprobar que el contenido sea correcto.
2. Abrir el mismo archivo en un editor hexadecimal.
3. Identificar la representación hexadecimal de algunos caracteres alfabéticos y numéricos.
4. Examinar cómo se almacena la letra acentuada `é`.
5. Verificar si existe algún salto de línea al finalizar el archivo.

### Preguntas

1. ¿Es posible identificar los datos de cada persona utilizando posiciones fijas dentro del archivo?
2. ¿Qué dificultades podría presentar la recuperación automática de información desde este texto?
3. ¿Todos los caracteres ocupan necesariamente un byte en UTF-8?

## 5. Actividad 2: Identificación y estructuración de los datos

A partir del contenido de `persons_free.txt`, identificar las personas mencionadas y extraer los siguientes atributos:

- `id`: número de identificación.
- `name`: nombre de la persona.
- `birthYear`: año de nacimiento.

Organizar la información obtenida en la siguiente tabla, conservando el orden en que aparecen las personas en la narración.

| id   | name | birthYear |
| ---- | ---- | --------- |
| <br> | <br> | <br>      |
| <br> | <br> | <br>      |
| <br> | <br> | <br>      |

Los nombres deberán escribirse en mayúsculas y sin modificar su contenido.

### Preguntas

1. ¿Cuántas personas se identificaron?
2. ¿Qué atributos son comunes a todas las personas?
3. ¿La información aparece siempre en el mismo orden dentro de la narración?
4. ¿Qué ventajas ofrece organizar estos datos en una tabla?
5. ¿Qué diferencia existe entre el texto original y los registros obtenidos?

La tabla construida será la fuente de información para las siguientes actividades.

## 6. Actividad 3: Registros de texto de longitud fija

**Archivo:** `persons_fixed.txt`

**Herramienta de creación:** editor hexadecimal.

Construir un archivo que contenga tres registros consecutivos, utilizando la información obtenida en la actividad anterior.

Cada registro tendrá la siguiente estructura:

| Campo       | Longitud     | Representación   |
| ----------- | ------------ | ---------------- |
| `id`        | 10 bytes     | Dígitos ASCII    |
| `name`      | 10 bytes     | Caracteres ASCII |
| `birthYear` | 4 bytes      | Dígitos ASCII    |
| **Total**   | **24 bytes** | <br>             |

### Reglas de almacenamiento

- La identificación ocupará exactamente 10 bytes.
- El nombre ocupará exactamente 10 bytes.
- Los espacios restantes del nombre se rellenarán por la derecha utilizando `0x20` (espacio ASCII).
- El año de nacimiento ocupará exactamente 4 bytes.
- Los registros se almacenarán consecutivamente, sin separadores ni saltos de línea.

### Procedimiento

1. Consultar los valores ASCII necesarios.
2. Convertir cada carácter a su representación hexadecimal.
3. Introducir manualmente los bytes correspondientes a cada registro.
4. Guardar el archivo como `persons_fixed.txt`.
5. Abrirlo en un editor de texto plano y observar su contenido.
6. Regresar al editor hexadecimal y verificar la posición de los campos.

### Verificación

| Elemento                        | Resultado esperado |
| ------------------------------- | ------------------ |
| Cantidad de registros           | 3                  |
| Tamaño por registro             | 24 bytes           |
| Tamaño total                    | 72 bytes           |
| Posición inicial del registro 1 | 0                  |
| Posición inicial del registro 2 | 24                 |
| Posición inicial del registro 3 | 48                 |

Las posiciones corresponden a desplazamientos en bytes, comenzando desde cero.

### Preguntas

1. ¿Cómo podemos recuperar un registro específico si conocemos su posición y la longitud de cada registro?
2. ¿Por qué es necesario completar el campo `name` con espacios?
3. ¿Qué ocurriría si se omitieran los bytes de relleno?
4. ¿Qué diferencias se observan entre la vista textual y la vista hexadecimal?

## 7. Actividad 4: Registros binarios de longitud fija

**Archivo:** `persons_fixed.bin`

**Herramienta de creación:** editor hexadecimal.

Construir un archivo binario que almacene las mismas tres personas mediante la siguiente estructura:

| Campo       | Longitud     | Representación       |
| ----------- | ------------ | -------------------- |
| `id`        | 4 bytes      | `int32`, big-endian  |
| `name`      | 10 bytes     | ASCII                |
| `birthYear` | 2 bytes      | `uint16`, big-endian |
| **Total**   | **16 bytes** | <br>                 |

### Reglas de almacenamiento

- La identificación se representará mediante un entero con signo de 32 bits.
- El año de nacimiento se representará mediante un entero sin signo de 16 bits.
- Ambos campos numéricos utilizarán big-endian.
- El nombre ocupará exactamente 10 bytes.
- Los bytes restantes del nombre se rellenarán por la derecha utilizando `0x00`.
- Los registros se almacenarán consecutivamente, sin encabezados ni separadores.

### Procedimiento

1. Convertir cada identificación decimal a hexadecimal.
2. Representar cada identificación utilizando exactamente 4 bytes.
3. Ordenar los bytes siguiendo la convención big-endian.
4. Convertir cada carácter del nombre a ASCII.
5. Completar el campo del nombre hasta alcanzar 10 bytes utilizando `0x00`.
6. Convertir cada año de nacimiento a hexadecimal utilizando exactamente 2 bytes.
7. Introducir manualmente los bytes correspondientes a los tres registros.
8. Guardar el archivo como `persons_fixed.bin`.
9. Abrirlo en un editor de texto plano únicamente para observar su contenido, sin guardar modificaciones.

### Verificación

| Elemento                        | Resultado esperado |
| ------------------------------- | ------------------ |
| Cantidad de registros           | 3                  |
| Tamaño por registro             | 16 bytes           |
| Tamaño total                    | 48 bytes           |
| Posición inicial del registro 1 | 0                  |
| Posición inicial del registro 2 | 16                 |
| Posición inicial del registro 3 | 32                 |

### Preguntas

1. ¿Por qué los campos numéricos no aparecen necesariamente como números legibles en un editor de texto?
2. ¿Qué diferencia existe entre rellenar el nombre con `0x00` y hacerlo con `0x20`?
3. ¿Qué ocurriría si los cuatro bytes de una identificación se interpretaran como little-endian?
4. ¿Por qué este archivo ocupa menos espacio que `persons_fixed.txt`?
5. ¿Qué información se necesita para interpretar correctamente los bytes de este archivo?

## 8. Actividad 5: Construcción de un archivo CSV

**Archivo:** `persons.csv`

**Herramienta de creación:** editor de texto plano.

Crear un archivo CSV utilizando los registros obtenidos en la actividad 2.

El archivo tendrá las siguientes columnas:

`id,name,birthYear`

### Reglas

- La primera línea contendrá los nombres de las columnas.
- Cada persona ocupará una línea.
- Los campos estarán separados por comas.
- Los registros conservarán el orden de la tabla construida.
- Se utilizará UTF-8 sin BOM.

### Verificación

1. Abrir el archivo en un editor de texto plano.
2. Abrirlo en un editor hexadecimal.
3. Identificar los bytes correspondientes a las comas.
4. Identificar los bytes utilizados para los saltos de línea.
5. Determinar si el archivo incluye un salto de línea después del último registro.

### Preguntas

1. ¿Cómo se identifican los campos y registros en un archivo CSV?
2. ¿Qué ventajas ofrece CSV frente a los registros de longitud fija?
3. ¿Qué dificultades pueden presentarse cuando los valores contienen comas?

## 9. Actividad 6: Construcción de un archivo JSON

**Archivo:** `persons.json`

**Herramienta de creación:** editor de texto plano.

Crear un documento JSON que contenga un arreglo de tres objetos, uno por cada persona identificada.

Cada objeto tendrá las siguientes propiedades:

| Propiedad   | Tipo JSON | Contenido         |
| ----------- | --------- | ----------------- |
| `id`        | Número    | Identificación    |
| `name`      | Cadena    | Nombre            |
| `birthYear` | Número    | Año de nacimiento |

### Reglas

- El elemento principal será un arreglo JSON.
- Cada persona estará representada por un objeto.
- Se utilizarán exactamente las propiedades indicadas.
- Los nombres se escribirán entre comillas dobles.
- Las identificaciones y los años se representarán como números, sin comillas.
- El archivo utilizará UTF-8 sin BOM.

### Verificación

1. Comprobar que el documento tenga una sintaxis JSON válida.
2. Abrirlo en un editor hexadecimal.
3. Identificar los bytes correspondientes a las llaves, corchetes, comillas, comas y dos puntos.
4. Comparar la cantidad de caracteres utilizados con los del archivo CSV.

### Preguntas

1. ¿Cómo se identifican los atributos de cada persona en JSON?
2. ¿Qué información sobre la organización de los datos proporciona JSON que no aparece explícitamente en CSV?
3. ¿Qué diferencias existen entre representar un valor como número y representarlo como cadena?

## 10. Actividad 7: Construcción de un archivo XML

**Archivo:** `persons.xml`

**Herramienta de creación:** editor de texto plano.

Crear un documento XML que contenga las tres personas.

La estructura tendrá:

- Un elemento raíz denominado `persons`.
- Un elemento `person` por cada persona.
- Dentro de cada elemento `person`, los elementos `id`, `name` y `birthYear`.

### Reglas

- El documento debe tener un único elemento raíz.
- Cada elemento debe cerrarse correctamente.
- Los registros deben conservar el orden de la tabla construida.
- El archivo utilizará UTF-8 sin BOM.
- Puede incluirse una declaración XML con codificación UTF-8, siempre que sea coherente con el contenido.

### Verificación

1. Comprobar que el documento esté bien formado.
2. Abrirlo en un editor hexadecimal.
3. Identificar los bytes correspondientes a los caracteres `<`, `>`, `/` y `=`, cuando aparezcan.
4. Comparar su tamaño con los archivos CSV y JSON.

### Preguntas

1. ¿Cómo se identifican los atributos y registros en XML?
2. ¿Por qué XML suele requerir más caracteres para representar estos registros?
3. ¿Qué diferencias existen entre la organización de la información en XML y JSON?

## 11. Comparación de resultados

Una vez construidos los seis archivos, completar la siguiente tabla:

| Archivo             | Tamaño (bytes) | Representación | Organización    |
| ------------------- | -------------- | -------------- | --------------- |
| `persons_free.txt`  | Por determinar | Texto          | No estructurada |
| `persons_fixed.txt` | 72             | Texto          | Estructurada    |
| `persons_fixed.bin` | 48             | Binaria        | Estructurada    |
| `persons.csv`       | Por determinar | Texto          | Estructurada    |
| `persons.json`      | Por determinar | Texto          | Estructurada    |
| `persons.xml`       | Por determinar | Texto          | Estructurada    |

JSON y XML también pueden representar información semiestructurada. En esta práctica se utilizan con una estructura uniforme para las tres personas.

Para los archivos de texto con longitud variable, el tamaño dependerá de detalles como los espacios, la indentación y los saltos de línea utilizados.

### Comparación entre registros fijos

Los archivos `persons_fixed.txt` y `persons_fixed.bin` almacenan la misma información y contienen la misma cantidad de registros.

La reducción de espacio de la representación binaria respecto a la textual fija se calcula mediante:

[\
\frac{72-48}{72}\times100=33,33%\
]

Esta reducción corresponde exclusivamente a las representaciones definidas en la práctica y no significa que todos los archivos binarios sean necesariamente más pequeños que los archivos de texto.

## 12. Preguntas de análisis

Responder con base en los archivos construidos y las observaciones realizadas.

1. ¿Cuál es la diferencia entre datos estructurados, semiestructurados y no estructurados?
2. ¿Por qué un archivo `.txt` puede contener datos estructurados?
3. ¿Qué diferencias se observaron al abrir un archivo binario en un editor de texto?
4. ¿Qué información necesitamos conocer para interpretar correctamente un registro binario?
5. ¿Por qué la codificación de caracteres afecta la cantidad de bytes almacenados?
6. ¿Cuál es la diferencia entre almacenar un número como caracteres ASCII y almacenarlo como entero binario?
7. ¿Qué ventajas y limitaciones presentan los registros de longitud fija?
8. ¿Qué ventajas ofrecen CSV, JSON y XML para intercambiar información?
9. ¿Por qué JSON y XML pueden utilizarse para representar datos semiestructurados?
10. ¿Podemos determinar el contenido lógico de cualquier archivo examinando únicamente sus bytes? Justificar.
11. ¿Qué formato facilita más la lectura humana y cuál permite localizar registros mediante desplazamientos fijos?
12. ¿Por qué no es correcto afirmar que todos los archivos binarios ocupan menos espacio que los archivos de texto?

## 13. Entrega

Cada estudiante deberá entregar:

1. Los seis archivos construidos manualmente, conservando los nombres especificados.
2. La tabla de registros obtenida en la actividad 2.
3. Una tabla con los tamaños reales de los archivos.
4. Las respuestas a las preguntas de análisis.
5. Evidencias de inspección hexadecimal de los archivos `persons_fixed.txt` y `persons_fixed.bin`, donde puedan identificarse los límites de los registros.

Los archivos deben conservar las representaciones establecidas en esta guía. No deben utilizarse programas para generar automáticamente su contenido.

## 14. Conclusión

Esta práctica permite comprobar que una misma información puede almacenarse de diferentes maneras y que cada representación presenta ventajas y limitaciones.

Los archivos de texto facilitan la lectura humana, mientras que las representaciones binarias permiten almacenar valores mediante formatos específicos. La estructura lógica de los datos, la codificación de caracteres, el tamaño de los campos y el orden de los bytes determinan cómo se organiza e interpreta la información.

Comprender estas diferencias es fundamental para el estudio posterior de archivos, estructuras de datos, persistencia e intercambio de información entre sistemas.
