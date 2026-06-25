# authpipe-specs

OpenAPI specification for the [Authpipe](https://authpipe.dev) API.

## Files

- `openapi.json` — OpenAPI 3.1 specification generated from the Authpipe service

## Regenerating

From the `authpipe` service repository:

```bash
cd ../authpipe
go run ./cmd/authpipe openapi > ../authpipe-specs/openapi.json
```

## API Overview

The Authpipe API provides credential management for third-party API connections. It exposes two route groups:

### Public Routes

| Method | Path | Description |
|--------|------|-------------|
| GET | `/providers` | List provider catalog |
| GET | `/oauth/callback` | OAuth callback handler |
| POST | `/webhooks/{provider}` | Receive provider webhooks |

### Authenticated Routes (Bearer token)

**Credentials**

| Method | Path | Description |
|--------|------|-------------|
| POST | `/api/credentials` | Get a valid credential |
| POST | `/api/credentials/store` | Store an API key or webhook secret |
| POST | `/api/installation-credentials` | Get an installation credential |

**Connections**

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/connections` | List connections |
| GET | `/api/connections/{id}` | Get a connection |
| DELETE | `/api/connections/{id}` | Disconnect |

**Installations**

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/installations` | List installations |
| GET | `/api/installations/{id}` | Get an installation |
| DELETE | `/api/installations/{id}` | Delete installation |

**Auth Sessions**

| Method | Path | Description |
|--------|------|-------------|
| POST | `/api/auth-sessions` | Create OAuth authorization session |
| POST | `/api/install-sessions` | Create app installation session |

**Provider Configs**

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/provider-configs` | List provider configs |
| POST | `/api/provider-configs` | Create provider config |
| GET | `/api/provider-configs/{id}` | Get provider config |
| DELETE | `/api/provider-configs/{id}` | Delete provider config |

**API Keys**

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/api-keys` | List API keys |
| POST | `/api/api-keys` | Create API key |
| DELETE | `/api/api-keys/{id}` | Revoke API key |

**Workspaces**

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/workspaces/{id}` | Get workspace |
| PATCH | `/api/workspaces/{id}` | Update workspace |

## Authentication

All `/api/*` endpoints require a Bearer token in the `Authorization` header:

```
Authorization: Bearer ap_live_...
```

API keys are scoped to a workspace and environment (production or development).
