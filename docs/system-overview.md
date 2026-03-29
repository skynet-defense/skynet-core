# System Overview

## Purpose

skynet-core provides the shared foundational infrastructure for the Skynet Defense platform. It centralizes cross-cutting concerns — authentication, routing, configuration, and observability — so that individual application services can focus on their domain logic.

## Key Capabilities

| Capability | Description |
|------------|-------------|
| API Gateway | Unified entry point for all service traffic with routing, rate limiting, and TLS termination |
| Authentication & Authorization | Centralized identity management using JWT and OAuth 2.0 |
| Service Orchestration | Workflow engine that coordinates multi-service operations and handles failure recovery |
| Schema Registry | Versioned data contracts shared across all services |
| Configuration Management | Environment-aware configuration with secret injection support |
| Observability | Structured logging, distributed tracing, and metrics export |

## Data Flow

```
External Request
      │
      ▼
  [Gateway]  ──── validates token ────▶ [Auth]
      │
      ▼
  [Service]  ──── triggers workflow ──▶ [Orchestration]
      │
      ▼
  [Schemas]  ──── validates payload
```

## Technology Stack

| Layer | Technology |
|-------|------------|
| Runtime | Python 3.11 |
| Containerization | Docker / Docker Compose |
| API | REST (JSON) |
| Auth tokens | JWT (RS256) |
| Configuration | YAML |
| Testing | pytest |

## Environments

- **dev** – Local developer environment using Docker Compose
- **staging** – Pre-production integration environment
- **prod** – Production environment

## Related Documentation

- [Architecture](architecture.md)
- [Integration Model](integration-model.md)
