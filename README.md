## 👋 Welcome to openedx 🚀

Open-source online learning platform

## 📋 Description

Open-source online learning platform

## 🚀 Services

- **server**: openedx/edx-platform:latest

### Infrastructure Components

- **db**: Mongo database


## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/openedx/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/openedx" ~/.local/srv/docker/openedx
cd ~/.local/srv/docker/openedx
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install openedx
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
BASE_DOMAIN_NAME=example.com
BASE_HOST_NAME=openedx.example.com
SERVICE_USER=1000
SERVICE_GROUP=1000
DB_ADMIN_USER=admin
DB_ADMIN_PASS=replace-with-a-random-password
DB_USER_NAME=openedx
DB_USER_PASS=replace-with-a-random-password
DB_CREATE_DATABASE_NAME=openedx
APP_ORG_NAME=Open edX
UWSGI_WORKERS=2
UWSGI_THREADS=4
LANGUAGES=en
DEFAULT_LANGUAGE=en
EMAIL_SERVER_PORT=587
EMAIL_SERVER_HOST=172.17.0.1
EMAIL_SERVER_MAIL_FROM=no-reply@example.com
EMAIL_SERVER_LOGIN_NAME=replace-with-your-smtp-username
EMAIL_SERVER_LOGIN_PASS=replace-with-your-smtp-password
CLOUDFLARE_ZONE_NAME=example.com
CLOUDFLARE_TUNNEL_ID=replace-with-your-tunnel-id
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

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64283` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64283

## 📂 Volumes

- `./volumes/config/openedx/www` - Web root
- `./volumes/data/openedx` - Application data
- `./volumes/db/mongo/openedx` - Database data

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f server
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
