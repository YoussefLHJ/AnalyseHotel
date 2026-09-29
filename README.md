# API Protocol Comparison

Comparative study of REST, SOAP, GraphQL, and gRPC using a hotel-booking domain.

**Authors:** Saad Chihab, Youssef Lahjouji  
**Institution:** ÉCOLE MAROCAINE DE SCIENCES DE L'INGÉNIEUR  
**Date:** December 2025

## Scope

The repository contains implementations for REST/SOAP through the Spring backend and a GraphQL backend, plus a `backend-grpc` directory containing protocol contract material. The Docker Compose file explicitly leaves the gRPC service disabled and comments it as not currently implemented.

## Repository Components

| Component | Repository evidence |
|---|---|
| REST | `backend-spring` |
| SOAP | `backend-spring` |
| GraphQL | `backend-graphql` |
| gRPC | Contract material in `backend-grpc`; not enabled in Compose |
| PostgreSQL | `docker-compose.yml` |
| Prometheus | `monitoring/prometheus` |
| Grafana | `monitoring/grafana` |
| Jaeger | `docker-compose.yml` |
| Elasticsearch / Kibana | Optional services in `docker-compose.yml` |
| Load testing | `performance-tests` |
| Results | `results` |

## Benchmarking

The repository contains performance-test and results directories, but the previous README mixed implementation status with externally attributed benchmark claims. This README intentionally reports only repository-backed implementation structure and points readers to the raw artifacts for measured results.

### Status of the protocols

- **Implemented / wired in Compose:** REST, SOAP, GraphQL.
- **Contract-only / not enabled:** gRPC, based on the Compose configuration comment.
- **Benchmarks:** consult the files under `performance-tests/` and `results/` rather than relying on unsupported summary numbers.

## Reproducing the Study

1. Inspect `docker-compose.yml` and the service-specific Dockerfiles.
2. Start the database and implemented API services with Docker Compose.
3. Inspect the load-test scenarios under `performance-tests/`.
4. Run the provided load tests with the tool and configuration used by each test file.
5. Store and review raw outputs under `results/`.

## Architecture

```text
                    +------------------+
                    |    PostgreSQL     |
                    +--------+---------+
                             |
              +--------------+---------------+
              |                              |
      +-------v--------+             +-------v--------+
      | backend-spring |             | backend-graphql|
      | REST + SOAP    |             |    GraphQL     |
      +-------+--------+             +----------------+
              |
       +------v-------+
       | Monitoring   |
       | Prometheus   |
       | Grafana      |
       | Jaeger       |
       +--------------+

      backend-grpc: contract material only; not enabled by Compose
```

## Attribution

This is a joint academic project by Saad Chihab and Youssef Lahjouji. Any benchmark result should be interpreted together with its corresponding raw test and result artifacts.

## Limitations

Measured performance values are intentionally not reproduced here unless they can be directly tied to repository-resident test/result artifacts. Security or protocol characteristics described in general references are not presented as measured project results.
