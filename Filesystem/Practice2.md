## Práctica: Almacenamiento de objetos en archivos

### 1. Objetivo

Implementar un sistema que permita registrar empleados, mostrarlos, buscarlos por ID, guardarlos y cargarlos desde archivos, aplicando:

* Principios de Programación Orientada a Objetos.
* Separación de capas (`Domain`, `Data`, `UI`, `Utils`).
* Serialización de objetos.
* Manejo centralizado de entrada y salida a través de una clase auxiliar `Console`.

---

### 2. Estructura del proyecto

```
src/
 ├── data/
 │    └── EnterpriseStorage.java
 ├── domain/
 │    ├── Employee.java
 │    └── Enterprise.java
 ├── ui/
 │    └── Main.java
 └── utils/
      └── Console.java
```

---

### 3. Implementación por capas

---

#### Capa DOMAIN

**Archivo:** `domain/Employee.java`

```java
package domain;
import java.io.Serializable;

// Represents an employee in the company
public class Employee implements Serializable {
    private int id;
    private String name;
    private double salary;

    public Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    public int getId() { return id; }
    public String getName() { return name; }
    public double getSalary() { return salary; }

    @Override
    public String toString() {
        return "Employee{id=" + id +
                ", name='" + name + '\'' +
                ", salary=" + salary + '}';
    }
}
```

---

**Archivo:** `domain/Enterprise.java`

```java
package domain;
import java.io.Serializable;
import java.util.ArrayList;
import java.util.List;

// Represents an enterprise that contains multiple employees
public class Enterprise implements Serializable {
    private String name;
    private List<Employee> employees;

    public Enterprise(String name) {
        this.name = name;
        this.employees = new ArrayList<>();
    }

    public String getName() { return name; }

    public void addEmployee(Employee e) {
        employees.add(e);
    }

    public void showEmployees() {
        if (employees.isEmpty()) {
            System.out.println("No employees registered yet.");
        } else {
            for (Employee e : employees) {
                System.out.println(e);
            }
        }
    }

    // Find employee by ID
    public Employee findEmployeeById(int id) {
        for (Employee e : employees) {
            if (e.getId() == id) {
                return e;
            }
        }
        return null; // Not found
    }
}
```

---

#### Capa DATA

**Archivo:** `data/EnterpriseStorage.java`

```java
package data;
import domain.Enterprise;
import java.io.*;

// Handles saving and loading Enterprise objects from files
public class EnterpriseStorage {

    public static void save(Enterprise enterprise, String filename) {
        try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(filename))) {
            out.writeObject(enterprise);
            System.out.println("Enterprise data saved successfully.");
        } catch (IOException e) {
            System.err.println("Error saving enterprise data: " + e.getMessage());
        }
    }

    public static Enterprise load(String filename) {
        try (ObjectInputStream in = new ObjectInputStream(new FileInputStream(filename))) {
            return (Enterprise) in.readObject();
        } catch (IOException | ClassNotFoundException e) {
            System.err.println("Error loading enterprise data: " + e.getMessage());
            return null;
        }
    }
}
```

---

#### Capa UTILS

**Archivo:** `utils/Console.java`

```java
package utils;
import java.util.Scanner;

// Utility class for handling console input and output
public class Console {
    private static final Scanner scanner = new Scanner(System.in);

    // Writes a message or object followed by a new line
    public static void writeLine(Object message) {
        System.out.println(message);
    }

    // Reads a line of text after showing a prompt message
    public static String readLine(String message) {
        System.out.print(message);
        return scanner.nextLine();
    }
}
```

---

#### Capa UI

**Archivo:** `ui/Main.java`

```java
package ui;
import domain.*;
import data.EnterpriseStorage;
import utils.Console;

public class Main {

    private static final String FILE_NAME = "enterprise.dat";
    private static Enterprise enterprise = new Enterprise("TechSoft");

    public static void main(String[] args) {
        int option;

        do {
            showMenu();
            option = Integer.parseInt(Console.readLine("Select an option: "));

            switch (option) {
                case 1 -> addEmployee();
                case 2 -> showEmployees();
                case 3 -> findEmployee();
                case 4 -> saveEnterprise();
                case 5 -> loadEnterprise();
                case 6 -> Console.writeLine("Exiting system...");
                default -> Console.writeLine("Invalid option. Try again.");
            }
        } while (option != 6);
    }

    private static void showMenu() {
        Console.writeLine("\n===== ENTERPRISE MENU =====");
        Console.writeLine("1. Add Employee");
        Console.writeLine("2. Show Employees");
        Console.writeLine("3. Find Employee by ID");
        Console.writeLine("4. Save to File");
        Console.writeLine("5. Load from File");
        Console.writeLine("6. Exit");
        Console.writeLine("============================");
    }

    private static void addEmployee() {
        int id = Integer.parseInt(Console.readLine("Enter employee ID: "));
        String name = Console.readLine("Enter employee name: ");
        double salary = Double.parseDouble(Console.readLine("Enter employee salary: "));

        var employee = new Employee(id, name, salary);
        enterprise.addEmployee(employee);
        Console.writeLine("Employee added successfully!");
    }

    private static void showEmployees() {
        Console.writeLine("\n=== Employee List ===");
        enterprise.showEmployees();
    }

    private static void findEmployee() {
        int id = Integer.parseInt(Console.readLine("Enter employee ID to search: "));
        var found = enterprise.findEmployeeById(id);

        if (found != null) {
            Console.writeLine("Employee found: " + found);
        } else {
            Console.writeLine("No employee found with ID " + id);
        }
    }

    private static void saveEnterprise() {
        EnterpriseStorage.save(enterprise, FILE_NAME);
    }

    private static void loadEnterprise() {
        var loaded = EnterpriseStorage.load(FILE_NAME);
        if (loaded != null) {
            enterprise = loaded;
            Console.writeLine("Enterprise loaded successfully!");
        }
    }
}
```

---

### 4. Ejemplo de ejecución

```
===== ENTERPRISE MENU =====
1. Add Employee
2. Show Employees
3. Find Employee by ID
4. Save to File
5. Load from File
6. Exit
============================
Select an option: 1
Enter employee ID: 101
Enter employee name: Alice
Enter employee salary: 2500
Employee added successfully!

Select an option: 3
Enter employee ID to search: 101
Employee found: Employee{id=101, name='Alice', salary=2500.0}

Select an option: 4
Enterprise data saved successfully.

Select an option: 6
Exiting system...
```

---

### 5. Actividades complementarias

1. Agrega la opción **7. Eliminar empleado por ID**.
2. Implementa validación para evitar **IDs duplicados**.
3. Permite **editar el salario** de un empleado existente.
4. Automáticamente cargar (al iniciar) y guardar (al salir) los datos.
