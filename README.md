# inkar-opt — Docker deploy repo

Этот репозиторий предназначен для деплоя через Docker Compose.

Состав:
- `front/` — git submodule (frontend)
- `backend/` — git submodule (backend)
- `Dockerfile` — multi-stage: собирает фронт и запускает FastAPI
- `docker-compose.local.yml` — локальный запуск (Postgres + app)
- `docker-compose.prod.yml` — прод запуск на VPS (Postgres + app)

## Быстрый старт (prod на VPS)

1) Клон с сабмодулями:

```bash
git clone --recurse-submodules <THIS_REPO_URL>
cd <repo>
```

2) Создай `.env` (не коммить):

```bash
POSTGRES_PASSWORD=CHANGE_ME
PHCENTER_TOKEN=
PROVISOR_LOGIN=
PROVISOR_PASSWORD=
APP_PORT=8010
```

3) Запуск:

```bash
docker compose -f docker-compose.prod.yml --env-file .env up -d --build
```

## Обновление

```bash
git pull
git submodule update --init --recursive --remote
docker compose -f docker-compose.prod.yml --env-file .env up -d --build
```
