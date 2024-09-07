# Authentication and Authorization Microservice

This project is a microservice for handling authentication and authorization using **Clean Architecture**, **Java**, **Spring Boot**, **Hibernate**, and **PostgreSQL**. It implements JWT-based authentication and supports user roles and permissions management.

## Table of Contents
- [Architecture](#architecture)
- [Technologies](#technologies)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [API Endpoints](#api-endpoints)
- [Environment Variables](#environment-variables)
- [Database](#database)
- [Security](#security)
- [License](#license)

## Architecture

The project follows the **Clean Architecture** principles, which separate the application into distinct layers, ensuring maintainability and testability.

### Layers:
- **Domain**: Contains business entities and core business rules. This layer is completely independent of any external frameworks.
- **Application**: Implements use cases like user registration, authentication, and role assignments. This layer is dependent on domain and infrastructure through interfaces.
- **Interface**: Contains controllers and adapters to expose application functionality via HTTP (REST endpoints).
- **Infrastructure**: Contains implementations for persistence using **Hibernate** and security services like **JWT**.

## Technologies

- **Java** (JDK 17+)
- **Spring Boot** (2.x+)
- **Spring Security** (for authentication and authorization)
- **Hibernate** (ORM implementation)
- **PostgreSQL** (Database)
- **JWT** (JSON Web Token for authentication)
- **Gradle** (Build tool)
  
## Project Structure

```
.
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com.example.authservice
│   │   │       ├── domain         # Core business entities
│   │   │       ├── application    # Use cases implementation
│   │   │       ├── infrastructure # Hibernate Repositories, JWT, Spring Security
│   │   │       └── interfaces     # REST Controllers, DTOs
│   │   └── resources
│   │       ├── application.yml    # Application configuration
│   └── test                       # Unit and integration tests
└── README.md
```

## Getting Started

### Prerequisites
- Java 17+
- Maven
- PostgreSQL (or use Docker)

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-repo/auth-microservice.git
   cd auth-microservice
   ```

2. **Set up the database**:
   Make sure PostgreSQL is running and create a database for the application.
   
   ```sql
   CREATE DATABASE auth_db;
   ```

3. **Configure the environment**:
   Set up the necessary environment variables or edit the `application.properties` file with your PostgreSQL credentials and JWT secret.

4. **Build the project**:
   ```bash
   ./gradlew build
   ```

5. **Run the application**:
   ```bash
   ./gradlew bootRun
   ```

## API Endpoints

| Method | Endpoint            | Description                       |
|--------|---------------------|-----------------------------------|
| POST   | `/auth/login`       | Login and receive a JWT token     |
| POST   | `/auth/register`    | Register a new user               |
| POST   | `/auth/assign-role` | Assign a role to a user           |
| GET    | `/users/me`         | Get the authenticated user's info |

### Example Requests

- **Login** (`/auth/login`)
  ```json
  {
    "username": "john",
    "password": "password123"
  }
  ```

- **Register** (`/auth/register`)
  ```json
  {
    "username": "john",
    "password": "password123"
  }
  ```

- **Assign Role** (`/auth/assign-role`)
  ```json
  {
    "username": "john",
    "role": "ADMIN"
  }
  ```

## Environment Variables

You can set the following environment variables for database and security configuration:

| Variable          | Description                                     |
|-------------------|-------------------------------------------------|
| `DB_URL`          | The JDBC URL for the PostgreSQL database        |
| `DB_USERNAME`     | The database username                           |
| `DB_PASSWORD`     | The database password                           |
| `JWT_SECRET`      | Secret key for signing JWT tokens               |
| `JWT_EXPIRATION`  | Expiration time for JWT tokens (e.g., `3600s`)  |

Example `.env` file:

```
DB_URL=jdbc:postgresql://localhost:5432/authms
DB_USERNAME=postgres
DB_PASSWORD=yourpassword
JWT_SECRET=your-jwt-secret
JWT_EXPIRATION=3600
```

## Database

The project uses **Hibernate** for ORM (Object-Relational Mapping) and **PostgreSQL** as the database. Make sure PostgreSQL is installed and running.

You can configure the database connection in `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/authms
spring.datasource.username=user
spring.datasource.password=password
spring.datasource.driver-class-name=org.postgresql.Driver
```

## Security

- The application uses **JWT (JSON Web Tokens)** for stateless authentication.
- **Spring Security** is configured to secure the endpoints and verify JWT tokens in the request headers.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
