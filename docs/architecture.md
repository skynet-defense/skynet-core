# Architecture

This document describes the high-level architecture of the skynet-core platform.

## Overview

skynet-core is designed as a modular, service-oriented platform. Each component is independently deployable and communicates over well-defined interfaces. The system follows a layered architecture:

```
┌─────────────────────────────────────────────┐
│                   Clients                   │
└─────────────────────┬───────────────────────┘
                      │
┌─────────────────────▼───────────────────────┐
│                   Gateway                   │
│         (routing, rate-limiting, TLS)       │
└──────┬──────────────┬──────────────┬────────┘
       │              │              │
┌──────▼──────┐ ┌─────▼──────┐ ┌────▼───────┐
│    Auth     │ │  Services  │ │  Schemas   │
│  (authn/z)  │ │            │ │ (contracts)│
└─────────────┘ └─────┬──────┘ └────────────┘
                      │
         ┌────────────▼────────────┐
         │      Orchestration      │
         │  (workflows, scheduling)│
         └─────────────────────────┘
```

## Components

### Gateway

The gateway is the single entry point for all external traffic. It is responsible for:

- TLS termination
- Request routing to downstream services
- Rate limiting and throttling
- Request/response logging

### Auth

The auth component handles all authentication and authorization concerns:

- Token issuance and validation (JWT / OAuth 2.0)
- Role-based access control (RBAC)
- API key management

### Orchestration

The orchestration layer coordinates multi-step workflows across services:

- Workflow definitions (DAG-based)
- Retry and error handling policies
- Async job scheduling

### Schemas

Shared schema definitions ensure consistent data contracts across all services:

- JSON Schema / Protobuf definitions
- Versioned API contracts
- Validation utilities

### Config

Environment-specific configuration management:

- YAML-based configuration files per environment (`dev`, `staging`, `prod`)
- Feature flags

## Deployment

All components are containerized and orchestrated via Docker Compose (local) or Kubernetes (production). See the [`docker/`](../docker/) directory for container definitions and the [`config/`](../config/) directory for environment configuration.
