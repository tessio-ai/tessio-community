# Quickstart

Get a working Tessio on one machine with Docker Compose in about five minutes.

## 1. Get the code

```bash
git clone https://github.com/tessio-ai/tessio-community.git tessio
cd tessio
```

## 2. Configure

```bash
cp .env.production.example .env
```

Edit `.env` and set the two required secrets:

```bash
# Session cookie signing
openssl rand -base64 48
# 32-byte encryption key (for stored AI provider keys)
node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"
```

Paste the first into `SESSION_SECRET` and the second into `TESSIO_SECRET_KEY`. To create
the first admin automatically, also set `TESSIO_ADMIN_EMAIL` and `TESSIO_ADMIN_PASSWORD`.

## 3. Start

```bash
docker compose up -d
```

This pulls the published images from `ghcr.io/tessio-ai/tessio-*`. Pin a version with
`TESSIO_VERSION=X.Y.Z` in `.env` (default `latest`).

Compose starts Postgres, Redis, runs database migrations (and seeds the admin if you set
the credentials), then brings up the app. Open **http://localhost** and sign in.

## Next steps

- Put it on a domain with HTTPS → [TLS](operations/tls.md)
- Tune configuration → [Configuration](configuration.md)
- Keep it current → [Upgrading](operations/upgrading.md)
- Protect your data → [Backup & restore](operations/backup-restore.md)
