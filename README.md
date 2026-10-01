# Habit Log API

REST API для трекера привычек на FastAPI + PostgreSQL. Позволяет логировать выполнение привычек по дням (название привычки, дата, выполнена/нет, заметка).

## Что внутри

- Python 3
- FastAPI
- SQLAlchemy 2
- PostgreSQL
- Uvicorn

## Структура проекта
```text
habit-log-api/
├── app/
│   └── main.py
├── .env.example
├── requirements.txt
```

## API методы

### Проверка состояния
```bash
curl http://127.0.0.1:8010/health
```

### Создать запись
```bash
curl -X POST http://127.0.0.1:8010/logs \
  -H 'Content-Type: application/json' \
  -d '{"habit_name":"Чтение","log_date":"2026-10-01","completed":true,"notes":"30 минут"}'
```

### Получить список записей (с фильтром по привычке)
```bash
curl http://127.0.0.1:8010/logs
curl "http://127.0.0.1:8010/logs?habit_name=Чтение"
```

### Получить запись по ID
```bash
curl http://127.0.0.1:8010/logs/1
```

### Обновить запись
```bash
curl -X PUT http://127.0.0.1:8010/logs/1 \
  -H 'Content-Type: application/json' \
  -d '{"completed":true}'
```

### Удалить запись
```bash
curl -X DELETE http://127.0.0.1:8010/logs/1
```

---

## Задача

Задеплоить этот API самостоятельно, с нуля:

1. Создать пользователя и базу данных в PostgreSQL (`habit_user` / `habit_db`, пароль на своё усмотрение, не забыть `GRANT`).
2. Развернуть приложение в `venv`, установить зависимости из `requirements.txt`.
3. Заполнить `.env` по образцу `.env.example` (реальный пароль от БД, хост, порт).
4. Написать systemd unit-файл самостоятельно (без образца) и запустить приложение через него — `enable --now`, проверить `systemctl status`.
5. Проверить все пять эндпоинтов через `curl` (см. примеры выше) и убедиться, что данные реально сохраняются в PostgreSQL (`psql`, `SELECT * FROM habit_logs;`).
