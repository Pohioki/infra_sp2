### ЯП - Спринт 15 - Проект Infra. Python-разработчик (бекенд) (Яндекс.Практикум)

### Стек технологий использованный в проекте:
- Python 3.7
- Django 2.2.28
- DRF 3.12.4
- PyJWT 2.1.0
- Docker 20.10.14

Проект YAMDb собирает отзывы от пользователей на произведения

Полная документация к API находится по эндпоинту /redoc

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