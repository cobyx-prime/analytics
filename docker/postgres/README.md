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

## Датасет для практики (Chinook)

Реальный датасет (275 артистов, 3503 трека, 412 счетов) для SQL-практики на настоящем масштабе,
не на 5 строках. Грузится один раз в отдельную базу `chinook` внутри того же контейнера:

```bash
docker exec -i analytics-postgres psql -U almat -d analytics < seed/chinook.sql
```

Скрипт сам создаёт базу `chinook` (`DROP DATABASE IF EXISTS` + `CREATE DATABASE` внутри),
поэтому можно перезапускать безопасно. Ноутбук `notebooks/02-postgres-chinook.ipynb`
подключается именно к ней.

## Остановить

```bash
docker compose stop      # выключить контейнер, данные остаются
docker compose down      # удалить контейнер, volume остаётся
```
