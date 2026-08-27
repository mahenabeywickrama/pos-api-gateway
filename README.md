# Api-Gateway

A reactive API Gateway built with Spring Cloud Gateway (WebFlux). It serves as the single entry point for all client requests in the POS system, routing traffic to the appropriate microservices discovered via the Service-Registry.

## About

This project is part of the Enterprise Cloud Architecture (ECA) module in the Higher Diploma in Software Engineering (HDSE) program at the Institute of Software Engineering (IJSE).

## Student & Submission Information

| Field | Details               |
| :--- |:----------------------|
| **Student Name** | Mahen Abeywickrama    |
| **Student Number** | 241711112             |
| **GCP Project ID** | `pos-project-506311`     |
| **GCP Region** | `asia-south2` (Delhi) |

## Project Description

Api-Gateway is the single entry point for all client requests to POS, a cloud-native Point-of-Sale system built on a microservice architecture. It routes incoming traffic to the appropriate backend microservice (inventory, sales, payment) using service instances discovered dynamically via Service-Registry.

## Tech Stack

| Technology | Details |
|---|---|
| Java | 25 |
| Spring Boot | 4.1.0 |
| Spring Cloud | 2025.1.2 |
| Spring Cloud Gateway (WebFlux) | Reactive API routing |
| Spring Cloud Netflix Eureka Client | Service discovery |
| Spring Cloud Config Client | Fetches config from Config-Server |
| Spring Boot Actuator | Health & management endpoints |

## Routing Table

All requests go through `http://localhost:7000`. The gateway forwards them to the registered service instances.

| Route ID           | Path Prefix         | Target Service          |
|--------------------|---------------------|-------------------------|
| `customer-service` | `/api/v1/customers` | `lb://CUSTOMER-SERVICE` |
| `product-service`  | `/api/v1/products`  | `lb://PRODUCT-SERVICE`  |
| `order-service`    | `/api/v1/orders` | `lb://ORDER-SERVICE`    |

## Service Details

| Property | Value |
|---|---|
| Port | `7000` |
| Artifact ID | `Api-Gateway` |
| Group ID | `com.pos` |
| Config Source | `http://localhost:9000` (Config-Server) |
| Service Registry | `http://localhost:9001/eureka` |

## CORS

Cross-Origin Resource Sharing is configured globally to allow all origins, methods, and headers — suitable for development and the frontend webapp.

## Setup / Getting Started

> **Important:** Config-Server and Service-Registry must be running before starting the Api-Gateway.

**Startup order:**
1. Config-Server (`9000`)
2. Service-Registry (`9001`)
3. **Api-Gateway** (`7000`)
4. Domain services...

```bash
./mvnw spring-boot:run
```

The gateway will be available at: `http://localhost:7000`