# Kittygram

Веб-приложение для публикации карточек с животными (кошки). Проект включает backend на Django (REST API) и frontend на React. Репозиторий содержит Docker-конфигурацию для быстрой локальной разработки и развёртывания.

## Основные возможности

- Регистрация и авторизация пользователей (через REST API).
- CRUD операций с карточками животных (создание, редактирование, удаление, список).
- Загрузка и хранение изображений (в `media/`).
- Подготовка к развёртыванию через Docker + Nginx.

## Стек

* Python 3.9, Django, Django REST Framework, Gunicorn
* SQLite (dev), PostgreSQL (prod)
* React (CRA), JavaScript (ES6+), npm
* Docker, Docker Compose, Nginx
* pytest, ESLint, Prettier

## Быстрый старт (Docker)

Проще всего запустить приложение с помощью Docker Compose — это создаст и запустит backend, frontend и (опционально) nginx.

1) Скопируйте `.env` при необходимости и настройте параметры (например, секретный ключ Django, настройки БД и т.п.).

2) Соберите и запустите контейнеры:

```bash
docker-compose up --build
```

После успешного запуска:
- Backend будет доступен по адресу http://localhost:8000/ (если в `docker-compose.yml` указан проброс 8000).
- Frontend — http://localhost:3000/ (или сконфигурированному порту).

Для production-сборки используйте `docker-compose.production.yml`.

## Переменные окружения

Файлы и переменные, которые стоит задать:

- `.env` — основной файл с настройками окружения для Docker/compose.
- Для backend (Django) обычно требуются: `SECRET_KEY`, `DJANGO_DEBUG`, `DB_NAME`, `DB_USER`, `DB_PASSWORD`, `DB_HOST`, `DB_PORT`.
- Для frontend — переменные окружения, начинающиеся с `REACT_APP_`, при необходимости указывающие URL API.

Примерно `.env` может выглядеть так (не храните секреты в репозиториях):

```
SECRET_KEY=changeme
DB_NAME=kittygram
DB_USER=postgres
DB_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
```

## Развёртывание

Рекомендации для production:

- Используйте `docker-compose.production.yml` и собирайте статические файлы для backend (`collectstatic`).
- Настройте безопасное хранение секретов и переменных окружения (Vault, Kubernetes Secrets, или CI/CD secrets).
- Используйте nginx в качестве прокси и для отдачи статических файлов.

Примерная последовательность:

```bash
docker-compose -f docker-compose.production.yml up --build -d
```

**Путь к репозиторию:**  
https://github.com/Hayko19/Kittygram
