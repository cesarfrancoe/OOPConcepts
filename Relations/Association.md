# Asociación

## Prerrequisito

[Fundamentos de relaciones en UML](UMLBasics.md)

## Definición

La asociación es una relación entre clases en la cual un objeto **conoce o utiliza a otro**, sin ser responsable de su creación ni de su ciclo de vida.

Es la relación más básica en POO y se utiliza cuando se requiere establecer un vínculo lógico entre objetos sin implicar propiedad.

En UML, se representa mediante **una línea con dirección (flecha) y sin símbolos adicionales**.

## Características

* No hay dependencia del ciclo de vida
* No existe relación de propiedad
* Puede ser unidireccional o bidireccional
* Puede ser 1:1, 1:N o N:N
* Bajo acoplamiento

---

## Asociación uno a uno (1:1)

---

### Representación UML (unidireccional)

```text
Person --------> Passport
   1               0..1
```

### Implementación (unidireccional)

```java
public class Passport {
    private String number;

    public Passport(String number) {
        this.number = number;
    }

    public String getNumber() {
        return number;
    }
}
```

```java
public class Person {
    private String name;
    private Passport passport;

    public Person(String name, Passport passport) {
        this.name = name;
        this.passport = passport;
    }

    public Passport getPassport() {
        return passport;
    }
}
```

### Test (unidireccional)

```java
public class TestPerson {
    public static void main(String[] args) {
        Passport passport = new Passport("A1234567");
        Person person = new Person("Jane", passport);

        System.out.println("Pasaporte: " + person.getPassport().getNumber());
    }
}
```

---

### Representación UML (bidireccional)

```text
Person <--------> Passport
   1               0..1
```

### Implementación (bidireccional)

```java
public class Passport {
    private String number;
    private Person person;

    public Passport(String number) {
        this.number = number;
    }

    public String getNumber() {
        return number;
    }

    public Person getPerson() {
        return person;
    }

    public void setPerson(Person newPerson) {
        this.person = newPerson;
    }
}
```

```java
public class Person {
    private String name;
    private Passport passport;

    public Person(String name) {
        this.name = name;
    }

    public void setPassport(Passport passport) {
        this.passport = passport;
        if (passport != null && passport.getPerson() != this) {
            passport.setPerson(this);
        }
    }

    public Passport getPassport() {
        return passport;
    }
}
```

### Test (bidireccional)

```java
public class TestPersonBidirectional {
    public static void main(String[] args) {
        Person person = new Person("Jane");
        Passport passport = new Passport("A1234567");

        person.setPassport(passport);

        System.out.println("Persona -> Pasaporte: " + person.getPassport().getNumber());
        System.out.println("Pasaporte -> Persona: " + passport.getPerson());
    }
}
```

---

## Asociación uno a muchos (1:N)

### Representación UML (unidireccional)

```text
School --------> Teacher
   1              0..*
```

### Implementación (unidireccional)

```java
public class Teacher {
    private String name;

    public Teacher(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

```java
import java.util.List;

public class School {
    private List<Teacher> teachers;

    public School(List<Teacher> teachers) {
        this.teachers = teachers;
    }

    public List<Teacher> getTeachers() {
        return teachers;
    }
}
```

### Test (unidireccional)

```java
import java.util.ArrayList;
import java.util.List;

public class TestSchool {
    public static void main(String[] args) {
        List<Teacher> teachers = new ArrayList<>();
        teachers.add(new Teacher("John"));
        teachers.add(new Teacher("Jane"));

        School school = new School(teachers);

        for (Teacher t : school.getTeachers()) {
            System.out.println("Docente: " + t.getName());
        }
    }
}
```

### Representación UML (bidireccional)

```text
School <--------> Teacher
   1              0..*
```

### Implementación (bidireccional)

```java
public class Teacher {
    private String name;
    private School school;

    public Teacher(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public School getSchool() {
        return school;
    }

    public void setSchool(School newSchool) {
        this.school = newSchool;
    }
}
```

```java
import java.util.ArrayList;
import java.util.List;

public class School {
    private List<Teacher> teachers;

    public School() {
        this.teachers = new ArrayList<>();
    }

    public List<Teacher> getTeachers() {
        return teachers;
    }

    public void addTeacher(Teacher teacher) {
        if (teacher != null && !teachers.contains(teacher)) {
            teachers.add(teacher);

            if (teacher.getSchool() != this) {
                teacher.setSchool(this);
            }
        }
    }

    public void removeTeacher(Teacher teacher) {
        if (teacher != null && teachers.contains(teacher)) {
            teachers.remove(teacher);

            if (teacher.getSchool() == this) {
                teacher.setSchool(null);
            }
        }
    }
}
```

### Test (bidireccional)

```java
public class TestSchoolBidirectional {
    public static void main(String[] args) {
        School school = new School();

        Teacher t1 = new Teacher("John");
        Teacher t2 = new Teacher("Jane");

        school.addTeacher(t1);
        school.addTeacher(t2);

        for (Teacher t : school.getTeachers()) {
            System.out.println("Docente: " + t.getName());
        }

        System.out.println("Escuela de John: " + t1.getSchool());
    }
}
```

---

## Asociación muchos a muchos (N:N)

### Representación UML (bidireccional)

```text
Student <--------> Course
   0..*             0..*
```

### Implementación

```java
import java.util.List;

public class Student {
    private String name;
    private List<Course> courses;

    public Student(String name, List<Course> courses) {
        this.name = name;
        this.courses = courses;
    }

    public List<Course> getCourses() {
        return courses;
    }
}
```

```java
import java.util.List;

public class Course {
    private String title;
    private List<Student> students;

    public Course(String title, List<Student> students) {
        this.title = title;
        this.students = students;
    }

    public List<Student> getStudents() {
        return students;
    }
}
```

### Test

```java
import java.util.ArrayList;
import java.util.List;

public class TestManyToMany {
    public static void main(String[] args) {
        Student s1 = new Student("Ana", new ArrayList<>());
        Student s2 = new Student("Luis", new ArrayList<>());

        List<Student> students = new ArrayList<>();
        students.add(s1);
        students.add(s2);

        Course course = new Course("POO", students);

        System.out.println("Estudiantes en el curso:");
        for (Student s : course.getStudents()) {
            System.out.println(s);
        }
    }
}
```

## Consideración importante

En muchos sistemas reales, una relación muchos a muchos se transforma en una **clase intermedia**.

```text
Student --------> Enrollment <-------- Course
```

Esto permite:

* Agregar atributos a la relación (nota, fecha, estado)
* Tener mayor control del modelo

## Conclusión

La asociación se utiliza cuando:

* Solo se requiere que una clase conozca a otra
* No existe dependencia de ciclo de vida
* No hay relación de propiedad

Es la relación más flexible y la base para modelar interacciones entre objetos.
