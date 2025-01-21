# ForoAlura

ForoAlura es un proyecto de foro de preguntas y respuestas diseñado para que los usuarios puedan interactuar mediante tópicos organizados. El sistema está construido en Java y utiliza una base de datos MySQL, con un enfoque en seguridad gracias a Spring Security y JWT para la autenticación.

## Características principales

- **Gestión de tópicos:** Crear, actualizar, detallar y eliminar tópicos.
- **Autenticación y seguridad:** Sistema de autenticación con JWT para garantizar la seguridad de las operaciones.
- **Validaciones:** Todos los campos de un tópico son obligatorios, y no se permite la creación de tópicos con títulos duplicados.
- **Endpoints RESTful:** Los endpoints están diseñados para interactuar con el sistema utilizando `@RequestBody`.

## Estructura de la base de datos

La base de datos está configurada para MySQL y contiene una tabla principal para los tópicos:

### Tabla: `topicos`

| Campo          | Tipo        | Restricciones                            |
|----------------|-------------|------------------------------------------|
| `id`           | BIGINT      | PRIMARY KEY, AUTO_INCREMENT             |
| `titulo`       | VARCHAR(255)| NOT NULL, ÚNICO                         |
| `mensaje`      | TEXT        | NOT NULL                                |
| `fecha_creacion` | TIMESTAMP   | NOT NULL, DEFAULT CURRENT_TIMESTAMP    |
| `status`       | ENUM        | NOT NULL, valores posibles: `ABIERTO`, `CERRADO` |
| `autor`        | VARCHAR(255)| NOT NULL                                |
| `curso`        | VARCHAR(255)| NOT NULL                                |

## Requisitos

- Java 17 o superior.
- MySQL 8.0 o superior.
- Maven.
- Spring Boot.

## Configuración del proyecto

1. Clona el repositorio:

   ```bash
   git clone https://github.com/usuario/foroalura.git
   cd foroalura
   ```

2. Configura la base de datos en el archivo `application.properties`:

   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/foroalura
   spring.datasource.username=tu_usuario
   spring.datasource.password=tu_contraseña
   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.show-sql=true

   spring.security.jwt.secret=clave_secreta
   spring.security.jwt.expiration=3600000
   ```

3. Ejecuta el proyecto:

   ```bash
   mvn spring-boot:run
   ```

## Endpoints

### Crear un tópico
- **Método:** POST
- **URL:** `/api/topicos`
- **Body:**
  ```json
  {
    "titulo": "Título del tópico",
    "mensaje": "Mensaje del tópico",
    "status": "ABIERTO",
    "autor": "Nombre del autor",
    "curso": "Nombre del curso"
  }
  ```

### Actualizar un tópico
- **Método:** PUT
- **URL:** `/api/topicos/{id}`
- **Body:**
  ```json
  {
    "titulo": "Nuevo título",
    "mensaje": "Nuevo mensaje",
    "status": "CERRADO",
    "autor": "Nuevo autor",
    "curso": "Nuevo curso"
  }
  ```

### Detallar un tópico
- **Método:** GET
- **URL:** `/api/topicos/{id}`

### Eliminar un tópico
- **Método:** DELETE
- **URL:** `/api/topicos/{id}`

## Seguridad

- Autenticación basada en JWT.
- Los tokens se deben incluir en el encabezado de la solicitud:
  ```
  Authorization: Bearer <token>
  ```
- Los usuarios no autenticados no pueden acceder a los endpoints.

## Validaciones

- Todos los campos son obligatorios.
- No se permiten títulos duplicados para los tópicos.
