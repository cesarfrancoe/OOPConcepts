# **Introducción a las Excepciones en Java**

## **1. Introducción a las excepciones**

Cuando un programa se ejecuta, pueden ocurrir situaciones inesperadas que interrumpen su flujo normal: archivos que no existen, errores de conexión, datos inválidos, operaciones matemáticas imposibles, entre otras.
Para manejar estos eventos de forma ordenada y segura, Java incorpora un mecanismo sólido basado en *excepciones*.

Una excepción es un objeto que representa un error durante la ejecución. En lugar de que el programa termine abruptamente, Java permite detectar, lanzar y capturar estos errores para tratarlos adecuadamente.

Este mecanismo mejora la robustez del software, separa la lógica principal del manejo de errores y facilita la depuración.

## **2. ¿Qué es una excepción?**

Una excepción es una condición anormal que ocurre en tiempo de ejecución. Al producirse, Java crea un objeto que describe el problema y lo envía a la parte del programa responsable de manejarlo.

Ejemplos comunes:

* División entre cero
* Acceso fuera de rango a un arreglo
* Archivo no encontrado
* Error al convertir tipos
* Uso de una referencia nula

## **3. Jerarquía de excepciones en Java**

La jerarquía está encabezada por la clase base:

```
java.lang.Throwable
 ├── Error
 └── Exception
      ├── RuntimeException
      └── (Checked exceptions)
```

* **Error** representa fallos graves de la JVM.
* **Exception** representa errores que el programa puede manejar.
* Dentro de estas, Java distingue entre **checked** y **unchecked**.

## **4. Tipos de excepciones**

### **4.1 Excepciones Checked**

El compilador obliga a declararlas o manejarlas con `try-catch`.
Representan problemas del mundo real que deben anticiparse:

* Entrada/salida
* Archivos
* Bases de datos
* Fechas y formatos

Ejemplos:

* `IOException`
* `FileNotFoundException`
* `SQLException`
* `ParseException`

### **4.2 Excepciones Unchecked (RuntimeException)**

No requieren declaración ni manejo explícito.
Son errores de programación o lógicos:

* `NullPointerException`
* `IllegalStateException`
* `IndexOutOfBoundsException`
* `ArithmeticException`
* `NumberFormatException`

## **5. Manejo básico de excepciones**

### **5.1 Estructura try-catch-finally**

```java
try {
    // Código que puede causar un error
} catch (ExceptionType e) {
    // Manejo del error
} finally {
    // Siempre se ejecuta
}
```

### **5.2 Ejemplo: división entre cero**

```java
try {
    int result = 10 / 0;
    System.out.println(result);
} catch (ArithmeticException e) {
    System.out.println("Error: division by zero.");
}
```

### **5.3 Uso del bloque finally**

Útil para liberar recursos.

```java
FileInputStream fis = null;

try {
    fis = new FileInputStream("data.txt");
    // ...
} catch (IOException e) {
    System.out.println("File error.");
} finally {
    if (fis != null) {
        try {
            fis.close();
        } catch (IOException e) {
            System.out.println("Error closing file.");
        }
    }
}
```

## **6. Lanzar excepciones manualmente (throw)**

Se usa para indicar explícitamente un error detectado en la lógica del programa.

```java
public void setAge(int age) {
    if (age < 0) {
        throw new IllegalArgumentException("Age must be non-negative.");
    }
    this.age = age;
}
```

## **7. Declarar excepciones (throws)**

Se utiliza para indicar que un método puede lanzar una excepción checked.

```java
public String loadFile(String path) throws IOException {
    var file = new FileInputStream(path);
    var data = file.readAllBytes();
    file.close();
    return new String(data);
}
```

## **8. Tabla ampliada: excepciones más comunes y cuándo usarlas**

| Excepción                     | Tipo      | Cuándo usarla                       |
| ----------------------------- | --------- | ----------------------------------- |
| IllegalArgumentException      | Unchecked | Argumentos inválidos en un método   |
| NullPointerException          | Unchecked | Referencia nula                     |
| IllegalStateException         | Unchecked | Estado incorrecto del objeto        |
| IndexOutOfBoundsException     | Unchecked | Índice fuera de rango               |
| ArithmeticException           | Unchecked | Errores matemáticos                 |
| NumberFormatException         | Unchecked | Conversión fallida texto → número   |
| UnsupportedOperationException | Unchecked | Operación no soportada              |
| ClassCastException            | Unchecked | Conversión ilegal de tipos          |
| IOException                   | Checked   | Entrada/salida                      |
| FileNotFoundException         | Checked   | Archivo inexistente                 |
| SQLException                  | Checked   | Error en base de datos              |
| ParseException                | Checked   | Error al interpretar formatos       |
| ClassNotFoundException        | Checked   | Error cargando clases dinámicamente |


## **9. Ejemplos prácticos adicionales**

### **9.1 Validación de parámetros**

```java
public void setPrice(double price) {
    if (price < 0) {
        throw new IllegalArgumentException("Price must be positive.");
    }
    this.price = price;
}
```

### **9.2 Lectura de un archivo**

```java
public String read(String path) throws IOException {
    var file = new FileInputStream(path);
    var data = file.readAllBytes();
    file.close();
    return new String(data);
}
```

### **9.3 Conversión de tipos**

```java
try {
    int value = Integer.parseInt("ABC");
} catch (NumberFormatException e) {
    System.out.println("Invalid number format.");
}
```

### **9.4 Excepción personalizada**

```java
public class InvalidScoreException extends Exception {
    public InvalidScoreException(String message) {
        super(message);
    }
}
```

## **10. Buenas prácticas**

* Lanza excepciones específicas, no genéricas.
* No utilices excepciones para controlar flujos normales.
* No captures excepciones si no puedes manejarlas.
* Evita bloques catch vacíos.
* Agrega mensajes significativos.
* Separa el manejo de errores de la lógica de negocio.
* Revisa los contratos (qué lanza cada método).

## **11. Diferencias en el manejo de excepciones entre Java y otros lenguajes**

Java se puede comparar con otros lenguajes en cuanto al diseño, nivel de explicitud y filosofía.

### **Java vs Python**

* Python no tiene checked exceptions.
* Manejo más simple pero menos explícito.
* Todo es equivalente a RuntimeException.

### **Java vs C#**

* C# no tiene checked exceptions.
* Java obliga a documentar errores externos.
* C# produce código más compacto.

### **Java vs Swift**

* Swift usa `throws` pero sin checked estrictos.
* Permite manejar errores con `try`, `try?`, `try!`.
* Los errores se modelan como enums.

### **Java vs Kotlin**

* Kotlin elimina las checked exceptions.
* Usa `Result<T>` y `runCatching` para errores controlados.
* Filosofía más funcional y menos verbosa.

### **Java vs JavaScript / TypeScript**

* Todo es unchecked.
* Puede lanzarse cualquier objeto.
* TypeScript añade tipos a nivel de error, pero sigue siendo dinámico en tiempo de ejecución.

## **12. Conclusión**

El manejo de excepciones en Java combina un enfoque orientado a objetos con un sistema claro y estructurado que obliga a pensar en los posibles errores desde el diseño. Aprender a usar correctamente las excepciones permite crear software robusto, claro y mantenible.
Comprender las diferencias con otros lenguajes facilita formar un criterio profesional sobre cuándo aplicar cada enfoque.
