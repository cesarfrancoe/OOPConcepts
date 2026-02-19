# Git: Fundamentos, Funcionamiento y Plataformas en la Nube

## 1. Introducción

Git es actualmente el sistema de control de versiones más utilizado en el desarrollo de software. Constituye una herramienta esencial para el trabajo colaborativo, la trazabilidad de cambios y la gestión estructurada del ciclo de vida del código. Sobre Git se han construido diversas plataformas en la nube que amplían sus capacidades mediante servicios de colaboración, automatización e integración continua.

---

## 2. ¿Qué es Git?

Git es un sistema de control de versiones distribuido (DVCS) creado en 2005 por Linus Torvalds para gestionar el desarrollo del kernel de Linux.

Su función principal es registrar los cambios realizados en archivos a lo largo del tiempo, permitiendo:

* Control de versiones.
* Trabajo colaborativo concurrente.
* Recuperación de versiones anteriores.
* Gestión de ramas de desarrollo.
* Auditoría y trazabilidad de modificaciones.

A diferencia de los sistemas centralizados tradicionales, Git es distribuido: cada desarrollador posee una copia completa del repositorio, incluyendo todo el historial.

---

## 3. Conceptos Fundamentales

### 3.1 Repositorio

Es la base de datos que almacena el historial del proyecto. Puede ser:

* Local: ubicado en la máquina del desarrollador.
* Remoto: alojado en un servidor o plataforma en la nube.

---

### 3.2 Commit

Un commit es una instantánea del estado del proyecto en un momento determinado. Cada commit contiene:

* Cambios realizados.
* Autor.
* Fecha.
* Mensaje descriptivo.
* Identificador único (hash criptográfico).

Internamente, Git organiza los commits como un grafo acíclico dirigido (DAG).

---

### 3.3 Ramas (Branches)

Una rama es un puntero móvil a una secuencia de commits. Permite desarrollar nuevas funcionalidades sin afectar la línea principal del proyecto (generalmente `main`).

---

### 3.4 Merge

Proceso mediante el cual se integran cambios provenientes de distintas ramas.

---

### 3.5 Área de Preparación (Staging Area)

Zona intermedia donde se registran los cambios antes de confirmarlos mediante un commit.

---

## 4. Flujo Básico de Trabajo en Git

El flujo operativo estándar es:

1. Modificación de archivos.
2. `git add` → envío de cambios al staging.
3. `git commit` → creación de nueva instantánea.
4. `git push` → envío al repositorio remoto.
5. `git pull` → actualización desde el repositorio remoto.

Este modelo permite trabajo offline y sincronización posterior.

---

## 5. Principales Plataformas en la Nube Basadas en Git

Git es la tecnología subyacente. Las siguientes plataformas proporcionan infraestructura remota y herramientas complementarias.

---

### GitHub

Propiedad de Microsoft, es la plataforma más utilizada globalmente.

Características:

* Repositorios públicos y privados.
* Pull Requests para revisión de código.
* Gestión de incidencias (Issues).
* Automatización con GitHub Actions (CI/CD).
* Ecosistema colaborativo amplio.

---

### GitLab

Enfoque integral DevOps.

Características:

* CI/CD integrado.
* Implementación en la nube o self-hosted.
* Gestión completa del ciclo de vida del software.
* Control avanzado de permisos.

---

### Bitbucket

Desarrollado por Atlassian.

Características:

* Integración con Jira y Confluence.
* Repositorios privados empresariales.
* Integración continua mediante Pipelines.

---

## 6. Relación Conceptual entre Git y las Plataformas

* Git es el sistema de control de versiones.
* GitHub, GitLab y Bitbucket son plataformas que utilizan Git como motor.
* Estas plataformas no reemplazan Git; lo complementan con herramientas de colaboración y automatización.

---

## 7. Creación de Cuenta en GitHub con Correo Institucional (@ucaldas.edu.co)

GitHub ofrece beneficios académicos mediante GitHub Education y el GitHub Student Developer Pack.

---

### 7.1 Registro Inicial

1. Ingresar a [https://github.com](https://github.com)
2. Seleccionar “Sign up”.
3. Registrar el correo institucional: [nombre@ucaldas.edu.co](mailto:nombre@ucaldas.edu.co)
4. Crear usuario y contraseña.
5. Confirmar el correo desde el mensaje recibido.

Se recomienda utilizar el correo institucional desde el inicio para facilitar la verificación.

---

### 7.2 Solicitud de Beneficios Educativos

1. Acceder a [https://education.github.com](https://education.github.com)
2. Iniciar sesión.
3. Solicitar acceso como estudiante o docente.
4. Completar el proceso de verificación académica.

GitHub puede solicitar documentación que acredite vinculación institucional.

---

### 7.3 Beneficios Obtenidos

Una vez aprobado:

* GitHub Pro sin costo mientras la condición académica esté vigente.
* Acceso al Student Developer Pack.
* Herramientas premium de desarrollo.
* Créditos y servicios tecnológicos asociados.

---

### 7.4 Buenas Prácticas

* Activar autenticación de dos factores (2FA).
* Mantener actualizada la afiliación institucional.
* Separar proyectos académicos y personales cuando sea pertinente.

---

## 8. Conclusiones

Git es una infraestructura fundamental para el desarrollo moderno de software, basada en un modelo distribuido eficiente y robusto. Las plataformas en la nube como GitHub, GitLab y Bitbucket amplían sus capacidades mediante servicios colaborativos y automatización DevOps.

En el contexto académico, el uso de cuentas institucionales permite acceder a beneficios adicionales que fortalecen la formación técnica y el desarrollo profesional.
