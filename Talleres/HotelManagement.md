# Taller: Diseño e Implementación de un Sistema de Gestión Hotelera

## Objetivo

Analizar, diseñar e implementar en un lenguaje de programación un sistema para administrar un único hotel, aplicando abstracción, encapsulamiento, herencia, sobrescritura, polimorfismo y relaciones entre clases. El énfasis principal está en el diseño orientado a objetos, que deberá justificarse antes de iniciar la implementación.

## Contexto y reglas del negocio

Un hotel turístico necesita administrar sus habitaciones, huéspedes, reservas y comprobantes. El sistema corresponde a un solo establecimiento, representado por un objeto principal del dominio; no se requiere gestionar cadenas hoteleras ni múltiples establecimientos.

### 1. Hotel

El hotel tiene un identificador único, nombre y dirección. Ocupa una sola torre de mínimo ocho pisos. La cantidad total de pisos se define al crear el hotel, debe ser mayor o igual a ocho y no cambia posteriormente.

El hotel administra sus habitaciones, huéspedes y reservas. Las habitaciones son partes exclusivas de su estructura: se crean para ese hotel, no se trasladan a otros establecimientos y dejan de existir en el sistema si se elimina el hotel. Cada habitación conoce el hotel al que pertenece.

El hotel establece una tarifa base de habitación por noche (TBH), una tarifa de cama sencilla por noche (TCS) y una tarifa de minibar por noche (TMI), utilizada exclusivamente en las suites. Estos valores deben ser mayores que cero y son comunes a las habitaciones del hotel. Las tarifas de cama doble y de persona adicional se calculan a partir de TCS; el recargo por vista de frente al mar se calcula sobre TBH y el recargo por piso se calcula sobre el recargo por vista de frente al mar. El hotel define el porcentaje de recargo por vista de frente al mar (PVM); por ejemplo, 30 representa el 30 %. También define un recargo fijo por televisión con canales premium por habitación y por noche (RCP), aplicado únicamente a las habitaciones que la incluyen. No se asignan tarifas base independientes a cada habitación.

### 2. Habitaciones

Cada habitación posee un número único dentro del hotel, piso, configuración de camas y la indicación de si tiene vista de frente al mar. Su piso debe estar entre 1 y la cantidad total de pisos del hotel.

Cada cama sencilla permite alojar una persona y cada cama doble, dos. La capacidad máxima se obtiene de la configuración de camas; no es un valor independiente de ella.

Todas las habitaciones incluyen televisión por cable. Cada habitación individual, doble o familiar puede tener o no televisión con canales premium, según las características definidas al crearla; todas las suites la incluyen. El huésped puede solicitar una reserva de una habitación con televisión con canales premium, pero solo se asignará si existe una disponible. La solicitud no modifica las características de las habitaciones. Cada habitación con televisión con canales premium genera el cargo correspondiente por cada noche reservada, independientemente de la cantidad de huéspedes; en las habitaciones sin televisión con canales premium ese cargo es cero.

Cada habitación puede estar habilitada o fuera de servicio por mantenimiento. Una habitación fuera de servicio no puede reservarse. Su disponibilidad para una nueva reserva depende tanto de su estado operativo como de la ausencia de reservas pendientes o confirmadas.

Se contemplan cuatro tipos:

- **Habitación individual (Single Room):** una cama sencilla y capacidad para una persona. Se cobra la tarifa base ajustada de habitación más la tarifa de una cama sencilla por noche.
- **Habitación doble (Double Room):** una cama doble y capacidad para dos personas. Se cobra la tarifa base ajustada de habitación más la tarifa de cama doble correspondiente a uno o dos huéspedes.
- **Habitación familiar (Family Room):** exactamente dos camas dobles y entre dos y cuatro camas sencillas; su capacidad es de seis a ocho personas, según la configuración. Para uno a seis huéspedes se cobra una tarifa mínima de camas equivalente a una cama doble ocupada por dos personas más cuatro camas sencillas, además de la tarifa base ajustada de habitación. Esta equivalencia es únicamente tarifaria y no modifica la configuración física. Por cada huésped que exceda seis se agrega el 70 % de la tarifa de cama sencilla, por noche, siempre que la capacidad lo permita.
- **Suite:** una cama doble, capacidad máxima para dos personas, sala privada, televisión con canales premium y minibar. Es el único tipo de habitación con minibar y solo puede ubicarse en **uno de los dos pisos superiores**. Se cobra la tarifa base ajustada de habitación más la tarifa de cama doble ocupada por dos personas y la tarifa de minibar, independientemente de que se aloje una o dos personas.

### 3. Modelo tarifario

Todos los valores monetarios se expresan en pesos colombianos (COP). El costo de cada noche se compone de la tarifa base ajustada de habitación, la tarifa de camas según el tipo y la ocupación y, únicamente en las suites, la tarifa de minibar.

Las abreviaturas utilizadas en este modelo tarifario sirven únicamente para simplificar la visualización de las fórmulas. No deben utilizarse como identificadores en la implementación; en el código deben emplearse nombres descriptivos en inglés, de acuerdo con las convenciones de estilo del taller.

#### Tarifas de alojamiento

| Variable | Descripción | Cálculo | Valor de ejemplo |
| --- | --- | --- | ---: |
| TBH | Tarifa base de habitación por noche | Definida por el hotel | $50.000 |
| TCS | Tarifa de cama sencilla por noche | Definida por el hotel | $40.000 |
| TCD1 | Tarifa de cama doble ocupada por una persona, por noche | `TCS × 1.45` | $58.000 |
| TCD2 | Tarifa de cama doble ocupada por dos personas, por noche | `TCS × 1.90` | $76.000 |
| TPA | Tarifa por persona adicional por noche | `TCS × 0.70` | $28.000 |

Las tarifas de cama doble equivalen a `TCD1 = TCS × (1 + 45 / 100)` y `TCD2 = TCS × (1 + (2 × 45) / 100)`.

#### Recargos y servicios

El recargo por vista de frente al mar se calcula sobre TBH. Después se calcula el recargo por piso sobre RVM, aplicando el porcentaje del piso. El recargo por televisión con canales premium es un valor fijo definido por el hotel. Estos importes se suman a TBH para obtener TBA; no se aplican sobre las tarifas de camas o minibar. Si la habitación no tiene vista de frente al mar, tanto RVM como RPI son cero.

| Variable | Descripción | Cálculo | Valor de ejemplo con TBH de $50.000 |
| --- | --- | --- | ---: |
| RPI | Recargo por piso, por noche | `RVM × porcentaje del piso` | $0 / $1.500 / $3.000 con RVM de $15.000 |
| PVM | Porcentaje de recargo por vista de frente al mar | Definido por el hotel, expresado como porcentaje | 30 (30 %) |
| RVM | Recargo por vista de frente al mar, por noche | `TBH × (PVM / 100)` si tiene esa vista; cero en caso contrario | $15.000 / $0 |
| RCP | Recargo por televisión con canales premium, por noche | Valor fijo definido por el hotel si la habitación incluye este servicio; cero en caso contrario | $3.500 / $0 |
| TMI | Tarifa de minibar por suite y por noche | Definida por el hotel | $30.000 |
| TBA | Tarifa base ajustada de habitación por noche | `TBH + RPI + RVM + RCP` | Variable |

El recargo por televisión con canales premium se cobra por habitación y por noche, independientemente de la cantidad de huéspedes; por ejemplo, $3.500. Todas las suites incluyen este recargo. La tarifa de minibar es fija por suite y noche, independientemente de la cantidad de huéspedes.

| Ubicación | Porcentaje de recargo por piso sobre RVM |
| --- | ---: |
| Pisos 1 a 3 | 0 % |
| Pisos 4 a 6 | 10 % |
| Piso 7 en adelante | 20 % |

#### Variables de ocupación y reserva

| Variable | Descripción |
| --- | --- |
| NHP | Número de huéspedes de la reserva |
| CMH | Capacidad máxima de la habitación |
| NNO | Número de noches de alojamiento |
| TCA | Tarifa de camas según el tipo de habitación y su ocupación |
| CPN | Costo por noche |
| CTR | Costo total de la reserva |

Se deben cumplir `1 ≤ NHP ≤ CMH` y `NNO ≥ 1`.

#### Fórmulas por tipo de habitación

| Tipo y ocupación | Tarifa de camas (TCA) | Costo total de la reserva (CTR) |
| --- | --- | --- |
| Individual, un huésped | `TCS` | `(TBA + TCS) × NNO` |
| Doble, un huésped | `TCD1` | `(TBA + TCD1) × NNO` |
| Doble, dos huéspedes | `TCD2` | `(TBA + TCD2) × NNO` |
| Familiar, de uno a seis huéspedes | `TCD2 + 4 × TCS` | `(TBA + TCD2 + 4 × TCS) × NNO` |
| Familiar, siete u ocho huéspedes, si la capacidad lo permite | `TCD2 + 4 × TCS + (NHP − 6) × TPA` | `(TBA + TCD2 + 4 × TCS + (NHP − 6) × TPA) × NNO` |
| Suite, uno o dos huéspedes | `TCD2` | `(TBA + TCD2 + TMI) × NNO` |

La tarifa mínima de camas de la habitación familiar se cobra incluso con menos de seis huéspedes. La cama doble de la suite siempre se factura como ocupada por dos personas.

El cálculo general se realiza en tres pasos:

1. Tarifa base ajustada: `TBA = TBH + RPI + RVM + RCP`.
2. Costo por noche: `CPN = TBA + TCA + TMI_s`, donde `TMI_s` corresponde a TMI para las suites y a cero para los demás tipos.
3. Costo total: `CTR = CPN × NNO`.

#### Ejemplo consolidado en pesos colombianos (COP)

Para inicializar el hotel y realizar pruebas, pueden utilizarse TBH = $50.000, TCS = $40.000, TMI = $30.000, PVM = 30 y un recargo por televisión con canales premium de $3.500 por habitación y por noche. De estas tarifas se obtienen TCD1 = $58.000, TCD2 = $76.000 y TPA = $28.000.

Para habitaciones del piso 8, con vista de frente al mar y televisión con canales premium, en una reserva de tres noches, los recargos son:

- `RVM = $50.000 × (30 / 100) = $15.000`.
- `RPI = $15.000 × 0.20 = $3.000`.
- `RCP = $3.500`, valor fijo definido por el hotel.
- `TBA = $50.000 + $3.000 + $15.000 + $3.500 = $71.500`.

| Habitación | Huéspedes | Costo por noche | Total por tres noches |
| --- | --- | ---: | ---: |
| Individual | 1 | $111.500 | $334.500 |
| Doble | 1 | $129.500 | $388.500 |
| Doble | 2 | $147.500 | $442.500 |
| Familiar | 1 a 6 | $307.500 | $922.500 |
| Familiar | 7 | $335.500 | $1.006.500 |
| Familiar | 8 | $363.500 | $1.090.500 |
| Suite | 1 o 2 | $177.500 | $532.500 |

Los ejemplos familiares de siete y ocho huéspedes suponen habitaciones con capacidad suficiente. La suite del ejemplo debe pertenecer a un hotel en el que el piso 8 sea uno de los dos superiores.

### 4. Huéspedes

De cada huésped se registran un identificador único, nombre completo, documento de identificación, teléfono y correo electrónico. Un huésped puede existir sin reservas y puede ser responsable de varias. Cada reserva tiene un único huésped responsable.

### 5. Reservas

Cada reserva registra un identificador único, huésped responsable, habitación, cantidad de personas, cantidad de noches y estado: pendiente, confirmada o cancelada.

Se deben respetar las siguientes condiciones:

- El huésped responsable debe estar registrado.
- La habitación debe estar habilitada y no tener otra reserva pendiente o confirmada.
- La cantidad de huéspedes debe ser mayor que cero y no exceder la capacidad de la habitación.
- La cantidad de noches debe ser mayor que cero.
- Una reserva pendiente puede confirmarse o cancelarse; una confirmada puede cancelarse; una cancelada no puede confirmarse nuevamente.
- Cancelar una reserva libera la habitación para nuevas reservas, siempre que esté habilitada.

El costo de la reserva se calcula según la ubicación, el tipo de habitación, la cantidad de huéspedes y las noches. **No se utilizarán fechas de entrada y salida ni calendarios**: para efectos del taller, una reserva pendiente o confirmada ocupa la habitación hasta que sea cancelada.

### 6. Comprobantes

Al confirmar una reserva se genera un único comprobante, con número único, identificador de la reserva, nombre del huésped responsable, número de habitación, cantidad de noches y costo total del alojamiento.

El comprobante pertenece exclusivamente a la reserva que lo originó y se conserva incluso si posteriormente se cancela la reserva. El sistema debe permitir consultar un comprobante por su número único. La estrategia para localizarlo forma parte de las decisiones de diseño del desarrollador.

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
6. Elaborar en papel el diagrama de clases UML.

El desarrollador presentará y justificará su diagrama ante el jefe de proyectos. Deberá explicar cómo el diseño satisface las reglas del negocio. Se aceptan distintas soluciones justificadas; no existe un único diagrama obligatorio. No se establece una cantidad mínima, máxima ni aproximada de clases: cada clase deberá responder a una responsabilidad identificable y justificarse durante la revisión técnica.

**Es indispensable obtener la aprobación del diseño antes de iniciar la implementación.**

---

## Parte II. Implementación y validación en Java

### 2A. Implementación del paquete `model`

Implementar el modelo de acuerdo con el diagrama UML aprobado. El código deberá:

- Aplicar encapsulamiento y validar los datos para preservar las reglas del negocio.
- Implementar correctamente las relaciones entre objetos y mantener la consistencia de las relaciones bidireccionales.
- Utilizar herencia, sobrescritura y polimorfismo de forma coherente con el diseño.
- Calcular los costos sin trasladar las reglas del negocio al programa de pruebas.
- Lanzar excepciones cuando se incumplan las restricciones; las clases del modelo no deben imprimir mensajes en consola ni solicitar datos al usuario.

### 2B. Esquema del hotel e implementación del paquete `view`

**Diseño físico individual.** Cada desarrollador diseñará su propio hotel y presentará un esquema visual de la torre, que muestre:

- Nombre del hotel y cantidad total de pisos (mínimo ocho).
- Distribución de habitaciones por piso, con número y tipo de habitación.
- Orientación de cada habitación: con vista de frente al mar o sin vista de frente al mar.
- Configuración de camas en las habitaciones familiares.

Los diseños de los desarrolladores deberán ser diferentes y cumplir las mismas reglas del negocio. El esquema se presentará y justificará ante el jefe de proyectos y deberá corresponder a los objetos que posteriormente se creen en Java.

**Inicialización y pruebas.** Dentro del paquete `view`, implementar una clase `Main` que:

1. Cree un único hotel con las características de su esquema, las tarifas TBH, TCS y TMI, el porcentaje PVM, el valor fijo del recargo por televisión con canales premium y las políticas de recargos del modelo tarifario.
2. Cree y registre las habitaciones diseñadas, con sus pisos, orientación, camas y características, utilizando las tarifas y políticas de recargos establecidas en el hotel.
3. Registre huéspedes y realice reservas con distintas cantidades de personas y noches.
4. Calcule y muestre tarifas que permitan verificar los recargos por ubicación y las reglas específicas de cada tipo de habitación.
5. Confirme y cancele reservas, y consulte comprobantes por su número único.
6. Pruebe situaciones inválidas y controle las excepciones lanzadas por el modelo, mostrando los resultados por consola.

`Main` será únicamente el punto de entrada y escenario de validación: no deberá duplicar los cálculos tarifarios ni las reglas del dominio. **No se requiere interfaz gráfica.**

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

- Lenguaje: Java.
- Identificadores del código en inglés: `UpperCamelCase` para clases y `lowerCamelCase` para atributos y métodos.
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
| Televisión con canales premium | Television with premium channels | Noche | Night |
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
