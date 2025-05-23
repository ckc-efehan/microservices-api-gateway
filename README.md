# Microservices API Gateway

A Spring Cloud Gateway implementation that serves as an API Gateway for a microservices-based online shop application. This gateway provides routing, security, circuit breaking, and observability features for the underlying microservices.

## Architecture

This API Gateway is part of a microservices architecture that includes:

- **Product Service** (port 8080): Manages product information
- **Order Service** (port 8081): Handles order processing
- **Inventory Service** (port 8082): Manages inventory levels
- **API Gateway** (port 9000): Routes requests to appropriate services

The API Gateway provides:
- Centralized routing to microservices
- Authentication and authorization via Keycloak
- Circuit breaking for resilience
- API documentation aggregation
- Observability through Prometheus, Grafana, Tempo, and Loki

## Features

- **Routing**: Routes requests to appropriate microservices based on path
- **Security**: OAuth2/JWT authentication with Keycloak
- **Resilience**: Circuit breaking, timeout, and retry patterns using Resilience4j
- **API Documentation**: Aggregated Swagger UI for all microservices
- **Observability**: Integrated with Prometheus, Grafana, Tempo, and Loki

## Prerequisites

- Java 17 or higher
- Maven
- Docker and Docker Compose

## Setup and Running

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/microservices-api-gateway.git
cd microservices-api-gateway
```

### 2. Start the supporting services with Docker Compose

```bash
docker-compose up -d
```

This will start:
- Keycloak (with MySQL) for authentication
- Prometheus for metrics collection
- Tempo for distributed tracing
- Loki for log aggregation
- Grafana for visualization

### 3. Build and run the API Gateway

```bash
mvn clean install
mvn spring-boot:run
```

## Usage

### Accessing the API Gateway

The API Gateway is accessible at: http://localhost:9000

### Accessing the Microservices

- Product Service: http://localhost:9000/api/product
- Order Service: http://localhost:9000/api/orders
- Inventory Service: http://localhost:9000/api/inventory

### Swagger UI

Access the aggregated Swagger UI for all microservices at:
http://localhost:9000/swagger-ui.html

### Authentication

The API Gateway uses Keycloak for authentication. Keycloak is accessible at:
http://localhost:8181

Default admin credentials:
- Username: admin
- Password: admin

A default realm "spring-microservices-security-realm" is pre-configured.

## Monitoring and Observability

### Grafana

Access Grafana at: http://localhost:3000

Grafana is pre-configured with:
- Prometheus data source for metrics
- Tempo data source for traces
- Loki data source for logs

### Prometheus

Access Prometheus at: http://localhost:9090

### Tempo (Distributed Tracing)

Tempo is accessible through Grafana or directly at: http://localhost:3110

### Loki (Log Aggregation)

Loki is accessible through Grafana or directly at: http://localhost:3100

## Configuration

Key configuration files:
- `application.properties`: Main configuration for the API Gateway
- `Routes.java`: Defines routing rules for microservices
- `SecurityConfig.java`: Configures security and authentication
- `docker-compose.yml`: Configures supporting services

## Circuit Breaking

The API Gateway implements circuit breaking using Resilience4j. If a service is unavailable, the circuit breaker will open and return a fallback response.

## License

[Add your license information here]

## Contributing

[Add contribution guidelines here]
