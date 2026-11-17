# Práctica: Representación y almacenamiento de datos en archivos

## 1. Introducción

Los archivos permiten almacenar información de manera persistente. Sin embargo, una misma información puede representarse de distintas formas, dependiendo de cómo se organicen los datos, qué codificación se utilice, cómo se almacenen físicamente sus valores y de los requerimientos técnicos que deban cumplirse.

En esta práctica se construirán y examinarán diferentes archivos que contienen información equivalente sobre tres personas. El propósito es comprender las diferencias entre datos estructurados, semiestructurados y no estructurados, así como entre las representaciones textuales y binarias.

La práctica se desarrollará mediante la creación manual de archivos y su inspección con un editor hexadecimal, sin necesidad de escribir programas.

## 2. Herramientas y preparación

Se utilizarán las siguientes herramientas:

| Herramienta | Propósito |
|---|---|
| [Visual Studio Code](https://code.visualstudio.com/) | Crear y examinar archivos |
| [Hex Editor (Microsoft)](https://marketplace.visualstudio.com/items?itemName=ms-vscode.hexeditor) | Visualizar y modificar bytes |
| Procesador de texto | Crear documentos `.doc` y `.docx` |
| Calculadora | Convertir números decimales a hexadecimales |

Para utilizar Hex Editor en Visual Studio Code, instalar la extensión `ms-vscode.hexeditor`. Posteriormente, abrir un archivo mediante **Open With... → Hex Editor**.

### Condiciones generales

- Todos los archivos se construirán manualmente, sin desarrollar programas.
- Los archivos de texto utilizarán UTF-8 sin BOM.
- El contenido de los archivos de texto utilizará únicamente caracteres ASCII.
- Los nombres se escribirán en mayúsculas al construir los registros estructurados.
- Los registros de longitud fija no tendrán encabezados, separadores ni saltos de línea.
- Los campos numéricos binarios utilizarán big-endian.
- Los archivos `.doc` y `.docx` conservarán sus formatos originales, sin cambiar simplemente sus extensiones.

## 3. Actividad 1: Archivo de texto libre

**Archivo:** `persons_free.txt`

Crear un archivo de texto plano que contenga exactamente la siguiente narración en inglés.

**Texto en español (referencia):**

> Ana, identificada con la cédula 1001234567, nació en el año 2001. Por otra parte, Luis nació en 1998 y su número de identificación es 1002345678. Finalmente, tenemos a Maria, cuyo documento es 1003456789 y que nació en 2003.

**Texto en inglés (contenido del archivo):**

> Ana, identified by ID number 1001234567, was born in 2001. On the other hand, Luis was born in 1998, and his ID number is 1002345678. Finally, Maria has ID number 1003456789 and was born in 2003.

Guardar el archivo utilizando UTF-8 sin BOM y sin agregar un salto de línea al final.

Abrirlo con Hex Editor e identificar las representaciones hexadecimales de letras, números, espacios y signos de puntuación.

**Resultado esperado:** 195 caracteres y 195 bytes.

Comprobar que cada carácter ocupa un byte y que no existen bytes adicionales al final.

## 4. Actividad 2: Documentos de procesador de texto

**Archivos:** `persons_free.doc` y `persons_free.docx`

Utilizando un procesador de texto, crear dos documentos que contengan exactamente el mismo párrafo en inglés de la actividad anterior.

Guardar el primero en formato Microsoft Word 97–2003 (`.doc`) y el segundo en formato Word moderno (`.docx`).

### Exploración

1. Abrir ambos archivos con Hex Editor.
2. Comparar sus primeros bytes y sus tamaños con los de `persons_free.txt`.
3. Crear una copia de `persons_free.docx` y cambiar la extensión de la copia a `.zip`.
4. Descomprimir el archivo ZIP y explorar su estructura interna.
5. Localizar `word/document.xml` y examinar su contenido.

El formato DOCX utiliza un contenedor ZIP que incluye documentos XML y otros recursos. Cambiar la extensión de la copia no transforma el archivo: permite examinar su estructura utilizando herramientas ZIP.

Observar que un documento puede contener texto legible para una persona y, sin embargo, utilizar una representación física que no corresponde a un archivo de texto plano.

## 5. Actividad 3: Identificación y estructuración de los datos

A partir de la narración de la actividad 1, identificar las tres personas y extraer los siguientes atributos:

- `id`: número de identificación.
- `name`: nombre de la persona.
- `birthYear`: año de nacimiento.

Completar la siguiente tabla, conservando el orden de aparición de las personas y escribiendo los nombres en mayúsculas.

| id | name | birthYear |
|---|---|---|
| | | |
| | | |
| | | |

Esta información se utilizará para construir los archivos de las siguientes actividades.

## 6. Actividad 4: Registros de texto de longitud fija

**Archivo:** `persons_fixed.txt`

Construir manualmente un archivo con tres registros consecutivos, utilizando la siguiente estructura:

| Campo | Longitud | Representación |
|---|---:|---|
| `id` | 10 bytes | Dígitos ASCII |
| `name` | 10 bytes | Caracteres ASCII |
| `birthYear` | 4 bytes | Dígitos ASCII |
| **Total** | **24 bytes** | |

### Reglas

- Cada identificación ocupará exactamente 10 bytes.
- Los nombres se rellenarán por la derecha con espacios ASCII (`0x20`) hasta completar 10 bytes.
- Cada año ocupará 4 bytes.
- No se utilizarán separadores ni saltos de línea.

Utilizar Hex Editor para introducir manualmente los bytes correspondientes a cada registro.

Después, abrir el archivo en el editor de texto y comparar ambas representaciones.

### Verificación

| Elemento | Resultado esperado |
|---|---:|
| Registros | 3 |
| Bytes por registro | 24 |
| Tamaño total | 72 bytes |
| Inicio del registro 1 | 0 |
| Inicio del registro 2 | 24 |
| Inicio del registro 3 | 48 |

Comprobar que los campos pueden localizarse mediante sus posiciones y longitudes.

## 7. Actividad 5: Registros binarios de longitud fija

**Archivo:** `persons_fixed.bin`

Construir manualmente un archivo binario que contenga los mismos tres registros, utilizando la siguiente estructura:

| Campo | Longitud | Representación |
|---|---:|---|
| `id` | 4 bytes | `int32`, big-endian |
| `name` | 10 bytes | ASCII |
| `birthYear` | 2 bytes | `uint16`, big-endian |
| **Total** | **16 bytes** | |

### Reglas

- Convertir las identificaciones decimales a enteros binarios de 32 bits.
- Representar los años mediante enteros sin signo de 16 bits.
- Utilizar big-endian para ambos campos numéricos.
- Rellenar los nombres por la derecha con bytes `0x00` hasta completar 10 bytes.
- No incluir encabezados, separadores ni saltos de línea.

Crear el archivo introduciendo manualmente los bytes mediante Hex Editor.

Examinar también el archivo desde el editor de texto, sin guardar modificaciones.

### Verificación

| Elemento | Resultado esperado |
|---|---:|
| Registros | 3 |
| Bytes por registro | 16 |
| Tamaño total | 48 bytes |
| Inicio del registro 1 | 0 |
| Inicio del registro 2 | 16 |
| Inicio del registro 3 | 32 |

Comparar los bytes de los campos numéricos con los del archivo de texto de longitud fija. Observar las diferencias entre almacenar dígitos ASCII y almacenar valores enteros binarios.

Para profundizar en el orden de bytes, consultar `Endianness.md`.

## 8. Actividad 6: Archivo CSV

**Archivo:** `persons.csv`

Crear un archivo CSV con la información de las tres personas.

Utilizar la siguiente cabecera:

```csv
id,name,birthYear
```

Cada persona ocupará una línea y sus campos estarán separados por comas. Conservar el orden de los registros y utilizar UTF-8 sin BOM.

Abrir el archivo con Hex Editor e identificar los bytes correspondientes a las comas y los saltos de línea.

## 9. Actividad 7: Archivo JSON

**Archivo:** `persons.json`

Crear un archivo JSON que contenga un arreglo de tres objetos, uno por cada persona.

Cada objeto deberá incluir:

| Propiedad | Tipo JSON |
|---|---|
| `id` | Número |
| `name` | Cadena |
| `birthYear` | Número |

Utilizar exactamente los nombres de propiedades indicados. Los números se representarán sin comillas y los nombres como cadenas.

Comprobar que el documento tenga una sintaxis JSON válida y examinar sus bytes con Hex Editor.

## 10. Actividad 8: Archivo XML

**Archivo:** `persons.xml`

Crear un archivo XML con la información de las tres personas.

Utilizar un elemento raíz `persons` que contenga tres elementos `person`. Cada persona tendrá los elementos `id`, `name` y `birthYear`.

El documento deberá estar bien formado y utilizar UTF-8 sin BOM.

Examinar el archivo con Hex Editor e identificar los bytes correspondientes a las etiquetas XML.

## 11. Comparación final

Registrar los tamaños reales de los ocho archivos construidos.

| Archivo | Tamaño (bytes) | Representación |
|---|---:|---|
| `persons_free.txt` | 195 | Texto plano UTF-8 |
| `persons_free.doc` | Por determinar | Documento binario Word 97–2003 |
| `persons_free.docx` | Por determinar | Contenedor ZIP con XML |
| `persons_fixed.txt` | 72 | Texto ASCII de longitud fija |
| `persons_fixed.bin` | 48 | Registros binarios de longitud fija |
| `persons.csv` | Por determinar | Texto plano CSV |
| `persons.json` | Por determinar | Texto plano JSON |
| `persons.xml` | Por determinar | Texto plano XML |

Los tamaños de algunos archivos pueden variar según los espacios, saltos de línea, indentación y herramientas utilizadas.

### Comparación de registros fijos

Los archivos `persons_fixed.txt` y `persons_fixed.bin` contienen la misma información, pero utilizan diferentes representaciones.

La reducción de tamaño obtenida con la representación binaria es:

\[
\frac{72-48}{72}\times100=33,33\%
\]

Este resultado corresponde a las estructuras definidas en la práctica y no implica que todos los archivos binarios sean más pequeños que los archivos de texto.

### Discusión final

Durante la clase, analizar conjuntamente las siguientes cuestiones:

1. ¿Qué diferencias existen entre datos estructurados, semiestructurados y no estructurados?
2. ¿Qué diferencias se observaron entre TXT, DOC y DOCX al examinar sus bytes?
3. ¿Por qué los mismos números ocupan diferentes cantidades de bytes en los registros textuales y binarios?
4. ¿Qué información se necesita para interpretar correctamente un archivo binario?
5. ¿Qué ventajas y limitaciones presentan los diferentes formatos utilizados?

El propósito de esta comparación es reconocer que la organización lógica de los datos, su representación física y el formato del archivo son aspectos relacionados, pero diferentes.