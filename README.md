# VG Institution Management Microservice – Technical Overview

🔧 Project Stack
- **Backend**: Java 17 (Spring Boot 3.5.6, WebFlux)
- **Database**: MongoDB (Reactive)
- **Architecture**: Microservices (Reactive Programming)
- **Documentation**: Swagger/OpenAPI 3.0
- **Build Tool**: Maven

## ✅ Project Purpose

This microservice manages educational institutions and their classrooms within the Valle Grande educational ecosystem. It provides a reactive REST API for creating, updating, and managing institutions with their associated users and classrooms through inter-service communication.

### Key Features
- Complete institution lifecycle management (CRUD operations)
- Classroom management per institution
- User association through external microservice integration
- Reactive programming for high performance and scalability
- Comprehensive API documentation with Swagger UI
- Support for multiple institution statuses and classroom types

---

## 🛠️ Setup Instructions (Imperatives)

### Prerequisites
Ensure you have the following installed:
- **JDK 17** or higher
- **Maven 3.6+**
- **MongoDB Atlas account** (or local MongoDB instance)
- **Git**

### 1. Clone the repository:
```bash
git clone https://github.com/MauricioTorresDev/vg-ms-institution-management.git
cd vg-ms-institution-management
```

### 2. Configure environment variables:
Create a `.env` file or update `application.yml` with your configuration:
```yaml
spring:
  data:
    mongodb:
      uri: your_mongodb_connection_string
      database: your_database_name
```

### 3. Build the project:
```bash
./mvnw clean install
```

### 4. Run the Spring Boot application:
```bash
./mvnw spring-boot:run
```

The service will start on **http://localhost:9080**

---

## 🧩 How to Use the API (Advice with "should")

- You **should** access the Swagger UI at `http://localhost:9080/swagger-ui.html` to explore all available endpoints.
- You **should** test the API using the interactive Swagger documentation before integrating with frontend applications.
- You **should** verify the MongoDB connection before performing any operations.
- You **should** ensure the User microservice is running at `http://localhost:9083` for full functionality.
- You **should** check the API response structure to understand the `ApiResponse` wrapper format.

### Main Endpoints:
- `GET /api/v1/institutions` - List all institutions
- `GET /api/v1/institutions/active` - List active institutions
- `GET /api/v1/institutions/inactive` - List inactive institutions
- `POST /api/v1/institutions` - Create a new institution with users
- `PUT /api/v1/institutions/{id}` - Update an institution
- `DELETE /api/v1/institutions/{id}` - Soft delete an institution
- `POST /api/v1/institutions/{id}/restore` - Restore a deleted institution

---

## 🎯 Future Plans (Advice & Suggestions)

- We **should** implement JWT authentication and authorization before production deployment.
- We **should** add Redis caching layer to improve read performance for frequently accessed institutions.
- We **should** implement event-driven communication using Apache Kafka or RabbitMQ.
- We **should** add comprehensive unit and integration tests with JUnit 5 and Testcontainers.
- We **should** implement rate limiting and circuit breaker patterns using Resilience4j.
- We **should** add monitoring and observability with Micrometer and Prometheus.
- We **should** create Docker containerization and Kubernetes deployment manifests.

---

## 📁 Repository Structure

```
/vg-ms-institution-management
├── src/
│   ├── main/
│   │   ├── java/pe/edu/vallegrande/vgmsinstitutionmanagement/
│   │   │   ├── VgMsInstitutionManagementApplication.java
│   │   │   ├── application/
│   │   │   │   ├── config/          # CORS, Swagger, WebClient configs
│   │   │   │   └── service/         # Business logic layer
│   │   │   ├── domain/
│   │   │   │   ├── enums/           # Status enumerations
│   │   │   │   └── model/           # Domain entities
│   │   │   └── infrastructure/
│   │   │       ├── client/          # External service clients
│   │   │       ├── dto/             # Request/Response DTOs
│   │   │       ├── repository/      # MongoDB repositories
│   │   │       └── rest/            # REST Controllers
│   │   └── resources/
│   │       └── application.yml      # Application configuration
│   └── test/                        # Unit and integration tests
├── pom.xml                          # Maven dependencies
├── mvnw, mvnw.cmd                   # Maven wrapper scripts
├── README.md                        # ← You are here
└── .gitignore                       # Git ignore rules
```

---

## 🧑‍🏫 Contributing (Imperatives & Advice)

1. **Fork** this repository.
2. **Create** a feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Implement** your feature following the existing architecture patterns:
   - Domain layer for entities
   - Service layer for business logic
   - Infrastructure layer for external concerns
4. **Write** unit tests for your changes.
5. **Run** the linter and formatter:
   ```bash
   ./mvnw spotless:apply
   ./mvnw verify
   ```
6. **Commit** your changes with clear, descriptive messages.
7. **Push** to your fork and **open** a Pull Request.
8. You **should** add "Fixes #<issue-number>" in your PR if it addresses an open issue.
9. You **should** ensure all CI/CD checks pass before requesting review.

---

## 🚀 Deployment Requirements (Must & Need To)

### Environment Configuration
You **must** set the following environment variables:

```yaml
# MongoDB Configuration
MONGODB_URI=your_mongodb_connection_string
MONGODB_DATABASE=your_database_name

# External Services
USER_SERVICE_BASE_URL=http://user-service:9083/api/v1/users

# Server Configuration
SERVER_PORT=9080
```

### Pre-Deployment Checklist
- You **must** ensure MongoDB is accessible from your deployment environment.
- You **need to** configure proper CORS origins for production in `CorsConfig.java`.
- You **must** secure sensitive data in environment variables (never commit credentials).
- You **need to** set up health check endpoints for container orchestration.
- You **must** configure proper logging levels for production.

### Building for Production
```bash
./mvnw clean package -DskipTests
```

The JAR file will be generated in `target/vg-ms-institution-management-0.0.1-SNAPSHOT.jar`

### Docker Deployment (Optional)
You **should** create a Dockerfile for containerized deployment:
```dockerfile
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY target/*.jar app.jar
EXPOSE 9080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

## 💡 Best Practices & Tips

- You **should** use reactive programming patterns consistently throughout the codebase.
- You **should** handle errors properly using `GlobalExceptionHandler`.
- You **should** document all new endpoints with Swagger annotations.
- You **should** validate all incoming requests using `@Valid` and custom validators.
- You **should** use DTOs for request/response to avoid exposing domain models directly.
- You **should** follow the established package structure for consistency.
- You **should** run `./mvnw clean verify` before committing changes.
- You **should** use Lombok annotations to reduce boilerplate code.
- You **should** implement proper logging with SLF4J for troubleshooting.

---

## 📚 API Documentation

Once the application is running, access the interactive API documentation:

- **Swagger UI**: http://localhost:9080/swagger-ui.html
- **OpenAPI Spec**: http://localhost:9080/v3/api-docs

---

## 🔗 Related Microservices

This microservice integrates with:
- **User Management Service** (Port 9083): For user creation and management
- **Authentication Service** (Future): For JWT token validation
- **Notification Service** (Future): For email/SMS notifications

---

## 📞 Questions & Support

If you need help:

- **Open an issue** in this repository with detailed description and steps to reproduce.
- **Tag** `@MauricioTorresDev` for urgent technical issues.
- **Check** the existing documentation and Swagger UI before asking questions.
- **Review** closed issues for similar problems and solutions.

---

## 📄 License

This project is part of the Valle Grande educational platform.

---

## 👥 Contributors

- **Development Team**: Valle Grande Institute
- **Maintainer**: Mauricio Torres (@MauricioTorresDev)

---

**Thank you for contributing!** 👍  
Let's build scalable and maintainable microservices together.