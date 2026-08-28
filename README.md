# analytics

Учебный репозиторий: тесты, практика по SQL / Python / статистике на пути в data-аналитику.

## Структура

- `notebooks/` — Jupyter-ноутбуки, разбор датасетов
- `sql/` — SQL-запросы и упражнения
- `data/` — локальные данные (не коммитятся, см. .gitignore)
- `docker/postgres/` — локальный Postgres в Docker (см. README там)

## Окружение

```bash
python3 -m venv .venv
./.venv/bin/pip install -r requirements.txt
./.venv/bin/python -m ipykernel install --user --name analytics --display-name "Python (analytics)"
```

В VS Code / Jupyter выбирать kernel **Python (analytics)** для ноутбуков, где нужен Postgres.
