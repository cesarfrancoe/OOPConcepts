# Introducción a los Sistemas de Archivos (Filesystem)

## ¿Qué es un sistema de archivos?

Un **sistema de archivos (filesystem)** es el componente del sistema operativo encargado de definir cómo se almacenan, organizan y recuperan los datos en dispositivos como discos duros, memorias USB o unidades de estado sólido (SSD). Su función es ofrecer al usuario y a las aplicaciones una visión lógica de la información, independientemente de los detalles físicos del almacenamiento.

---

# Funciones principales de un sistema de archivos

* Organización de datos en archivos y carpetas.
* Gestión de metadatos (nombre, tamaño, permisos, fechas, ubicación).
* Control de acceso, definiendo quién puede leer, modificar o eliminar.
* Mantenimiento de integridad para evitar corrupción de datos.
* Optimización del espacio, reduciendo fragmentación y mejorando el rendimiento.

---

# Tipos de sistemas de archivos

## FAT32

* Propietario: Microsoft (especificación pública, hoy universal).
* Particiones y volúmenes: particiones fijas.
* Limitaciones: no admite archivos mayores a 4 GB ni particiones superiores a 2 TB.
* Uso típico: memorias USB y tarjetas SD.

## exFAT

* Propietario: Microsoft.
* Particiones y volúmenes: particiones fijas, diseñado para grandes archivos.
* Uso típico: discos portátiles y tarjetas SDXC.

## NTFS

* Propietario: Microsoft.
* Particiones y volúmenes: esquema clásico, con soporte a volúmenes dinámicos en Windows.
* Ventajas: journaling, permisos avanzados, cifrado, soporte de archivos muy grandes.
* Uso típico: sistemas Windows.

## ext4

* Abierto: comunidad Linux.
* Particiones y volúmenes: particiones fijas, con soporte a LVM (Logical Volume Manager).
* Ventajas: confiabilidad y eficiencia.
* Uso típico: distribuciones Linux.

## APFS (Apple File System)

* Propietario: Apple.
* Particiones y volúmenes: introduce contenedores APFS, que permiten crear múltiples volúmenes dinámicos que comparten espacio libre de manera flexible.
* Ventajas: optimizado para SSD, snapshots, cifrado nativo.
* Uso típico: macOS, iOS, iPadOS, tvOS y watchOS.

---

# Particiones y Volúmenes

## Particiones

Una partición es una división lógica de un disco físico. Cada partición puede estar formateada con un sistema de archivos distinto.

## Volúmenes

Un volumen es una unidad lógica de almacenamiento que puede corresponder a una partición o abarcar varias.

### Caso especial: APFS

En APFS, un contenedor equivale a una partición y dentro de él se pueden crear varios volúmenes dinámicos que comparten el espacio automáticamente. Esto evita el desperdicio de almacenamiento y aporta flexibilidad.

---

# Unidades de Almacenamiento en los Sistemas Operativos

## Windows: Letras de unidad

* Utiliza letras (A:, B:, C:, …).
* A: y B: → disqueteras.
* C: → disco principal (SO).
* D:, E:, … → otras particiones, discos externos, memorias USB, DVD.

## Linux y sistemas Unix-like

* No existen letras de unidad.
* Todo se integra en un árbol de directorios bajo `/`.
* Los dispositivos se montan en directorios:

  * `/mnt/usb` → memoria USB.
  * `/home` → puede estar en otro disco.

## macOS

* Basado en Unix.
* Monta volúmenes en `/Volumes/`.
* En Finder aparecen como unidades independientes, aunque internamente son directorios montados.

---

# Compatibilidad entre sistemas de archivos y sistemas operativos

| Sistema de archivos | Windows                    | macOS                                             | Linux                                       |
| ------------------- | -------------------------- | ------------------------------------------------- | ------------------------------------------- |
| FAT32               | Lectura/Escritura          | Lectura/Escritura                                 | Lectura/Escritura                           |
| exFAT               | Lectura/Escritura          | Lectura/Escritura (desde 10.6.5)                  | Lectura/Escritura (nativo desde kernel 5.4) |
| NTFS                | Lectura/Escritura (nativo) | Solo lectura (escritura con software de terceros) | Lectura/Escritura (con NTFS-3G o ntfs3)     |
| ext4                | No soportado nativamente   | Solo lectura (con software de terceros)           | Lectura/Escritura (nativo)                  |
| APFS                | No soportado               | Lectura/Escritura (nativo)                        | Solo lectura (drivers experimentales)       |

---

# Archivos, Carpetas y Rutas (Paths)

## Archivos

Un archivo es la unidad básica de almacenamiento de información. Puede ser de texto, imagen, audio, video o ejecutable. Incluye metadatos como nombre, tamaño, ubicación, fechas y permisos.

## Carpetas o Directorios

Las carpetas organizan archivos jerárquicamente. Una carpeta puede contener tanto archivos como otras carpetas (subdirectorios).

## Rutas (Paths)

Una ruta indica la ubicación exacta de un archivo o carpeta en el sistema de archivos:

* Ruta absoluta: parte desde la raíz.

  * Windows: `C:\Users\Ana\Documents\tesis.docx`
  * Linux/macOS: `/home/ana/Documentos/tesis.docx`

* Ruta relativa: depende del directorio actual.

  * Linux/macOS: `../imagenes/foto.png`

### Ejemplo: Carpeta Documentos

* En Windows (ruta real utilizada en terminal y PowerShell):
  `C:\Users\Ana\Documents`
* En Windows en español (alias mostrado en el explorador):
  `C:\Usuarios\Ana\Documentos`
* En Linux:
  `/home/ana/Documentos`
* En macOS:
  `/Users/Ana/Documents`

---

# Sensibilidad a Mayúsculas y Minúsculas en los Sistemas de Archivos

## Windows (NTFS, FAT32, exFAT)

* Por defecto, no es sensible a mayúsculas y minúsculas (case-insensitive).
* Ejemplo: `Documento.txt`, `documento.txt` y `DOCUMENTO.TXT` son el mismo archivo.
* Internamente, NTFS puede manejar distinción, pero la mayoría de programas los tratan como equivalentes.

## Linux (ext4 y otros)

* Es sensible a mayúsculas y minúsculas (case-sensitive).
* Ejemplo: `archivo.txt` y `Archivo.txt` son dos archivos diferentes.

## macOS (APFS, HFS+)

* Por defecto, no es sensible a mayúsculas y minúsculas.
* Al crear o formatear un volumen, puede configurarse como sensible.
* Ejemplo:

  * En volumen estándar: `informe.docx` y `Informe.docx` son el mismo archivo.
  * En volumen sensible: son dos archivos diferentes.

