# 1) Базовый образ на Alpine
FROM python:3.11-alpine

# 2) Устанавливаем необходимые пакеты (включая те, которые нужны для компиляции psycopg2)
#    После установки зависимостей - удалим не нужные пакеты ("build-base" и т.п.)
RUN apk update && apk add --no-cache \
    postgresql-client \
    # Пакеты для сборки psycopg2
    gcc musl-dev postgresql-dev

# 3) Создаём непривилегированного пользователя/группу
RUN addgroup -S django && adduser -S django -G django

# 4) Создадим рабочую папку для приложения
WORKDIR /usr/src/app

# 5) Скопируем список зависимостей
COPY requirements.txt ./

# 6) Установим зависимости
#    Обратите внимание, что build-base удалять не нужно, если мы хотим
#    чтобы psycopg2 скомпилился. Но, как правило, уже после установки мы можем снести лишние пакеты
RUN pip install --no-cache-dir -r requirements.txt

# 7) Удалим пакеты, которые нужны были только для сборки (опционально, но уменьшает образ)
RUN apk del gcc musl-dev postgresql-dev

# 8) Копируем внутрь контейнера наш Django-проект
COPY myproject/ /usr/src/app/

# 9) Меняем права владельца на нашу папку, чтобы пользователь django имел доступ
RUN chown -R django:django /usr/src/app

# 10) Переключаемся на непривилегированного пользователя
USER django

# 11) По умолчанию (CMD) запускаем Gunicorn (или дев-сервер Django).
#     В реальном продакшене - лучше Gunicorn/Uvicorn.
#     Здесь для упрощения оставлю Django runserver:
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
