## 👋 Welcome to authentik 🚀

Authentik - Open-source Identity Provider (SSO, SAML, OAuth2, LDAP)

## 📋 Description

Authentik is an open-source Identity Provider focused on flexibility and versatility. Supports SAML, OAuth2/OIDC, LDAP, SCIM, and more. Perfect for implementing SSO across your infrastructure.

## 🚀 Services

- **server**: Authentik server (`ghcr.io/goauthentik/server:latest`)
- **worker**: Background task worker
- **redis**: Cache and message broker
- **db**: PostgreSQL database

### Infrastructure Components

- **Database**: PostgreSQL for persistent storage
- **Cache/Queue**: Redis for caching and background jobs

## 📦 Installation

### Using curl
```shell
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/authentik/main/docker-compose.yaml" | docker compose -f - up -d
```

### Using git
```shell
git clone "https://github.com/composemgr/authentik" ~/.local/srv/docker/authentik
cd ~/.local/srv/docker/authentik
docker compose up -d
```

### Using composemgr
```shell
composemgr install authentik
```

## 🔧 Configuration

### Environment Variables

```shell
# Core Settings
TZ=America/New_York
BASE_HOST_NAME=${HOSTNAME}

# Database
DB_ADMIN_PASS=changeme_admin_password

# Application
APP_SECRET_KEY=changeme_secret_key
APP_TEMP_PASS=changeme_bootstrap_password

# Email
EMAIL_SERVER_HOST=172.17.0.1
EMAIL_SERVER_PORT=587
EMAIL_SERVER_MAIL_FROM=no-reply@${BASE_DOMAIN_NAME}
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:62000
- **LDAP**: ldap://172.17.0.1:3389
- **LDAPS**: ldaps://172.17.0.1:6636
- **Bootstrap Email**: administrator@${BASE_DOMAIN_NAME}
- **Bootstrap Password**: Use APP_TEMP_PASS value

## 📂 Volumes

- `./rootfs/data/authentik/media` - Uploaded media files
- `./rootfs/data/authentik/templates` - Custom templates
- `./rootfs/db/postgres/authentik` - PostgreSQL data
- `./rootfs/db/redis/authentik` - Redis data

## 🔐 Security

- Change bootstrap password immediately after first login
- Generate strong APP_SECRET_KEY
- Configure 2FA/MFA for admin accounts
- Use HTTPS in production (reverse proxy)
- Rotate secrets regularly

## 🔍 Logging

```shell
docker compose logs -f server
docker compose logs -f worker
```

## 🛠️ Management

```shell
docker compose up -d
docker compose down
docker compose pull && docker compose up -d

# Create superuser
docker compose exec server ak create_admin_group
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+
- Reverse proxy with HTTPS for production
- Valid domain name for OAuth/SAML

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
