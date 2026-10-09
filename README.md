# Gauzy on Coolify

Ever Gauzy (https://github.com/ever-co/ever-gauzy) deployed on Coolify, Woodwolf server.
Domain: https://project.woodwolfdigital.com

## Stack (prebuilt images, no build step)

- `db` - postgres:17-alpine, persistent volume `gauzy-postgres-data`
- `api` - ghcr.io/ever-co/gauzy-api:latest (NestJS, port 3000 internal)
- `webapp` - ghcr.io/ever-co/gauzy-webapp:latest (Angular via nginx, port 4200)

The webapp nginx proxies `/api/*` to the API container, so only the webapp
needs the public domain. Browsers call `https://project.woodwolfdigital.com/api`.

## Coolify configuration

- Build pack: dockercompose, compose file at `/docker-compose.yml`
- Domain on `webapp`: `https://project.woodwolfdigital.com:4200`
- Required env vars (set in Coolify, never commit secrets):
  - `DB_NAME`, `DB_USER`, `DB_PASS`
  - `API_BASE_URL=https://project.woodwolfdigital.com/api`
  - `CLIENT_BASE_URL=https://project.woodwolfdigital.com`
  - `TRUST_PROXY=1`
  - `DEMO=true` (demo seed data + known logins; set `false` for clean prod)
  - `JWT_SECRET`, `JWT_REFRESH_TOKEN_SECRET`,
    `JWT_VERIFICATION_TOKEN_SECRET`, `EXPRESS_SESSION_SECRET`

## Default logins (DEMO=true)

- Super admin: admin@ever.co / admin
- Employee: employee@ever.co / 12345678
