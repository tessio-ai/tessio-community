# Tessio self-hosting

Tessio is a **self-hosted ITSM platform** (proprietary; free to self-host under the [Elastic License 2.0](https://www.elastic.co/licensing/elastic-license)) — ticketing,
asset/inventory (CMDB), knowledge base, custom forms, dashboards, and workflow
automation. Every feature is free; there is no paid tier or feature gating. The project
is sustained by optional managed hosting and support.

These docs cover running and operating Tessio on your own infrastructure.

## Pick an install path

| Path | Best for | Containers |
| --- | --- | --- |
| [Docker Compose](install/compose.md) | A single host / VM, the recommended default | 7 (app + Postgres + Redis) |
| [Single container (all-in-one)](install/all-in-one.md) | PaaS (Fly.io, Railway), simplest footprint | 1 app container + your datastores |
| [Kubernetes (Helm)](install/kubernetes.md) | Clusters, declarative + upgrade-safe | Pods via the chart |

All paths run the same images (`ghcr.io/tessio-ai/tessio-*`) and need a
**PostgreSQL with the `pgvector` extension** plus **Redis**.

## Requirements

- **Docker** (Compose v2) for the Compose / all-in-one paths, or a **Kubernetes**
  cluster + **Helm 3** for the Helm path.
- **PostgreSQL 16** with the `vector` and `pgcrypto` extensions available (the bundled
  Postgres image `pgvector/pgvector:pg16` has them; a managed Postgres must support
  `pgvector`).
- **Redis 7** (used as the job queue).
- Two secrets you generate once: a session-signing secret and a 32-byte encryption key
  (see [Configuration](configuration.md)).

New here? Start with the [5-minute quickstart](getting-started.md).
