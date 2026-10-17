# AirBnb
AirBnb Clone 
# Airbnb Backend — Spring Boot REST API

A backend application for an Airbnb-style hotel and room booking system. This project provides backend services for managing users, hotels, rooms, bookings, guests, inventory, and payments.

**Backend technology:** Java, Spring Boot, Maven, PostgreSQL  
**API testing:** Postman  
**Recommended IDE:** IntelliJ IDEA  
**Frontend:** Not included in this repository. You can build your own frontend separately.

---

## 1. Project Overview

This project contains the backend responsible for processing requests, applying business logic, interacting with the database, and returning API responses.

### Main modules

The repository's database design includes these entities:

- **User:** User and authentication-related information.
- **Hotel:** Hotel details.
- **Room:** Room information associated with a hotel.
- **ContactInfo:** Contact details.
- **Booking:** Booking records.
- **BookingGuest:** Relationship between bookings and guests.
- **Guest:** Guest information.
- **Inventory:** Room availability information.
- **Payment:** Payment-related records.

The exact fields, relationships, business rules, and supported operations are defined by the source code and database mappings.

## 2. Prerequisites

Install the following software before running the application.

| Software | Purpose |
|---|---|
| Java JDK | Compiles and runs the backend |
| IntelliJ IDEA | Opens and runs the Spring Boot project |
| PostgreSQL | Stores application data |
| pgAdmin or DBeaver | Creates and manages the database |
| Git | Downloads the project |
| Postman | Tests REST APIs |

**Java version:** Check the project's `pom.xml` and use the configured Java version. JDK 21 is a suitable starting point only if the project configuration supports it.

Download from the official websites:

- Java: https://adoptium.net/
- IntelliJ IDEA: https://www.jetbrains.com/idea/download/
- PostgreSQL: https://www.postgresql.org/download/
- Git: https://git-scm.com/downloads
- Postman: https://www.postman.com/downloads/

After installing Java and Git, open Command Prompt and check:

```cmd
java -version
javac -version
git --version
```

If Java commands are not recognized, configure `JAVA_HOME` and the Windows `Path` environment variable, then reopen Command Prompt.

## 3. Download the Project

Clone the repository using Git:

```cmd
git clone https://github.com/Anurag-20007/AirBnb-Backend.git
```

If the repository is private, you must first receive collaborator access and authenticate with GitHub.

Enter the downloaded directory:

```cmd
cd AirBnb-Backend
```

Locate the actual Spring Boot project folder. In the uploaded repository, the backend project is expected to be inside the `AirBnb` directory.

```cmd
cd AirBnb
```

Confirm that the folder contains:

- `pom.xml`
- `src`
- `mvnw.cmd` (if included in the repository)
- `src/main/java`
- `src/main/resources`

If `pom.xml` is not in the current directory, navigate to the folder containing it before continuing.

## 4. Open the Backend in IntelliJ IDEA

1. Open IntelliJ IDEA.
2. Select **Open**.
3. Select the backend folder containing `pom.xml`.
4. Allow IntelliJ to import the Maven project.
5. Configure the Project SDK to match the Java version specified by `pom.xml`.
6. Wait until Maven finishes downloading dependencies.
7. Resolve any dependency or JDK errors before running the application.

**Important:** Open the backend project, not a frontend folder. This repository does not include the frontend application.

## 5. Configure PostgreSQL

Install PostgreSQL and ensure its database service is running.

Open pgAdmin or DBeaver and connect to your local PostgreSQL server using your own PostgreSQL username and password.

### Create the database

Create a database named:

```sql
CREATE DATABASE "AirBnb";
```

PostgreSQL treats quoted mixed-case identifiers as case-sensitive. Use the database name that matches the datasource URL in `application.properties`.

If a database with that name already exists, do not create it again.

## 6. Configure Application Properties

Open:

```text
src/main/resources/application.properties
```

Find the existing datasource settings. They should point to your local PostgreSQL database.

The configuration generally follows this format:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/AirBnb
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}
```

Use the actual property names and configuration required by this project. If the file contains additional required settings, preserve them.

### Set database credentials on Windows

In Command Prompt, set the credentials for the current terminal session:

```cmd
set DB_USERNAME=your_postgres_username
set DB_PASSWORD=your_postgres_password
```

Replace the example values with your own PostgreSQL credentials.

If the project currently uses hardcoded datasource credentials, update the configuration consistently before running it. Do not upload real passwords, JWT secrets, or other credentials to GitHub.

**Note:** The environment-variable example works only after the datasource properties are configured to reference those variables. It does not automatically override hardcoded values.

## 7. Database Tables and Schema

The project uses Spring Boot with JPA/Hibernate, based on its configuration.

Check the following setting in `application.properties`:

```properties
spring.jpa.hibernate.ddl-auto=update
```

Use the value already intended for the project unless you understand the consequences of changing it.

- `update`: Attempts to update the schema based on entity mappings.
- `create`: Creates the schema when the application starts.
- `create-drop`: Creates the schema at startup and drops it when the application shuts down.
- `validate`: Checks the schema without creating or updating tables.

**Warning:** Avoid `create` and `create-drop` when you need to preserve existing database data.

Start with an empty development database if you are unsure which schema and demo-data setup the project expects. Check the source code for SQL scripts, migrations, initialization logic, or required seed data.

## 8. Run the Spring Boot Backend

### Option A — IntelliJ IDEA

1. Locate the main Spring Boot application class under `src/main/java`.
2. Open the class containing `@SpringBootApplication`.
3. Click the green Run icon next to the class or its `main()` method.
4. Monitor the Run console for startup errors.

The backend commonly runs on port `8080`, unless configured otherwise.

### Option B — Windows Command Prompt

Run these commands from the folder containing `pom.xml`.

If `mvnw.cmd` is present:

```cmd
mvnw.cmd clean install
```

After the build succeeds:

```cmd
mvnw.cmd spring-boot:run
```

If the Maven wrapper is unavailable, install Maven and use:

```cmd
mvn clean install
mvn spring-boot:run
```

Wait for the Spring Boot startup message. Keep the terminal open while using the backend.

**A successful Maven build alone does not prove that the application has connected to PostgreSQL.** Check the complete startup logs for database, port, and application errors.

## 9. Verify the Backend

Check the console for:

- Successful Spring Boot startup.
- Successful PostgreSQL connection.
- No unresolved dependency errors.
- No port conflict.
- No failed application initialization.

If Actuator or a health endpoint is configured, use its actual configured URL to check application health.

Otherwise, use Postman to send a request to a real endpoint defined by the project.

Opening `http://localhost:8080/` in a browser may return a 404 response if no route is mapped to the root path. That alone does not prove the backend has failed.

## 10. Test APIs Using Postman

1. Open Postman.
2. Create a new HTTP request.
3. Set the method and URL according to the backend controller.
4. Add the required headers, request body, and authentication.
5. Send the request.
6. Check the HTTP status code and response body.

The exact API endpoints, methods, payloads, and authentication requirements must be obtained from the project's controllers, DTOs, security configuration, and API documentation.

Do not assume an endpoint exists simply because its module appears in the database design.

### Where to find the endpoints

Inspect the Java source under:

```text
src/main/java
```

Search for controller classes and mappings such as:

```java
@RestController
@RequestMapping
@GetMapping
@PostMapping
@PutMapping
@DeleteMapping
```

These annotations help identify the routes implemented by the backend.

If authentication is enabled, inspect the authentication controller and security configuration to understand how to obtain and supply a token.

## 11. Connect Your Own Frontend Later

This repository contains the backend only. You can build a frontend using React, Angular, plain HTML/CSS/JavaScript, or another framework.

For local development, the frontend will generally send HTTP requests to the backend, for example:

```text
http://localhost:8080
```

Use the actual backend port and endpoint paths configured in this project.

Before connecting the frontend:

1. Confirm the backend starts successfully.
2. Test the required APIs in Postman.
3. Confirm request and response formats.
4. Configure CORS for the frontend's development origin if required.
5. Implement authentication and error handling according to the backend API contract.

Do not expose database credentials or JWT signing secrets in frontend code.

## 12. Troubleshooting

### Error: `Connection refused` or PostgreSQL connection failure

- Confirm PostgreSQL is running.
- Check the datasource URL and port.
- Verify the database exists.
- Verify the username and password.
- Confirm the database is accessible from the machine running the backend.

### Error: `password authentication failed`

The PostgreSQL credentials do not match the configured server credentials. Correct the datasource configuration.

### Error: `database does not exist`

Create the required database or correct the database name in the datasource URL.

### Error: `Port 8080 was already in use`

Another process is using the configured port. Stop the conflicting process or change the backend port in the configuration.

### Error: `JAVA_HOME` or Java version mismatch

Install the Java version supported by the project's `pom.xml`, configure `JAVA_HOME`, and select the same JDK in IntelliJ.

### Error: Maven dependency download or build failure

- Check the internet connection.
- Confirm Maven imported the project correctly.
- Review the first meaningful error in the build output.
- Run the build again after resolving the cause.

### Error: `404 Not Found` in Postman

Check that the backend is running and that the HTTP method and URL match the controller mapping.

### Error: `401 Unauthorized` or `403 Forbidden`

Check whether the endpoint requires authentication, a valid token, or specific permissions.

### Error: CORS

CORS mainly affects browser-based frontend requests. Verify the frontend origin and the backend's CORS/security configuration. Postman does not enforce browser CORS rules.

## 13. Useful Project Files

| File or directory | Purpose |
|---|---|
| `pom.xml` | Maven dependencies and Java/build configuration |
| `src/main/java` | Java source code, controllers, services, entities, and configuration |
| `src/main/resources/application.properties` | Database and application settings |
| `src/test/java` | Automated tests, if included |
| `mvnw.cmd` | Windows Maven wrapper, if included |

## 14. Important Notes

- Use a separate local development database.
- Never commit personal database passwords, production credentials, or JWT secrets.
- Do not run destructive database commands on a database containing important data.
- Check the actual project configuration before changing Java, Maven, or database settings.
- The backend must be running before API requests can be processed.
- This README is a setup guide, not proof that every API or configuration has been tested on every machine.

## 15. First-Run Checklist

- [ ] Repository cloned successfully.
- [ ] Correct backend folder opened in IntelliJ.
- [ ] Supported JDK configured.
- [ ] Maven dependencies downloaded.
- [ ] PostgreSQL running.
- [ ] Required database created.
- [ ] Datasource credentials configured.
- [ ] Spring Boot application starts successfully.
- [ ] Required API endpoints tested in Postman.
- [ ] No secrets committed to GitHub.

Once these steps are complete, the backend should be ready for local development and for building a separate frontend against its APIs.

