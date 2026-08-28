# Postgres в Docker (локально)

Поднимается через Colima (`brew services start colima` — уже настроен как автозапускаемый сервис,
переживает релогин/ребут ноута).

## Запуск

```bash
cd docker/postgres
cp .env.example .env   # один раз, поменять пароль по желанию
docker compose up -d
```

## Данные

Хранятся в именованном docker-volume `analytics-pgdata` — не в контейнере.
`docker compose down` / `docker restart` / перезапуск Colima данные не трогают.
Только `docker compose down -v` или `docker volume rm analytics-pgdata` удалит всё.

## Подключение

```
host: localhost
port: 5432
user/db/password: см. .env
```

```bash
docker exec -it analytics-postgres psql -U almat -d analytics
```

## Остановить

```bash
docker compose stop      # выключить контейнер, данные остаются
docker compose down      # удалить контейнер, volume остаётся
```
