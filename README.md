# MarketPulse

**Real-Time Market Data Processing Platform**

MarketPulse is a backend engineering project built to explore event-driven architecture, Java concurrency, microservices, distributed messaging, containerization, and cloud deployment.

The platform simulates stock-price events, processes them asynchronously through Apache Kafka, stores historical prices in PostgreSQL, and exposes market data through REST APIs. Redis is used to cache frequently requested latest prices.

> **Status:** Initial setup and architecture planning.

All market data is simulated for educational purposes. This is not a trading or investment platform.

## Problem Statement

A market-data application needs to ingest frequent price updates, process events asynchronously, maintain historical records, and serve read requests without tightly coupling ingestion, processing, and querying.

MarketPulse explores how these responsibilities can be separated and operated reliably.

## Architecture

```text
Market Simulator
       |
       v
Ingestion Service
       |
       v
Apache Kafka
       |
       v
Processing Service
       |
       +------> PostgreSQL
       |
       +------> Redis
                    |
                    v
               Market API
                    |
                    v
                 Clients
```

An API Gateway may be introduced in a later phase if the architecture benefits from a centralized entry point.

## Planned Services

### 1. Ingestion Service
- Accept and validate market-price events.
- Assign or validate event identifiers.
- Publish events to Kafka.
- Expose health and readiness information.

### 2. Processing Service
- Consume price events from Kafka.
- Validate and handle duplicate events.
- Persist historical price records in PostgreSQL.
- Update the latest-price cache in Redis.
- Handle failures and retries safely.

### 3. Market API
- Retrieve the latest price for a symbol.
- Query historical prices over a time range.
- Provide a market summary.
- Support pagination and input validation.

### 4. Market Simulator
- Generate deterministic or configurable sample price events.
- Simulate different symbols and event rates.
- Help test the processing pipeline without an external market-data provider.

## Technology Stack

| Area | Technology |
|---|---|
| Language | Java 25 |
| Backend | Spring Boot |
| Build | Maven |
| Messaging | Apache Kafka |
| Relational storage | PostgreSQL |
| Caching | Redis |
| Containers | Docker, Docker Compose |
| Orchestration | Kubernetes |
| Cloud | AWS |
| Version control | Git, GitHub |
| CI/CD | GitHub Actions |

Technology versions and compatibility will be documented as the implementation progresses.

## Engineering Concepts

- Object-oriented programming and SOLID principles.
- Appropriate use of Strategy, Factory, Builder, and Observer patterns.
- Unit and integration testing.
- Event-driven architecture and asynchronous communication.
- Idempotency, retries, and failure handling.
- Database transactions, indexes, and query optimization.
- Container health checks, orchestration, and observability.
- System design trade-offs involving scalability, consistency, and availability.

## Development Roadmap

1. **Foundation:** Repository structure, Maven setup, Spring Boot service, REST API, and tests.
2. **Persistence:** PostgreSQL schema, historical records, and transactions.
3. **Event streaming:** Kafka producer, consumer, event contracts, retries, and idempotency.
4. **Caching and APIs:** Redis cache and market query endpoints.
5. **Containerization:** Dockerfiles and local multi-service environment.
6. **Orchestration:** Kubernetes deployments, services, configuration, probes, and scaling.
7. **Cloud and CI/CD:** AWS deployment, automated tests, image builds, and monitoring.
8. **Hardening:** Load testing, failure scenarios, documentation, and system design review.

## Repository Structure

The repository will evolve as the services are implemented:

```text
MarketPulse/
├── README.md
├── docs/
│   ├── architecture.md
│   └── decisions/
├── ingestion-service/
├── processing-service/
├── market-api/
├── docker-compose.yml
└── .github/
    └── workflows/
```

## Running the Project

Local setup and run instructions will be added once the first service and its dependencies are implemented.

## Disclaimer

MarketPulse uses simulated data and is intended for software engineering education and portfolio demonstration only.