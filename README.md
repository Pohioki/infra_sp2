### ЯП - Спринт 15 - Проект Infra. Python-разработчик (бекенд) (Яндекс.Практикум)

### Стек технологий использованный в проекте:
- Python 3.7
- Django 2.2.28
- DRF 3.12.4
- PyJWT 2.1.0
- Docker 20.10.14

Проект YAMDb собирает отзывы от пользователей на произведения

Полная документация к API находится по эндпоинту /redoc

### Запуск проекта через docker-compose
- Клонировать репозиторий, открыть терминал в корневой папке проекта и перейти в папку, содержащую файл *docker-compose.yaml*.

```bash
cd infra_sp2/api_yamdb/infra
```

- Создайте файл `.env` с переменными окружения для работы с базой данных:
```YAML
DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД 
```


- Собираем образ при помощи docker-compose
```bash
docker-compose up -d --build
```

- Выполняем миграции:
```bash
docker-compose exec web python manage.py migrate
```

- Заполняем базу данных сайта:

```bash
docker-compose exec web python manage.py load_users 
docker-compose exec web python manage.py load_titles
docker-compose exec web python manage.py load_genre 
docker-compose exec web python manage.py load_comments
docker-compose exec web python manage.py load_category
```

- Собираем статику:

```bash
docker-compose exec web python manage.py collectstatic --no-input
```

И создаем администратора сайта:

```bash
docker-compose exec web python manage.py createsuperuser
```

### Ссылка на образ в DockerHub
```bash
docker pull pohioki/infra_sp2:v04.04.2023
```

### Примеры работы с API для всех пользователей

Подробная документация доступна по эндпоинту /redoc/


Для неавторизованных пользователей работа с API доступна в режиме чтения, что-либо изменить или создать не получится. 

```
Права доступа: Доступно без токена.
GET /api/v1/categories/ - Получение списка всех категорий
GET /api/v1/genres/ - Получение списка всех жанров
GET /api/v1/titles/ - Получение списка всех произведений
GET /api/v1/titles/{title_id}/reviews/ - Получение списка всех отзывов
GET /api/v1/titles/{title_id}/reviews/{review_id}/comments/ - Получение списка всех комментариев к отзыву
Права доступа: Администратор
GET /api/v1/users/ - Получение списка всех пользователей
```

### Запуск проекта в dev-режиме
- Клонировать репозиторий и перейти в него в командной строке.
- Установите и активируйте виртуальное окружение c учетом версии Python 3.7 (выбираем python не ниже 3.7):

```bash
python3.7 -m venv venv
```

```bash
source venv/Scripts/activate
```

- Затем нужно установить все зависимости из файла requirements.txt

```bash
python3.7 -m pip install --upgrade pip
```

```bash
pip3 install -r requirements.txt
```

- Выполняем миграции:

```bash
python3.7 manage.py migrate --run-syncdb
```

Если есть необходимость, заполняем базу тестовыми данными командами:

```bash
python3.7 manage.py load_title
```
```bash
python3.7 manage.py load_category
```
```bash
python3.7 manage.py load_comments
```
```bash
python3.7 manage.py load_genre
```
```bash
python3.7 manage.py load_reviews
```
```bash
python3.7 manage.py load_titles
```
```bash
python3.7 manage.py load_users
```


Создаем суперпользователя, после меняем в админ панели роль с user на admin:

```bash
python3.7 manage.py createsuperuser
```

Запускаем проект:

```bash
python3.7 manage.py runserver localhost:8000
```

### Примеры работы с API для всех пользователей

Подробная документация доступна по эндпоинту /redoc/


Для неавторизованных пользователей работа с API доступна в режиме чтения, что-либо изменить или создать не получится. 

```
Права доступа: Доступно без токена.
GET /api/v1/categories/ - Получение списка всех категорий
GET /api/v1/genres/ - Получение списка всех жанров
GET /api/v1/titles/ - Получение списка всех произведений
GET /api/v1/titles/{title_id}/reviews/ - Получение списка всех отзывов
GET /api/v1/titles/{title_id}/reviews/{review_id}/comments/ - Получение списка всех комментариев к отзыву
Права доступа: Администратор
GET /api/v1/users/ - Получение списка всех пользователей
```


