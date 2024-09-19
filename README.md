#  Как работать с репозиторием финального задания

## Что нужно сделать

Настроить запуск проекта Kittygram в контейнерах и CI/CD с помощью GitHub Actions

## Как проверить работу с помощью автотестов

В корне репозитория создайте файл tests.yml со следующим содержимым:
```yaml
repo_owner: ваш_логин_на_гитхабе
kittygram_domain: полная ссылка (https://доменное_имя) на ваш проект Kittygram
taski_domain: полная ссылка (https://доменное_имя) на ваш проект Taski
dockerhub_username: ваш_логин_на_докерхабе
```

Скопируйте содержимое файла `.github/workflows/main.yml` в файл `kittygram_workflow.yml` в корневой директории проекта.

Для локального запуска тестов создайте виртуальное окружение, установите в него зависимости из backend/requirements.txt и запустите в корневой директории проекта `pytest`.

## Чек-лист для проверки перед отправкой задания

- Проект Taski доступен по доменному имени, указанному в `tests.yml`.
- Проект Kittygram доступен по доменному имени, указанному в `tests.yml`.
- Пуш в ветку main запускает тестирование и деплой Kittygram, а после успешного деплоя вам приходит сообщение в телеграм.
- В корне проекта есть файл `kittygram_workflow.yml`.

# Проект контейнеры и CI/CD для Kittygram

Проект подготовлен в рамках финального задания спринта №17 в целях получения навыков настройки и запуска проектов в контейнерах, настройки автоматического тестирования и деплоя проектов на удалённый сервер.

# Стек технологий
- Python 3.9
- Django 3.2.3
- gunicorn 20.1.0
- PyYAML 6.0
- djoser 2.1.0
- djangorestframework 3.12.4
- Pillow 9.0.0
- webcolors 1.11.1
- psycopg2-binary 2.9.3

# Инструкция по запуску
1. форкнуть репозиторий проекта: kiwinwin/kittygram_final
2. клонировать форкнутый репозиторий
3. в репозитории проекта во вкладке settings/Secrets and variables/actions определить ваши secrets:
- ALLOWED_HOSTS (доменное имя вашего сайта)
- SECRET_KEY (SECRET_KEY вашего проекта )
Логин и пароль вашего профиля на Docker.com:
- DOCKER_PASSWORD
- DOCKER_USERNAME
Данные вашего удалённого сервера:
- HOST (IP-адрес вашего сервера)
- SSH_KEY (закрытый SSH-ключ)
- USER (имя пользователя)
- SSH_PASSPHRASE (passphrase от закрытого SSH-ключа)
Данные для отправки сообщения о деплое проекта:
- TELEGRAM_TO (id получателя сообщения)
- TELEGRAM_TOKEN (token робота)
4. на сервере:

- измените настройки location в секции server в файле /etc/nginx/sites-enabled/default:
server {
    server_name <IP-адрес вашего сервера> <доменное имя вашего сайта>;
    location / {
        proxy_set_header Host $http_host;
        proxy_pass http://127.0.0.1:9000;
    }
}
5. сделайте пуш:
- git add .
- git commit -m "<ваше сообщение коммита>"
- git push

# Эндпоинты
- https://kiwinwin.duckdns.org/signup - регистрация нового пользователя;
- https://kiwinwin.duckdns.org/signin - войти на сайт;
- https://kiwinwin.duckdns.org/ - главная страница сайта;
- https://kiwinwin.duckdns.org/cats/add - добавить нового кота;
- https://kiwinwin.duckdns.org/cats/<id> - просмотр профиля отдельного кота

# Авторы
- команда Яндекс Практикума [yandex-praktikum] (https://github.com/yandex-praktikum)
- Галия Байбулова [kiwinwin] (https://github.com/kiwinwin)
