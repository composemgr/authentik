## 👋 Welcome to authentik 🚀

Open-source Identity Provider with SSO, SAML, OAuth2, and LDAP support

## 📋 Description

authentik is an open-source identity provider that supports single sign-on
through SAML, OAuth2, OpenID Connect, and LDAP. The web interface runs on
native port `9000` (HTTP) with `9443` (HTTPS) available inside the network.

The upstream project publishes version-tagged images only — there is no
`:latest` tag — so the compose files pin the current release, `2026.8.3`.

## 🚀 Services

- **app**: ghcr.io/goauthentik/server:2026.8.3
- **worker**: ghcr.io/goauthentik/server:2026.8.3

### Infrastructure Components

- **db**: postgres:16-alpine - Postgres database
- **redis**: redis:alpine - Redis cache and queue

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/authentik/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/authentik" ~/.local/srv/docker/authentik
cd ~/.local/srv/docker/authentik
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install authentik
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
DB_USER_NAME=authentik
DB_USER_PASS=replace-with-a-random-password
APP_ADMIN_USER=administrator
APP_ADMIN_PASS=replace-with-a-random-password
APP_SECRET_KEY=replace-with-a-random-32-byte-hex-string
AUTHENTIK_ERROR_REPORTING=false
EMAIL_SERVER_HOST=172.17.0.1
EMAIL_SERVER_PORT=587
EMAIL_SERVER_USE_TLS=true
EMAIL_SERVER_USE_SSL=false
```

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

The bootstrap administrator is created from `APP_ADMIN_USER` and
`APP_ADMIN_PASS` on the first start only. Change them before first run, and
never reuse a real `APP_SECRET_KEY` across installations — losing it means
losing encrypted configuration.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64115` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64115

## 📂 Volumes

- `./volumes/data/authentik/media` - User media
- `./volumes/data/authentik/templates` - Branding templates
- `./volumes/config/worker/certs` - Outpost certificates
- `./volumes/db/postgres/authentik` - Database data
- `./volumes/cache/redis/authentik` - Redis data

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
