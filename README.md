## 👋 Welcome to authentik 🚀

Open-source Identity Provider with SSO, SAML, OAuth2, and LDAP support

## 📋 Description

Open-source Identity Provider with SSO, SAML, OAuth2, and LDAP support

## 🚀 Services

- **server**: ghcr.io/goauthentik/server:latest
- **worker**: ghcr.io/goauthentik/server:latest

### Infrastructure Components

- **redis**: Redis database
- **db**: Postgres database


## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/authentik/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/authentik" ~/.local/srv/docker/authentik
cd ~/.local/srv/docker/authentik
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install authentik
```

## 🔧 Configuration

### Environment Variables

```shell
DB_ADMIN_PASS=ZStaZrbT23a0TONiYQELiBErx2ZSV_B0
APP_SECRET_KEY=cC3JPCcwnj+MlCinOhnL6BszRT9IFYsLrDW+Z5ylhkM=
EMAIL_SERVER_PORT=25
EMAIL_SERVER_HOST=172.17.0.1
EMAIL_SERVER_USE_TLS=true
EMAIL_SERVER_USE_SSL=false
EMAIL_SERVER_TIMEOUT=10
EMAIL_SERVER_FROM_NAME=no-reply@${BASE_HOST_NAME:-$HOSTNAME
AUTHENTIK_ERROR_REPORTING=true
APP_TEMP_PASS=lkdfjdlkjaflkjadlgknvczmbnvnoi4e
# ... see docker-compose.yaml for more
```

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:62000

## 📂 Volumes

- `./rootfs/data/authentik/media` - Data storage
- `./rootfs/data/authentik/templates` - Data storage
- `./rootfs/config/worker/certs` - Data storage
- `./rootfs/data/db/redis/authentik` - Data storage
- `./rootfs/data/db/postgres/authentik` - Data storage

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose logs -f server
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
