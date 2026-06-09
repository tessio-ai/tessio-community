# Configuration

Tessio is configured entirely through environment variables (Compose / all-in-one) or
Helm values (Kubernetes). Two secrets are required; everything else has a sensible
default.

## Required secrets

| Variable | How to generate |
| --- | --- |
| `SESSION_SECRET` | `openssl rand -base64 48` |
| `TESSIO_SECRET_KEY` | `node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"` (32-byte base64) |

`SESSION_SECRET` signs session cookies. `TESSIO_SECRET_KEY` encrypts stored AI-provider
keys. Keep both stable across restarts — changing `SESSION_SECRET` logs everyone out;
changing `TESSIO_SECRET_KEY` invalidates stored provider keys. The Helm chart generates
and preserves both automatically.

## Environment variables

| Variable | Default | Used by | Purpose |
| --- | --- | --- | --- |
| `DATABASE_URL` | — | api, worker, migrate | PostgreSQL connection (needs `pgvector`) |
| `REDIS_URL` | — | api, worker | Redis connection (job queue) |
| `SESSION_SECRET` | — | api | Cookie signing (required in production) |
| `TESSIO_SECRET_KEY` | — | api | Provider-key encryption (base64 32-byte) |
| `TESSIO_STORAGE_DIR` | `/data/storage` | api | On-disk attachment storage path |
| `TESSIO_ADMIN_EMAIL` | — | migrate | Seed the first admin (optional) |
| `TESSIO_ADMIN_PASSWORD` | — | migrate | First-admin password (optional) |
| `TESSIO_ADMIN_NAME` | — | migrate | First-admin display name (optional) |
| `TESSIO_SITE_ADDRESS` | `:80` | web (Caddy) | Site address; a domain enables auto-HTTPS |
| `TESSIO_VERSION` | `latest` | compose | Image tag to run |
| `POSTGRES_PASSWORD` | `tessio` | bundled postgres | Bundled DB password (keep in sync with `DATABASE_URL`) |
| `TESSIO_HTTP_PORT` / `TESSIO_HTTPS_PORT` | `80` / `443` | compose | Host ports for the edge |

The admin seed is idempotent — it only creates the admin and default schemas on first
run; later starts skip it.

## Helm values

The same settings map to Helm values (see `deploy/helm/tessio/values.yaml`):

| Concern | Helm value |
| --- | --- |
| Image | `image.registry` / `image.repository` / `image.tag` |
| Postgres | `postgresql.enabled` or `externalDatabase.url` |
| Redis | `redis.enabled` or `externalRedis.url` |
| Secrets | `secrets.sessionSecret` / `secrets.secretKey` (auto-generated if empty) |
| Admin seed | `admin.email` / `admin.password` / `admin.name` |
| Attachments | `persistence.enabled` / `persistence.size` |
| Ingress / TLS | `ingress.host` / `ingress.tls` / `ingress.className` |
| Site address | `config.siteAddress` (`:80`; TLS terminates at the Ingress) |
