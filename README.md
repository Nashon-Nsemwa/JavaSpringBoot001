# Software Engineer API

A small Java 17 and Spring Boot REST API for storing and retrieving software
engineer records. Each record has an `id`, `name`, and `techStack`, and is
stored in PostgreSQL using Spring Data JPA.

## API endpoints

| Method | Endpoint | Description |
| --- | --- | --- |
| `GET` | `/` | Returns a simple “Hello World Spring Boot” message. |
| `GET` | `/api/v1/software-engineers` | Returns all software engineer records. |
| `GET` | `/api/v1/software-engineers/{id}` | Returns the record with the specified ID. |
| `POST` | `/api/v1/software-engineers` | Adds a software engineer record from a JSON request body. |

Example request body for `POST /api/v1/software-engineers`:

```json
{
  "name": "Alex",
  "techStack": "Java, Spring Boot"
}
```

## Project packages

The application classes are in the `com.nshon` package:

- `NshonSpringApplication` — starts the Spring Boot application and handles the
  root greeting endpoint.
- `SoftwareEngineerController` — defines the software engineer REST endpoints.
- `SoftwareEngineerService` — contains the service logic for retrieving and
  adding records.
- `SoftwareEngineerRepository` — provides database operations through Spring
  Data JPA.
- `SoftwareEngineer` — the JPA entity representing a software engineer.

## Technologies

- Java 17
- Spring Boot and Spring Web MVC
- Spring Data JPA / Hibernate
- PostgreSQL
- Maven

## Run locally

You need Java 17 or newer and Docker with Docker Compose. Start the PostgreSQL
database using the included `docker-compose.yml`:

```sh
docker compose up -d db
```

This starts PostgreSQL on `localhost:5332` and creates the `nshon` database
expected by the application. Connection settings are in
`src/main/resources/application.properties`. Start the Spring Boot application
in a separate terminal:

```sh
./mvnw spring-boot:run
```

The API is then available at `http://localhost:8080`. When you are done, stop
the database container with `docker compose down`.

The current Hibernate configuration uses `create-drop`, which recreates the
schema when the application starts and drops it when it stops; do not use it
with data you need to keep.
