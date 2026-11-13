# Endianness: Big-endian y Little-endian

## 1. Introducción

El **endianness** es la convención que establece el orden de los bytes de un dato que ocupa más de un byte, como un entero de 16, 32 o 64 bits.

Existen dos convenciones principales:

- **Big-endian:** almacena primero el byte más significativo (*Most Significant Byte*, MSB).
- **Little-endian:** almacena primero el byte menos significativo (*Least Significant Byte*, LSB).

### Convención de lectura

En este documento, las secuencias de bytes se presentan de **izquierda a derecha (LTR)**, siguiendo el orden en que aparecen en el archivo, desde la posición de menor desplazamiento hasta la de mayor desplazamiento.

Por tanto:

- El **primer byte** es el situado más a la izquierda.
- El **último byte** es el situado más a la derecha.
- El primer byte no necesariamente es el más significativo: esto depende del endianness.

### Almacenamiento e interpretación

Es importante distinguir dos operaciones:

**Almacenamiento:** consiste en escribir los bytes que representan un valor numérico, siguiendo un orden determinado.

**Interpretación:** consiste en recuperar el valor numérico a partir de los bytes almacenados, aplicando las reglas correspondientes a su tamaño, orden y representación.

El endianness no modifica el valor matemático de un número cuando se almacena y se interpreta utilizando la misma convención. Sin embargo, utilizar una convención incorrecta durante la lectura puede producir un valor diferente.

## 2. Ejemplo de almacenamiento

Consideremos el número hexadecimal `0x12345678`, que ocupa cuatro bytes:

| Byte | Valor hexadecimal | Importancia         |
| ---- | ----------------- | ------------------- |
| 1    | `12`              | Más significativo   |
| 2    | `34`              | <br>                |
| 3    | `56`              | <br>                |
| 4    | `78`              | Menos significativo |

Su almacenamiento depende de la convención:

| Convención    | Primero (izquierda) → Último (derecha) |
| ------------- | -------------------------------------- |
| Big-endian    | `12 34 56 78`                          |
| Little-endian | `78 56 34 12`                          |

Ambas secuencias representan el mismo número cuando se interpretan utilizando el orden correspondiente.

## 3. Ejemplo de interpretación

Supongamos que un archivo contiene exactamente los siguientes bytes, presentados de izquierda a derecha:

`80 00 00 01`

No conocemos el endianness ni sabemos si representan un entero de 32 bits con signo (`int32`) o sin signo (`uint32`).

Existen cuatro interpretaciones posibles:

| Endianness    | Tipo     | Hexadecimal interpretado | Valor decimal  |
| ------------- | -------- | ------------------------ | -------------- |
| Big-endian    | `int32`  | `0x80000001`             | −2.147.483.647 |
| Big-endian    | `uint32` | `0x80000001`             | 2.147.483.649  |
| Little-endian | `int32`  | `0x01000080`             | 16.777.344     |
| Little-endian | `uint32` | `0x01000080`             | 16.777.344     |

**Observación:** los cuatro bytes almacenados permanecen iguales. Los resultados cambian porque se aplican diferentes reglas de interpretación.

## 4. Enteros con signo y sin signo

El endianness y la representación de números negativos son conceptos independientes.

Para enteros de 32 bits:

| Tipo     | Valor mínimo   | Valor máximo  |
| -------- | -------------- | ------------- |
| `int32`  | −2.147.483.648 | 2.147.483.647 |
| `uint32` | 0              | 4.294.967.295 |

En `int32`, suponiendo complemento a dos, el bit 31 tiene un peso de (-2^{31}). En `uint32`, ese mismo bit tiene un peso positivo de (2^{31}).

### Nota: cálculo manual del complemento a dos

Para representar −5 utilizando 8 bits:

1. **Representar +5:** `00000101`
2. **Invertir todos los bits:** `11111010`
3. **Sumar 1:** `11111011`

Por tanto:

`−5 = 11111011` (8 bits, complemento a dos).

Podemos verificarlo asignando peso negativo al bit más significativo:

[\
-128+64+32+16+8+2+1=-5\
]

El procedimiento depende del número de bits utilizado. Por ejemplo, −5 en 32 bits se representa como `0xFFFFFFFB`.

## 5. Preguntas generales y respuestas

### 1. ¿Qué diferencia existe entre big-endian y little-endian?

Big-endian almacena primero el byte más significativo, mientras que little-endian almacena primero el menos significativo. Ambas convenciones permiten representar los mismos valores numéricos.

### 2. ¿Qué significa «primer byte»?

Es el byte que ocupa la primera posición del dato almacenado, es decir, el de menor desplazamiento dentro de ese dato. En las representaciones LTR de este documento, aparece a la izquierda.

### 3. ¿El primer byte siempre es el más significativo?

No. En big-endian, el primer byte es el más significativo. En little-endian, es el menos significativo.

### 4. ¿Qué diferencia existe entre almacenar e interpretar un número?

Almacenar consiste en escribir su representación en bytes. Interpretar consiste en reconstruir el valor numérico aplicando las reglas del formato. Los bytes pueden permanecer idénticos y producir valores diferentes si cambian las reglas de interpretación.

### 5. ¿El endianness modifica el valor matemático de un número?

No, siempre que el orden utilizado al almacenar y recuperar el número sea consistente. Si se interpreta con un orden diferente, generalmente se obtiene otro valor.

### 6. ¿Todos los datos se ven afectados por el endianness?

No. Un dato de un solo byte no presenta diferencias de endianness. Este concepto resulta relevante cuando un dato ocupa varios bytes y su orden determina la interpretación.

### 7. ¿Qué sucede si un número almacenado en little-endian se interpreta como big-endian?

Generalmente se obtiene otro valor. Por ejemplo, `01 00 00 00` representa 1 en little-endian y 16.777.216 en big-endian, suponiendo un entero de 32 bits.

### 8. ¿Qué diferencia existe entre `int32` y `uint32`?

Ambos utilizan 32 bits. `int32` representa valores positivos y negativos mediante complemento a dos, mientras que `uint32` representa únicamente valores no negativos.

### 9. ¿Por qué `FF FF FF FF` puede representar −1 o 4.294.967.295?

Porque depende de la representación numérica:

| Interpretación              | Valor         |
| --------------------------- | ------------- |
| `int32` (complemento a dos) | −1            |
| `uint32`                    | 4.294.967.295 |

El endianness no afecta este ejemplo porque los cuatro bytes son iguales.

### 10. ¿Qué es el complemento a dos?

Es una representación binaria que permite expresar enteros positivos y negativos utilizando una cantidad fija de bits. Para representar un número negativo, puede escribirse su valor absoluto, invertirse todos sus bits y sumarse 1, siempre que el número esté dentro del rango representable.

### 11. ¿Existen otras representaciones para los números negativos?

Sí. Entre ellas se encuentran signo y magnitud y complemento a uno. Sin embargo, el complemento a dos es el método predominante para representar enteros con signo en los sistemas modernos.

### 12. ¿El bit más significativo siempre indica el signo?

No. En un entero con signo representado mediante complemento a dos, el bit más significativo determina si el valor es negativo. En un entero sin signo, ese bit tiene un peso positivo.

### 13. ¿El endianness modifica el orden de los bits dentro de cada byte?

No. El endianness convencional determina el orden de los bytes, no el orden de los bits individuales dentro de ellos.

Por ejemplo, el byte `80` corresponde al patrón binario `10000000`, independientemente de que forme parte de un dato big-endian o little-endian.

### 14. ¿Dónde se encuentra el bit 31 de un entero de 32 bits?

El bit 31 es el más significativo del valor numérico. En big-endian se encuentra en el primer byte almacenado; en little-endian, en el cuarto.

### 15. ¿Cómo podemos identificar el endianness de un archivo?

La forma más confiable es consultar la especificación de su formato. Algunos archivos incluyen indicadores de orden de bytes o campos conocidos que permiten identificarlo. No siempre puede determinarse examinando únicamente los bytes.

### 16. ¿Es posible convertir datos entre big-endian y little-endian?

Sí. Para un entero de tamaño fijo, basta con invertir el orden de sus bytes.

Por ejemplo:

- Big-endian: `12 34 56 78`
- Little-endian: `78 56 34 12`

Ambas secuencias representan `0x12345678` cuando se interpretan correctamente.

### 17. ¿Un archivo puede contener campos con diferentes órdenes de bytes?

Sí. Un formato binario puede definir distintas convenciones para diferentes campos. Por ello, deben respetarse las especificaciones de cada uno.

### 18. ¿Dónde se utilizan big-endian y little-endian?

Big-endian se utiliza tradicionalmente como orden de bytes de red (*network byte order*) en diversos protocolos. Little-endian es el orden nativo habitual de arquitecturas como x86 y x86-64.

### 19. ¿Cuál convención es mejor?

Ninguna es universalmente superior. Ambas son válidas. La elección depende de la arquitectura, el protocolo o el formato de archivo.

### 20. ¿Por qué es importante conocer el endianness al utilizar un editor hexadecimal?

Porque el editor muestra los bytes almacenados, pero estos no necesariamente revelan el valor numérico original. Para interpretarlos correctamente debemos conocer el tamaño del dato, su orden de bytes y su representación numérica.
