Проект Taski-Docker

Taski-Docker — проект, нацеленный на контейнеризацию приложения для управления задачами с использованием Docker. Этот репозиторий содержит необходимые файлы и конфигурации для настройки и запуска приложения в среде Docker.

## Стэк технологий
![Python 3.9](https://img.shields.io/badge/Python-3.9-blue.svg)
![Django 3.2.16](https://img.shields.io/badge/Django-3.2.16-green.svg)
![djangorestframework
3.12.4](https://img.shields.io/badge/djangorestframework-3.12.4-green)

## Другие пакеты и библиотеки
Включены в requirements.txt. Адрес: backend/requirements.txt

Возможности
Бэкенд: Бэкенд на основе Python для управления задачами.
Фронтенд: Удобный интерфейс для работы с задачами.
Шлюз: API-шлюз для управления коммуникацией между сервисами.
Docker: Конфигурации для запуска приложения в Docker.

Предварительные требования
Docker
Docker Compose

### Как запустить проект: 
Клонируйте репозиторий:

```bash
git clone https://github.com/kise2k/taski-docker.git
```
Перейдите в него в командной строке:

```bash
cd taski-docker
```

Cоздайте и активируйте виртуальное окружение:

```bash
python3 -m venv venv 
```

Установите зависимости
```bash
source venv/Scripts/activate
```

Обновите pip и установите зависимости: каждая команда - отдельно
```bash
python -m pip install --upgrade pip
pip install -r backend/requirements.txt
```

В корне проекта создайте файл .env и присвойте значения переменным окружения.

Пример:

```bash

DB_HOST=db

DB_PORT=5432

DB_USER=user

DB_PASSWORD=password

DB_NAME=taski

```

Установите [docker](https://www.docker.com/) на свой компьютер.

Запустите проект через docker compose:

```bash
docker compose -f docker-compose.yml up --build -d
```

Выполните миграции:

```bash
docker compose -f docker-compose.yml exec backend python manage.py migrate
```

Соберите статику:

```bash
docker compose -f docker-compose.yml exec backend python manage.py collectstatic
```

## Workflow

Для использования Continuous Integration (CI) и Continuous Deployment (CD): в репозитории GitHub Actions Settings/Secrets/Actions создайте Secrets - переменные окружения для доступа к сервисам:

```bash
DOCKER_USERNAME                # имя пользователя в DockerHub
DOCKER_PASSWORD                # пароль пользователя в DockerHub
HOST                           # ip_address сервера
USER                           # имя пользователя
SSH_KEY                        # приватный ssh-ключ (cd ~/.ssh/id_rsa)
PASSPHRASE                     # кодовая фраза (пароль) для ssh-ключа

TELEGRAM_TO                    # id телеграм-аккаунта (можно узнать у @userinfobot, команда /start)
TELEGRAM_TOKEN                 # токен бота (получить токен можно у @BotFather, /token, имя бота)
```

При push в ЛЮБУЮ ветку автоматически отрабатывают сценарии:
* *tests* - проверка кода на соответствие стандарту PEP8.

При push в ветку main автоматически отрабатывают сценарии:
* *build\_and\_push\_to\_docker\_hub* - сборка и доставка докер-образов на DockerHub
* *deploy* - автоматический деплой проекта на боевой сервер. Выполняется копирование файлов из DockerHub на сервер;
* *send\_message* - отправка уведомления в Telegram.

Структура каталогов
backend/: Код бэкенд-сервиса.

frontend/: Код фронтенд-сервиса.

gateway/: Код API-шлюза.

.github/workflows/: Workflows GitHub Actions для CI/CD.

docker-compose.yml: Конфигурация Docker Compose для разработки.

docker-compose.production.yml: Конфигурация Docker Compose для продакшн.

.env: Файл конфигурации переменных окружения.

.gitignore: Файл игнорирования Git.

README.md: Документация проекта.
