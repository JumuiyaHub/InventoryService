# Inventory Service

A Spring Boot microservice for managing inventory data, providing REST APIs with MySQL database integration, Flyway migrations, and comprehensive OpenAPI documentation.

## 🛠 Technologies Used

- **Java 21**
- **Spring Boot 3.x**
- **MySQL 8.3**
- **Flyway Database Migration**
- **Docker & Docker Compose**
- **Maven**
- **OpenAPI 3.0 / Swagger**
- **Testcontainers** (for integration testing)

## 📋 Project Structure

```plaintext
inventory-service/
├── docker/
│   └── mysql/
│       └── init.sql                    # MySQL initialization script
├── docker-compose.yml                  # Docker services configuration
├── src/
│   ├── main/
│   │   ├── java/com/kiru/microservice/inventory/
│   │   │   ├── config/
│   │   │   │   └── OpenAPIConfig.java  # Swagger/OpenAPI configuration
│   │   │   ├── controller/
│   │   │   │   └── InventoryController.java  # REST endpoints
│   │   │   ├── model/
│   │   │   │   └── Inventory.java      # Entity model
│   │   │   ├── repository/
│   │   │   │   └── InventoryRepository.java  # Data access layer
│   │   │   ├── service/
│   │   │   │   └── InventoryService.java     # Business logic
│   │   │   └── InventoryServiceApplication.java  # Main application class
│   │   └── resources/
│   │       ├── db/migration/
│   │       │   ├── V1__init.sql        # Initial database schema
│   │       │   └── V2__add_inventory.sql  # Sample inventory data
│   │       └── application.properties  # Application configuration
│   └── test/
│       └── java/com/kiru/microservice/inventory/
│           ├── InventoryServiceApplicationTests.java
│           ├── TestcontainersConfiguration.java
│           └── TestInventoryServiceApplication.java
├── pom.xml                             # Maven dependencies
└── README.md
```

## 🚀 Getting Started

### Prerequisites

- **Java 21** or higher
- **Docker** and **Docker Compose**
- **Maven 3.8+**

### Quick Start

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd inventory-service
   ```

2. **Start the MySQL database:**
   ```bash
   docker-compose up -d
   ```

3. **Run the application:**
   ```bash
   ./mvnw spring-boot:run
   ```

4. **Access the application:**
    - API Base URL: `http://localhost:8083`
    - Swagger UI: `http://localhost:8083/swagger-ui.html`
    - OpenAPI Spec: `http://localhost:8083/v3/api-docs`

## 🗄️ Database Configuration

### MySQL Settings
- **Host:** localhost
- **Port:** 3308
- **Database:** inventory_service
- **Username:** root
- **Password:** mysql

### Connection String
```
jdbc:mysql://localhost:3308/inventory_service
```

## 📚 API Documentation

The service provides comprehensive API documentation through OpenAPI 3.0.

### Access Points
- **Swagger UI:** `http://localhost:8083/swagger-ui.html`
- **OpenAPI JSON:** `http://localhost:8083/v3/api-docs`
- **OpenAPI YAML:** `http://localhost:8083/v3/api-docs.yaml`

### API Information
- **Version:** v0.0.1
- **License:** Apache 2.0
- **Contact:** [Your Contact Information]

## 🔄 Database Migrations

The application uses Flyway for database versioning and migrations.

### Migration Files
Located in `src/main/resources/db/migration/`:
- **V1__init.sql:** Creates initial database schema
- **V2__add_inventory.sql:** Adds sample inventory data

### Migration Commands
```bash
# Run migrations manually
./mvnw flyway:migrate

# Get migration info
./mvnw flyway:info

# Clean database (development only)
./mvnw flyway:clean
```

## ⚙️ Build and Test

### Running Tests
```bash
# Run all tests
./mvnw test

# Run tests with coverage
./mvnw test jacoco:report

# Run integration tests only
./mvnw test -Dtest=*IntegrationTest
```

### Building the Application
```bash
# Clean and compile
./mvnw clean compile

# Package as JAR
./mvnw clean package

# Skip tests during build
./mvnw clean package -DskipTests
```

## 🐳 Docker Operations

### Using Docker Compose
```bash
# Start all services
docker-compose up -d

# Stop all services
docker-compose down

# View logs
docker-compose logs -f

# Rebuild and start
docker-compose up -d --build
```

### Manual Docker Commands
```bash
# Build application image
docker build -t inventory-service .

# Run container
docker run -p 8083:8083 inventory-service

# Run with environment variables
docker run -p 8083:8083 \
  -e SPRING_DATASOURCE_URL=jdbc:mysql://host.docker.internal:3308/inventory_service \
  inventory-service
```

## 🏛️ Architecture Overview

### Layered Architecture
- **Controller Layer:** REST endpoints and request handling
- **Service Layer:** Business logic and transaction management
- **Repository Layer:** Data access and persistence
- **Model Layer:** Entity definitions and data structures
- **Config Layer:** Application configuration and beans

### Key Components
- **InventoryController:** Handles HTTP requests and responses
- **InventoryService:** Implements business logic
- **InventoryRepository:** Manages data persistence
- **Inventory:** Entity model representing inventory items
- **OpenAPIConfig:** Configures API documentation

## 🔧 Configuration

### Application Properties
Key configurations in `application.properties`:

```properties
# Server Configuration
server.port=8083

# Database Configuration
spring.datasource.url=jdbc:mysql://localhost:3308/inventory_service
spring.datasource.username=root
spring.datasource.password=mysql
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA Configuration
spring.jpa.hibernate.ddl-auto=validate
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true

# Flyway Configuration
spring.flyway.locations=classpath:db/migration
spring.flyway.baseline-on-migrate=true

# OpenAPI Configuration
springdoc.api-docs.path=/v3/api-docs
springdoc.swagger-ui.path=/swagger-ui.html
```

## 🔒 Security Considerations

- Database credentials should be externalized using environment variables
- Consider implementing authentication and authorization
- Use HTTPS in production environments
- Regular security updates for dependencies

## 📊 Monitoring and Health Checks

### Health Endpoints
- **Health Check:** `GET /actuator/health`
- **Application Info:** `GET /actuator/info`
- **Metrics:** `GET /actuator/metrics`

### Logging
- Application logs are configured in `application.properties`
- Database queries can be logged by setting `spring.jpa.show-sql=true`

## 🚀 Deployment

### Environment Variables
```bash
# Database Configuration
SPRING_DATASOURCE_URL=jdbc:mysql://your-db-host:3306/inventory_service
SPRING_DATASOURCE_USERNAME=your_username
SPRING_DATASOURCE_PASSWORD=your_password

# Server Configuration
SERVER_PORT=8083

# Profile Selection
SPRING_PROFILES_ACTIVE=production
```

### Production Checklist
- [ ] Configure external database
- [ ] Set up proper logging
- [ ] Configure security
- [ ] Set up monitoring
- [ ] Configure backup strategy
- [ ] Set up CI/CD pipeline

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the Apache License 2.0 - see the LICENSE file for details.

## 📞 Support

For support and questions:
- Create an issue in the repository
- Contact the development team(ikruruto@gmail.com)
- Check the project documentation
