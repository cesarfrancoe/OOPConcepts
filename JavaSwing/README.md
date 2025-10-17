# Tutorial: Java Swing con Capas, Eventos y Construcción Progresiva

## Estructura del proyecto

```
SwingApp
└── src
    ├── domain
    │   └── Person.java
    ├── ui
    │   ├── MainWindow.java
    │   └── SecondWindow.java
    └── App.java
```

---

## PARTE 1: MODELO Y PRIMERA VENTANA

### Capa DOMAIN – Clase `Person`

Archivo: `src/domain/Person.java`

```java
package domain;

// Code block #1
public class Person {

    // Code block #2
    // Code block #3
}
```

#### Paso 1 – Reemplaza `// Code block #2`
Atributos:

```java
private String name;
private int age;
```

#### Paso 2 – Reemplaza `// Code block #3`
Constructor y getters:

```java
public Person(String name, int age) {
    this.name = name;
    this.age = age;
}

public String getName() { return name; }
public int getAge() { return age; }
```

La clase `Person` (capa Domain) compila correctamente.

---

### Capa UI – Clase `MainWindow`

Archivo: `src/ui/MainWindow.java`

```java
package ui;

// Code block #4
public class MainWindow extends JFrame {

    // Code block #5

    public MainWindow() {
        // Code block #6
    }

    // Code block #7
    // Code block #8
    // Code block #9
}
```

#### Paso 3 – Reemplaza `// Code block #4`
Importaciones necesarias:

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
```

#### Paso 4 – Reemplaza `// Code block #5`
Atributos de instancia:

```java
private JTextField txtName;
private JTextField txtAge;
private JButton btnSend;
private JLabel lblMessage;
private JPanel pnlMain;
```

#### Paso 5 – Reemplaza `// Code block #7`
Definir los métodos vacíos `initComponents()` e `initEvents()` (bloque completo reemplazado):

```java
private void initComponents() {
    // components will be defined later
}

private void initEvents() {
    // event listeners will be added later
}
```

#### Paso 6 – Reemplaza `// Code block #6`
Constructor que llama los métodos definidos:

```java
setTitle("Main Window");
setSize(400, 250);
setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

initComponents();
initEvents();

setVisible(true);
```

#### Paso 7 – Implementar el método `initComponents()`

```java
private void initComponents() {
    pnlMain = new JPanel();
    pnlMain.setLayout(new GridLayout(4, 1, 5, 5));

    txtName = new JTextField("Enter your name");
    txtAge = new JTextField("Enter your age");
    btnSend = new JButton("Send Info");
    lblMessage = new JLabel("", SwingConstants.CENTER);

    pnlMain.add(txtName);
    pnlMain.add(txtAge);
    pnlMain.add(btnSend);
    pnlMain.add(lblMessage);

    add(pnlMain);
}
```

#### Paso 8 – Reemplaza `// Code block #8`
Agregar la importación del dominio y una versión temporal del evento.

```java
import domain.Person;
```

```java
private void initEvents() {
    btnSend.addActionListener(e -> onSendButtonClick());
}

// temporary placeholder
private void onSendButtonClick() {
    JOptionPane.showMessageDialog(this, "Send button clicked!");
}
```

En este punto, al ejecutar el programa y hacer clic en “Send Info”, aparece un mensaje.

#### Paso 9 – Reemplazo definitivo del método `onSendButtonClick()`

```java
private void onSendButtonClick() {
    var name = txtName.getText().trim();
    var ageText = txtAge.getText().trim();

    if (name.isEmpty() || ageText.isEmpty()) {
        JOptionPane.showMessageDialog(
            this,
            "Please enter both name and age.",
            "Input Error",
            JOptionPane.WARNING_MESSAGE
        );
        return;
    }

    try {
        var age = Integer.parseInt(ageText);
        var person = new Person(name, age);
        new SecondWindow(person);
    } catch (NumberFormatException ex) {
        JOptionPane.showMessageDialog(
            this,
            "Age must be a valid number.",
            "Format Error",
            JOptionPane.ERROR_MESSAGE
        );
    }
}
```

#### Paso 10 – Agregar método `main()`

```java
public static void main(String[] args) {
    SwingUtilities.invokeLater(() -> {
        MainWindow mainWindow = new MainWindow();
    });
}
```

---

## PARTE 2: SEGUNDA VENTANA

Archivo: `src/ui/SecondWindow.java`

```java
package ui;

// Code block #10
public class SecondWindow extends JFrame {

    // Code block #11

    public SecondWindow(Person person) {
        // Code block #12
    }

    // Code block #13
    // Code block #14
    // Code block #15
}
```

#### Paso 11 – Reemplaza `// Code block #10`
Importaciones necesarias:

```java
import javax.swing.*;
import java.awt.*;
```

#### Paso 12 – Reemplaza `// Code block #11`
Atributos (incluye `Person` como atributo de instancia):

```java
private Person person;
private JLabel lblInfo;
private JPanel pnlContainer;
private JButton btnClose;
```

#### Paso 13 – Reemplaza `// Code block #13`
Definir los métodos vacíos `initComponents()` e `initEvents()` (bloque completo reemplazado):

```java
private void initComponents() {
    // components will be defined later
}

private void initEvents() {
    // event listeners will be added later
}
```

#### Paso 14 – Reemplaza `// Code block #12`
Constructor que llama los métodos definidos:

```java
this.person = person;
setTitle("Second Window");
setSize(300, 200);
setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);

initComponents();
initEvents();

setVisible(true);
```

#### Paso 15 – Reemplaza `// Code block #14`
Agregar la importación `domain.Person`:

```java
import domain.Person;
```

#### Paso 16 – Reemplaza `// Code block #15`
Implementar los métodos `initComponents()` e `initEvents()`:

```java
private void initComponents() {
    pnlContainer = new JPanel(new BorderLayout(10, 10));

    var text = "<html><h3>Received Information</h3>" +
               "<p>Name: " + person.getName() + "</p>" +
               "<p>Age: " + person.getAge() + "</p></html>";

    lblInfo = new JLabel(text, SwingConstants.CENTER);
    btnClose = new JButton("Close");

    pnlContainer.add(lblInfo, BorderLayout.CENTER);
    pnlContainer.add(btnClose, BorderLayout.SOUTH);

    add(pnlContainer);
}

private void initEvents() {
    btnClose.addActionListener(e -> onCloseButtonClick());
}

private void onCloseButtonClick() {
    dispose();
}
```

---

## PARTE 3: COMUNICACIÓN BIDIRECCIONAL

### Paso 17 – Cambios en `MainWindow`

Reemplazar en `onSendButtonClick()` la creación de la segunda ventana:

```java
SecondWindow second = new SecondWindow(this, person);
```

Agregar método para actualizar los campos:

```java
public void updateFields(Person updatedPerson) {
    txtName.setText(updatedPerson.getName());
    txtAge.setText(String.valueOf(updatedPerson.getAge()));
    lblMessage.setText("Data updated successfully!");
}
```

### Paso 18 – Cambios en `SecondWindow`

Reemplazar constructor:

```java
private MainWindow mainWindow;

public SecondWindow(MainWindow mainWindow, Person person) {
    this.mainWindow = mainWindow;
    this.person = person;

    setTitle("Edit Person Data");
    setSize(350, 250);
    setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);

    initComponents();
    initEvents();

    setVisible(true);
}
```

Modificar `initComponents()`:

```java
private JTextField txtName;
private JTextField txtAge;
private JButton btnSave;
private JPanel pnlForm;

private void initComponents() {
    pnlForm = new JPanel(new GridLayout(3, 2, 8, 8));

    pnlForm.add(new JLabel("Name:"));
    txtName = new JTextField(person.getName());
    pnlForm.add(txtName);

    pnlForm.add(new JLabel("Age:"));
    txtAge = new JTextField(String.valueOf(person.getAge()));
    pnlForm.add(txtAge);

    btnSave = new JButton("Save and Return");
    pnlForm.add(new JLabel());
    pnlForm.add(btnSave);

    add(pnlForm, BorderLayout.CENTER);
}
```

Modificar `initEvents()` y agregar `onSaveButtonClick()`:

```java
private void initEvents() {
    btnSave.addActionListener(e -> onSaveButtonClick());
}

private void onSaveButtonClick() {
    try {
        var newName = txtName.getText().trim();
        var newAge = Integer.parseInt(txtAge.getText().trim());

        if (newName.isEmpty()) {
            JOptionPane.showMessageDialog(this, "Name cannot be empty.", "Validation", JOptionPane.WARNING_MESSAGE);
            return;
        }

        person.setName(newName);
        person.setAge(newAge);

        JOptionPane.showMessageDialog(this, "Changes saved successfully!", "Confirmation", JOptionPane.INFORMATION_MESSAGE);

        mainWindow.updateFields(person);
        dispose();

    } catch (NumberFormatException ex) {
        JOptionPane.showMessageDialog(this, "Age must be a number.", "Error", JOptionPane.ERROR_MESSAGE);
    }
}
```

### Paso 19 – Agregar setters en `Person`

```java
public void setName(String name) {
    this.name = name;
}

public void setAge(int age) {
    this.age = age;
}
```

---

## Paso 20 – Clase `App`

Archivo: `src/App.java`

```java
import ui.MainWindow;
import javax.swing.SwingUtilities;

public class App {
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            MainWindow mainWindow = new MainWindow();
        });
    }
}
```

---

## Conceptos reforzados

| Principio | Aplicación |
|------------|-------------|
| Separación por capas | `domain` (modelo) y `ui` (interfaz) |
| Progresividad | Métodos vacíos primero, implementación después |
| Prototipado incremental | Uso temporal de `JOptionPane` antes de la lógica final |
| Comunicación bidireccional | `SecondWindow` modifica el mismo objeto `Person` |
| Encapsulamiento | Setters y getters en el modelo |
| Responsabilidad única | `Person` gestiona datos, `MainWindow` y `SecondWindow` manejan interfaz |

---

## Resultado final

1. `MainWindow` permite ingresar los datos de una persona.  
2. Al presionar **“Send Info”**, se abre `SecondWindow`.  
3. `SecondWindow` muestra y permite editar el nombre y la edad.  
4. Al presionar **“Save and Return”**, los cambios se aplican al mismo objeto.  
5. `MainWindow` actualiza sus campos al cerrarse `SecondWindow`.

