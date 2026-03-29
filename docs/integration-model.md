# Integration Model

This document describes how external systems and internal services integrate with skynet-core.

## Integration Patterns

skynet-core supports two primary integration patterns:

### 1. Synchronous REST API

External clients and internal services communicate via HTTP REST APIs exposed through the gateway.

- **Protocol:** HTTPS (TLS 1.2+)
- **Format:** JSON (application/json)
- **Authentication:** Bearer token (JWT) in the `Authorization` header
- **Versioning:** URL path versioning (e.g., `/v1/resource`)

**Example request:**

```http
GET /v1/status HTTP/1.1
Host: api.skynet-core.internal
Authorization: Bearer <token>
Accept: application/json
```

### 2. Asynchronous Event Streaming

For decoupled, high-throughput integration, services may publish and subscribe to events.

- **Protocol:** Depends on deployment (e.g., internal message bus)
- **Format:** JSON payloads conforming to schemas defined in [`schemas/`](../schemas/)
- **Delivery guarantee:** At-least-once

## Authentication Flow

```
Client ──── POST /auth/token ──▶ Auth Service
                                      │
                               issues JWT token
                                      │
Client ◀─── 200 OK { token } ─────────┘

Client ──── GET /v1/resource
            Authorization: Bearer <token> ──▶ Gateway
                                                  │
                                           validates token
                                                  │
                                           routes to service
```

## Schema Contracts

All API payloads must conform to the schemas defined in the [`schemas/`](../schemas/) directory. Schemas are versioned and backward-compatible changes are preferred. Breaking changes require a new API version.

## Error Handling

| HTTP Status | Meaning |
|-------------|---------|
| 400 | Bad request – invalid payload or missing required fields |
| 401 | Unauthorized – missing or invalid token |
| 403 | Forbidden – insufficient permissions |
| 404 | Not found |
| 429 | Too many requests – rate limit exceeded |
| 500 | Internal server error |

All error responses include a JSON body with `error` and `message` fields:

```json
{
  "error": "unauthorized",
  "message": "Bearer token is missing or invalid"
}
```

## External Service Dependencies

| Service | Purpose | Integration Type |
|---------|---------|-----------------|
| Identity Provider | Token issuance | OAuth 2.0 (OIDC) |

## Related Documentation

- [Architecture](architecture.md)
- [System Overview](system-overview.md)
