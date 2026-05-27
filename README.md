# Sistema de Control de Prácticas — HUSRT

Sistema web para gestión de estudiantes en prácticas del Hospital Universitario San Rafael de Tunja.

---

## Tecnologías utilizadas

| Tecnología | Rol en el proyecto |
|---|---|
| ![Java](https://img.shields.io/badge/Java%2017-ED8B00?style=flat&logo=openjdk&logoColor=white) | Lenguaje del backend |
| ![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=flat&logo=springboot&logoColor=white) | Framework REST API |
| ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white) | Base de datos relacional |
| ![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=flat&logo=supabase&logoColor=white) | Hosting de la base de datos en la nube |
| ![React](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black) | Framework del frontend |
| ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white) | Tipado estático en el frontend |
| ![Git](https://img.shields.io/badge/Git-F05032?style=flat&logo=git&logoColor=white) | Control de versiones |
| ![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white) | Repositorio remoto |
| ![draw.io](https://img.shields.io/badge/draw.io-F08705?style=flat&logo=diagramsdotnet&logoColor=white) | Diagramas y modelado |
| ![Word](https://img.shields.io/badge/Microsoft%20Word-2B579A?style=flat&logo=microsoftword&logoColor=white) | Documentación del proyecto |

---

## Vista previa del proyecto

| Login | Dashboard |
|---|---|
| <img width="400" src="https://github.com/user-attachments/assets/6db452a4-7a44-4b67-9f0f-58e08b28f074" /> | <img width="400" src="https://github.com/user-attachments/assets/6cccf937-29cb-4eb5-a1d2-f728507ab100" alt="Dashboard"/> |

| Presencia de estudiantes | Gestión de horarios |
|---|---|
| <img width="400" src="https://github.com/user-attachments/assets/93748bfe-cf8d-4de6-8566-70f8f1cfc51a" alt="Registro de estudiantes"/> | <img width="400" src="https://github.com/user-attachments/assets/6f321b84-3435-4c97-a8e8-5dd27deb3016" alt="Gestión de horarios"/> |

| Registro Estudiantes | Cronograma |
|---|---|
| <img width="400" src="https://github.com/user-attachments/assets/36efd486-9b77-464e-b64a-33925193dfb4" alt="Cronograma"/> | <img width="400" src="https://github.com/user-attachments/assets/8aa08c5c-a676-44e9-85a2-4d72746ff28a" alt="Presencia"/> |

---

## Requisitos previos

Antes de correr el proyecto, asegúrate de tener instalado:

| Herramienta | Versión recomendada | Cómo verificar |
|---|---|---|
| Java JDK | 17 | `java -version` |
| Maven | 3.8+ (o usar el wrapper incluido) | `mvn -version` |
| Node.js | 18 o 20 LTS | `node -v` |
| npm | 9+ (viene con Node) | `npm -v` |

> **¿No tienes Node.js?** Descárgalo desde https://nodejs.org — elige la versión **LTS**.  
> **¿No tienes Java 17?** Descárgalo desde https://adoptium.net

---

## Configuración de la base de datos

El proyecto se conecta a una base de datos PostgreSQL en Supabase.  
Las credenciales **no están en el repositorio** por seguridad. Debes editar el archivo de configuración localmente.

Abre el archivo `backend/src/main/resources/application.properties` y reemplaza su contenido con las credenciales reales que te comparta el equipo:

```properties
spring.datasource.url=jdbc:postgresql://SERVIDOR:5432/postgres?user=USUARIO&password=CONTRASEÑA
spring.datasource.username=USUARIO
spring.datasource.password=CONTRASEÑA
spring.datasource.driver-class-name=org.postgresql.Driver
spring.h2.console.enabled=false
spring.sql.init.mode=never
server.port=8080
spring.application.name=husrt-control-USTA
```

---

## Cómo correr el proyecto

### 1. Backend (Spring Boot)

```bash
cd backend

# En Windows:
mvnw.cmd spring-boot:run

# En Mac / Linux:
./mvnw spring-boot:run
```

El backend queda corriendo en: `http://localhost:8080`

---

### 2. Frontend (React + Vite)

```bash
cd frontend

# Instalar dependencias (solo la primera vez)
npm install --legacy-peer-deps

# Correr en modo desarrollo
npm run dev
```

El frontend queda en: `http://localhost:5173`

> **¿Por qué `--legacy-peer-deps`?**  
> Este proyecto usa varias librerías de Radix UI y otras que declaran versiones de React
> de forma estricta. A partir de npm 7, esos conflictos bloquean la instalación por defecto.
> El flag `--legacy-peer-deps` le dice a npm que ignore esos conflictos de versiones y proceda,
> tal como lo hacía npm 6. Es el comportamiento correcto para este proyecto y no representa
> un riesgo de seguridad adicional — las versiones quedan fijadas exactamente por el archivo
> `package-lock.json` incluido en el repositorio.

---

## Estructura del proyecto

```
/
├── backend/          ← API REST con Spring Boot (Java 17)
│   ├── src/
│   └── pom.xml
├── frontend/         ← Interfaz con React + TypeScript + Vite
│   ├── src/
│   └── package.json
└── README.md
```

---

## Credenciales de prueba

| Usuario | Cédula | Contraseña | Rol |
|---|---|---|---|
| Administrador | `1234567890` | `admin2026` | Acceso total al sistema |
| Médico | `0987` | `hola:)` | Vista de presencia, horarios y reportes |
| Estudiante (completo) | `1234567899` | `1234567899` | Dashboard de estudiante |
| Estudiante (incompleto) | `12345` | `123456` | Perfil sin completar |

---

## Solución de problemas frecuentes

### `npm install --legacy-peer-deps` da error de permisos en Windows

Abre PowerShell **como administrador** y ejecuta una sola vez:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

Luego vuelve a correr `npm install --legacy-peer-deps` normalmente.

---

### La instalación es muy lenta

Si ya corriste `npm install --legacy-peer-deps` antes, puedes usar la caché local:

```bash
npm install --legacy-peer-deps --prefer-offline
```

Si es la primera vez, la descarga puede tardar 2–5 minutos según la conexión. Es normal — son más de 40 librerías de UI (Radix UI, Tailwind, Recharts, etc.).

---

### `node_modules` ya existe y hay errores raros

Borra todo y vuelve a instalar desde cero:

```bash
# En Mac / Linux:
rm -rf node_modules package-lock.json
npm install --legacy-peer-deps

# En Windows (PowerShell):
Remove-Item -Recurse -Force node_modules, package-lock.json
npm install --legacy-peer-deps
```

---

### El backend no conecta a la base de datos

Verifica que:
- El archivo `application.properties` tiene las credenciales correctas.
- Tienes conexión a internet (la base de datos está en Supabase, en la nube).
- El puerto 5432 no está bloqueado por el firewall o antivirus de tu computador.

---

### "java: error: release version 17 not supported"

Tu JDK instalado es anterior a la versión 17. Descarga Java 17 desde https://adoptium.net y vuelve a intentar.

---

### El frontend no se conecta al backend

Verifica que el backend esté corriendo en `http://localhost:8080`. El frontend apunta a ese puerto
por defecto. Si necesitas cambiarlo, edita la primera línea de `frontend/src/app/service/api.ts`.