# skynet-core

skynet-core is the central infrastructure repository for the Skynet Defense platform. It provides the foundational components for secure, scalable, and highly available distributed system operations including API gateway routing, service orchestration, data schemas, authentication, and deployment configuration.

## Table of Contents

- [Project Structure](#project-structure)
- [Components](#components)
- [Getting Started](#getting-started)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

## Project Structure

```
skynet-core/
├── README.md
├── docs/
│   ├── architecture.md
│   ├── system-overview.md
│   └── integration-model.md
├── gateway/
├── orchestration/
├── schemas/
├── auth/
├── config/
├── tests/
└── docker/
```

## Components

| Directory | Description |
|-----------|-------------|
| `docs/` | Technical documentation including architecture diagrams, system overview, and integration models |
| `gateway/` | API gateway configuration and routing rules for all inbound and outbound service traffic |
| `orchestration/` | Service orchestration logic, workflow definitions, and inter-service coordination |
| `schemas/` | Shared data schemas, API contracts, and message format definitions |
| `auth/` | Authentication and authorization modules, token management, and access control policies |
| `config/` | Environment-specific configuration files and feature flag definitions |
| `tests/` | Integration, end-to-end, and smoke test suites |
| `docker/` | Dockerfiles and Docker Compose files for local development and CI environments |

## Getting Started

### Prerequisites

- Docker 24.x or later
- Python 3.11 or later

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/skynet-defense/skynet-core.git
   cd skynet-core
   ```

2. Configure your environment:
   ```bash
   cp config/config.example.yml config/config.local.yml
   # Edit config/config.local.yml with your local settings
   ```

3. Start the local stack:
   ```bash
   docker compose -f docker/docker-compose.yml up
   ```

4. Run the test suite:
   ```bash
   pytest tests/
   ```

## Documentation

Detailed documentation is available in the [`docs/`](docs/) directory:

- [Architecture](docs/architecture.md) – High-level system architecture and component relationships
- [System Overview](docs/system-overview.md) – Functional overview of the platform and its capabilities
- [Integration Model](docs/integration-model.md) – Integration patterns, external service contracts, and API conventions

## Contributing

1. Fork the repository and create a feature branch.
2. Make your changes with appropriate tests.
3. Open a pull request against `main` with a clear description of the change.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.