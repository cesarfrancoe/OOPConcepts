# Taller: Diseño e Implementación de un Sistema de Gestión Hotelera

## Objetivo

Analizar, diseñar e implementar en un lenguaje de programación un sistema para administrar **un único hotel**, aplicando abstracción, encapsulamiento, herencia, sobrescritura, polimorfismo y relaciones entre clases. El énfasis principal está en el **diseño orientado a objetos**, que deberá justificarse antes de iniciar la implementación.

## Contexto y reglas del negocio

Un hotel turístico necesita administrar sus habitaciones, huéspedes, reservas y comprobantes. El sistema corresponde a **un solo establecimiento**, representado por un objeto principal del dominio; no se requiere gestionar cadenas hoteleras ni múltiples establecimientos.

### 1. Hotel

El hotel tiene un identificador único, nombre y dirección. Ocupa **una sola torre de mínimo ocho pisos**. La cantidad total de pisos se define al crear el hotel, debe ser mayor o igual a ocho y no cambia posteriormente.

El hotel administra sus habitaciones, huéspedes y reservas. Las habitaciones son partes exclusivas de su estructura: se crean para ese hotel, no se trasladan a otros establecimientos y dejan de existir en el sistema si se elimina el hotel. Cada habitación conoce el hotel al que pertenece.

El hotel establece una **única tarifa básica por persona para cada noche de alojamiento**, común a todas sus habitaciones. Es un solo valor de referencia: no existen una tarifa por persona y otra tarifa por noche. También establece el **costo del minibar por noche**, utilizado exclusivamente en las suites. Ambos valores deben ser mayores que cero. La tarifa básica por persona sirve como referencia para calcular el precio de cada tipo de habitación; no se asigna una tarifa básica independiente a cada habitación.

### 2. Habitaciones

Cada habitación posee un **número único dentro del hotel**, piso, configuración de camas y la indicación de si tiene vista de frente al mar. Su piso debe estar entre 1 y la cantidad total de pisos del hotel.

Cada cama sencilla permite alojar una persona y cada cama doble, dos. La capacidad máxima se obtiene de la configuración de camas; no es un valor independiente de ella.

Todas las habitaciones incluyen televisión por cable. Cada habitación individual, doble o familiar **puede tener o no canales premium**, según las características definidas al crearla; todas las suites los incluyen. El huésped puede solicitar una reserva de una habitación con canales premium, pero solo se asignará si existe una disponible. La solicitud no modifica las características de las habitaciones.

Cada habitación puede estar **habilitada** o **fuera de servicio por mantenimiento**. Una habitación fuera de servicio no puede reservarse. Su disponibilidad para una nueva reserva depende tanto de su estado operativo como de la ausencia de reservas pendientes o confirmadas.

Se contemplan cuatro tipos:

- **Habitación individual (Single Room):** una cama sencilla y capacidad para una persona. Se cobra el equivalente a **una tarifa básica por persona**, ajustada por ubicación.
- **Habitación doble (Double Room):** una cama doble y capacidad para dos personas. Su tarifa completa equivale a **dos tarifas básicas por persona**, ajustadas por ubicación. Con dos huéspedes se cobra el 100 % de ese valor; con uno, el **70 %**.
- **Habitación familiar (Family Room):** exactamente dos camas dobles y entre dos y cuatro camas sencillas; su capacidad es de **seis a ocho personas**, según la configuración. Puede reservarse para menos de seis huéspedes, pero siempre se cobra el equivalente a **seis tarifas básicas por persona**, ajustadas por ubicación. Por cada huésped que exceda seis se cobra **un 50 % adicional de la tarifa básica por persona ajustada por ubicación**, por noche.
- **Suite:** una cama doble, capacidad máxima para dos personas, sala privada, canales premium y minibar. **Es el único tipo de habitación con minibar** y solo puede ubicarse en **uno de los dos pisos superiores**. Se cobra siempre el equivalente a **dos tarifas básicas por persona**, ajustadas por ubicación, con independencia de si la ocupan una o dos personas, más el costo diario del minibar establecido por el hotel.

### 3. Recargos por ubicación

La **tarifa básica por persona para cada noche de alojamiento**, establecida en el hotel, se ajusta según el piso y la vista de frente al mar:

| Ubicación | Recargo sobre la tarifa básica por persona |
|---|---:|
| Pisos 1 a 3 | 0 % |
| Pisos 4 a 6 | 10 % |
| Piso 7 en adelante | 20 % |
| Vista de frente al mar | 15 % adicional |

Los recargos por piso y vista de frente al mar **se suman**, sin aplicarse sucesivamente. Primero se obtiene la tarifa por persona ajustada por ubicación; después se aplica la regla de ocupación propia del tipo de habitación. En las suites, el costo del minibar se agrega **después** del ajuste por ubicación y del cálculo para dos personas.

Para precisar el cálculo, se utilizan las siguientes variables:

- **B:** tarifa básica por persona para cada noche de alojamiento, definida en el hotel.
- **A:** tarifa por persona ajustada por ubicación: `A = B × (1 + recargoPiso + recargoVista)`.
- **H:** número de huéspedes de la reserva.
- **N:** número de noches.
- **M:** costo del minibar por noche definido en el hotel.

El costo total de cada tipo de habitación se determina así:

| Tipo | Costo total de la reserva |
|---|---|
| Individual | `A × N` |
| Doble, un huésped | `(2 × A × 0.70) × N` |
| Doble, dos huéspedes | `(2 × A) × N` |
| Familiar, de uno a seis huéspedes | `(6 × A) × N` |
| Familiar, siete u ocho huéspedes, si la capacidad lo permite | `(6 × A + (H − 6) × 0.50 × A) × N` |
| Suite, uno o dos huéspedes | `(2 × A + M) × N` |

**Ejemplo:** si el hotel establece una tarifa básica de **$100.000 por persona para cada noche**, una habitación del piso 5 con vista de frente al mar tiene una tarifa ajustada de **$125.000 por persona para cada noche** (10 % + 15 %). En ese caso, una habitación doble ocupada por una persona cuesta **$175.000 por noche** (`2 × $125.000 × 0.70`), mientras que la misma habitación ocupada por dos personas cuesta **$250.000 por noche**.

El 50 % aplicable a cada huésped adicional de una habitación familiar se calcula sobre la **tarifa por persona ajustada**, no sobre el costo total de la habitación familiar.

### 4. Huéspedes

De cada huésped se registran un identificador único, nombre completo, documento de identificación, teléfono y correo electrónico. Un huésped puede existir sin reservas y puede ser responsable de varias. Cada reserva tiene un único huésped responsable.

### 5. Reservas

Cada reserva registra un identificador único, huésped responsable, habitación, cantidad de personas, cantidad de noches y estado: **pendiente, confirmada o cancelada**.

Se deben respetar las siguientes condiciones:

- El huésped responsable debe estar registrado.
- La habitación debe estar habilitada y no tener otra reserva pendiente o confirmada.
- La cantidad de huéspedes debe ser mayor que cero y no exceder la capacidad de la habitación.
- La cantidad de noches debe ser mayor que cero.
- Una reserva pendiente puede confirmarse o cancelarse; una confirmada puede cancelarse; una cancelada no puede confirmarse nuevamente.
- Cancelar una reserva libera la habitación para nuevas reservas, siempre que esté habilitada.

El costo de la reserva se calcula según la ubicación, el tipo de habitación, la cantidad de huéspedes y las noches. **No se utilizarán fechas de entrada y salida ni calendarios**: para efectos del taller, una reserva pendiente o confirmada ocupa la habitación hasta que sea cancelada.

### 6. Comprobantes

Al confirmar una reserva se genera **un único comprobante**, con número único, identificador de la reserva, nombre del huésped responsable, número de habitación, cantidad de noches y costo total del alojamiento.

El comprobante pertenece exclusivamente a la reserva que lo originó y se conserva incluso si posteriormente se cancela la reserva. El sistema debe permitir **consultar un comprobante por su número único**. La estrategia para localizarlo forma parte de las decisiones de diseño del desarrollador.

No se requiere gestionar pagos, impuestos, facturación electrónica, inventarios del minibar ni persistencia de datos.

---

## Parte I. Análisis y diseño orientado a objetos

### 1. Diagrama de clases UML

Antes de programar, cada desarrollador deberá:

1. Identificar las clases necesarias y sus responsabilidades.
2. Definir atributos, tipos de datos, visibilidad, métodos, parámetros, tipos de retorno y constructores.
3. Identificar las relaciones entre clases y justificar cuándo corresponden asociación, agregación o composición; indicar multiplicidades y navegabilidad.
4. Determinar qué comportamientos pueden generalizarse y cuáles requieren especialización mediante herencia y polimorfismo.
5. Establecer las validaciones y restricciones que deben garantizarse en el modelo.
6. Elaborar **en papel** el diagrama de clases UML.

El desarrollador presentará y justificará su diagrama ante el **jefe de proyectos**. Deberá explicar cómo el diseño satisface las reglas del negocio. Se aceptan distintas soluciones justificadas; no existe un único diagrama obligatorio. **No se establece una cantidad mínima, máxima ni aproximada de clases:** cada clase deberá responder a una responsabilidad identificable y justificarse durante la revisión técnica.

**Es indispensable obtener la aprobación del diseño antes de iniciar la implementación.**

---

## Parte II. Implementación y validación en Java

### 2A. Implementación del paquete `model`

Implementar el modelo de acuerdo con el diagrama UML aprobado. El código deberá:

- Aplicar encapsulamiento y validar los datos para preservar las reglas del negocio.
- Implementar correctamente las relaciones entre objetos y mantener la consistencia de las relaciones bidireccionales.
- Utilizar herencia, sobrescritura y polimorfismo de forma coherente con el diseño.
- Calcular los costos sin trasladar las reglas del negocio al programa de pruebas.
- **Lanzar excepciones** cuando se incumplan las restricciones; las clases del modelo no deben imprimir mensajes en consola ni solicitar datos al usuario.

### 2B. Esquema del hotel e implementación del paquete `view`

**Diseño físico individual.** Cada desarrollador diseñará su propio hotel y presentará un **esquema visual** de la torre, que muestre:

- Nombre del hotel y cantidad total de pisos (mínimo ocho).
- Distribución de habitaciones por piso, con número y tipo de habitación.
- Orientación de cada habitación: **con vista de frente al mar** o **sin vista de frente al mar**.
- Configuración de camas en las habitaciones familiares.

Los diseños de los desarrolladores deberán ser diferentes y cumplir las mismas reglas del negocio. El esquema se presentará y justificará ante el jefe de proyectos y deberá corresponder a los objetos que posteriormente se creen en Java.

**Inicialización y pruebas.** Dentro del paquete `view`, implementar una clase **`Main`** que:

1. Cree un único hotel con las características de su esquema, su tarifa básica por persona para cada noche y el costo diario del minibar.
2. Cree y registre las habitaciones diseñadas, con sus pisos, orientación, camas y características, utilizando la tarifa básica por persona establecida en el hotel.
3. Registre huéspedes y realice reservas con distintas cantidades de personas y noches.
4. Calcule y muestre tarifas que permitan verificar los recargos por ubicación y las reglas específicas de cada tipo de habitación.
5. Confirme y cancele reservas, y consulte comprobantes por su número único.
6. Pruebe situaciones inválidas y **controle las excepciones** lanzadas por el modelo, mostrando los resultados por consola.

`Main` será únicamente el **punto de entrada y escenario de validación**: no deberá duplicar los cálculos tarifarios ni las reglas del dominio. **No se requiere interfaz gráfica.**

### Organización sugerida del proyecto

```text
HotelManagement/
└── src/
    ├── model/
    │   └── ... clases del dominio
    └── view/
        └── Main.java
```

## Requisitos de diseño, implementación y estilo

### Requisitos de diseño

- El diagrama UML debe especificar clases, responsabilidades, atributos y sus tipos, operaciones con parámetros y tipos de retorno, constructores y visibilidad.
- Las relaciones propuestas deben incluir el tipo de relación, sus multiplicidades y navegabilidad, y ser justificadas durante la revisión técnica.
- Las abstracciones, especializaciones y comportamientos polimórficos deben responder a reglas reales del dominio; evitar clases, atributos o relaciones redundantes.
- No existe una cantidad obligatoria de clases. La calidad del diseño se valorará por la asignación coherente de responsabilidades y el cumplimiento de los requisitos, no por el número de clases propuestas.
- Las restricciones del negocio deben poder garantizarse desde el modelo, no depender únicamente de las pruebas realizadas en `Main`.
- El diseño aprobado y el código implementado deben ser consistentes; cualquier ajuste posterior debe justificarse.

### Requisitos de implementación

- Separar las clases del dominio en `model` y el punto de entrada de pruebas en `view/Main.java`.
- Mantener los atributos encapsulados y utilizar constructores, métodos de acceso y modificación solo cuando correspondan, sin permitir estados inválidos.
- Reutilizar el comportamiento común y emplear sobrescritura y despacho polimórfico para las políticas tarifarias; evitar cadenas de `if` o `switch` que distingan subclases para calcular el precio.
- Garantizar la consistencia de las relaciones bidireccionales y la pertenencia exclusiva de las habitaciones al hotel.
- Lanzar excepciones desde `model` ante operaciones inválidas y controlarlas desde `view`; no ocultar errores ni sustituirlos por mensajes impresos desde el modelo.
- Verificar desde `Main` casos válidos, casos límite y casos inválidos, incluyendo restricciones de pisos, ocupación, estados de reservas y consulta de comprobantes.
- Demostrar que las habitaciones del esquema visual coinciden con las instancias creadas y que los resultados de las pruebas pueden explicarse a partir de las reglas del negocio.
- No implementar interfaz gráfica, persistencia ni dependencias externas innecesarias.

### Requisitos de estilo

- Utilizar identificadores en inglés y nombres descriptivos: `UpperCamelCase` para clases, `lowerCamelCase` para atributos, métodos y variables, y `UPPER_SNAKE_CASE` para constantes.
- Declarar los atributos como `private` y exponer únicamente las operaciones necesarias para preservar el encapsulamiento.
- Mantener métodos de responsabilidad clara, sin duplicación innecesaria de lógica y con indentación uniforme.
- Evitar atributos derivados o innecesarios y métodos de modificación que permitan romper las invariantes del objeto.
- Escribir comentarios solo cuando aclaren decisiones o reglas que no sean evidentes en el código.
- Evitar entrada o salida por consola dentro de `model`; los mensajes de `Main` pueden estar en español o inglés.

## Condiciones generales y entregables

- Lenguaje: **Java**.
- Identificadores del código en **inglés**: `UpperCamelCase` para clases y `lowerCamelCase` para atributos y métodos.
- Los mensajes de consola pueden escribirse en español o inglés.
- No se requiere base de datos, persistencia ni interfaz gráfica.
- **Entregables:** (1) diagrama UML en papel aprobado; (2) esquema visual individual del hotel; (3) proyecto Java con `model` y `view/Main.java`; (4) presentación y justificación técnica de las decisiones de diseño y demostración de las pruebas.

Se evaluará la coherencia entre los requisitos, el diseño UML, el esquema físico y el comportamiento de la implementación.

## Diccionario español–inglés

Vocabulario de apoyo para comprender y expresar los conceptos del taller en inglés. Cada desarrollador deberá decidir cómo utilizar estos términos en su diseño y construir sus propios identificadores.

| Español | Inglés | Español | Inglés |
| --- | --- | --- | --- |
| Ajustado | Adjusted | Habitación individual | Single room |
| Alojamiento | Accommodation | Hotel | Hotel |
| Buscar | Find | Huésped | Guest |
| Buscar por nombre | Find by name | Identificador | Identifier |
| Buscar por… | Find by… | Mantenimiento | Maintenance |
| Calcular | Calculate | Máximo | Maximum |
| Cama doble | Double bed | Minibar | Minibar |
| Cama sencilla | Single bed | Mínimo | Minimum |
| Canales premium | Premium channels | Noche | Night |
| Cancelado | Cancelled | Nombre completo | Full name |
| Cancelar | Cancel | Número | Number |
| Cantidad | Count | Obtener | Get |
| Capacidad | Capacity | Obtener nombre | Get name |
| Comprobante de reserva | Reservation confirmation | Ocupación | Occupancy |
| Confirmado | Confirmed | Pendiente | Pending |
| Confirmar | Confirm | Piso | Floor |
| Consultar | Look up | Por noche | Per night |
| Correo electrónico | Email | Por persona | Per person |
| Costo | Cost | Recargo | Surcharge |
| Crear | Create | Registrar | Register |
| Dirección | Address | Reserva | Reservation |
| Disponible | Available | Responsable | Responsible |
| Documento de identificación | Identity document | Sala privada | Private living room |
| Eliminar | Delete | Suite | Suite |
| Establecer nombre | Set name | Tarifa | Rate |
| Estado | Status | Tarifa básica | Base rate |
| Fuera de servicio | Out of service | Teléfono | Phone number |
| Generar | Generate | Torre | Tower |
| Habilitado | Enabled | Total | Total |
| Habilitar | Enable | Ubicación | Location |
| Habitación | Room | Único | Unique |
| Habitación doble | Double room | Validar | Validate |
| Habitación familiar | Family room | Vista de frente al mar | Direct sea view |
