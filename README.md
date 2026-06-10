# Tessio

Tessio is a **self-hosted ITSM platform** — ticketing, asset/inventory (CMDB), knowledge
base, custom forms, dashboards, and workflow automation. It is **proprietary** software,
**free to self-host** under the [Elastic License 2.0](LICENSE): every feature is included
and free to run, but you may not resell it or offer it as a hosted service to third
parties.

> This repository is the **public distribution** for Tessio — docs, deployment files, and
> issues. It is **generated** from the private source repository; please don't edit it
> directly (changes are overwritten on each sync). The container images are public at
> `ghcr.io/tessio-ai/tessio-*` and the Helm chart at `oci://ghcr.io/tessio-ai/charts/tessio`.

## Install

**Docker Compose** (the recommended single-host path):

```bash
git clone https://github.com/tessio-ai/tessio-community.git tessio && cd tessio
cp .env.production.example .env   # set SESSION_SECRET, TESSIO_SECRET_KEY, TESSIO_ADMIN_*
docker compose up -d
```

**Single container (all-in-one):** `docker compose -f compose.aio.yaml up -d`

**Kubernetes (Helm):**

```bash
helm install tessio oci://ghcr.io/tessio-ai/charts/tessio \
  --set ingress.host=tessio.example.com \
  --set admin.email=admin@example.com --set admin.password=change-me
```

## Docs & support

Full install, configuration, upgrade, and backup docs live in `docs/manual/` and are
published at **<https://tessio-ai.github.io/tessio-community/>**. Questions and bug
reports: use this repository's **Issues** tab.
