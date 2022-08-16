https://github.com/Ka1las/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg

# Yamdb_final
## Описание проекта

Проект YaMDb собирает отзывы (Review) пользователей на произведения (Titles). Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий (Category) может быть расширен администратором.

Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

В каждой категории есть произведения: книги, фильмы или музыка.

Произведению может быть присвоен жанр (Genre) из списка предустановленных. Новые жанры может создавать только администратор.

Пользователи оставляют к произведениям текстовые отзывы (Review) и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.

## Используемые технологии

- asgiref==3.2.10
- Django==2.2.16
- django-filter==2.4.0
- djangorestframework==3.12.4
- djangorestframework-simplejwt==4.8.0
- gunicorn==20.0.4
- psycopg2-binary==2.8.6
- PyJWT==2.1.0
- pytz==2020.1
- sqlparse==0.3.1 


### Шаблон наполнения env-файла:

- DB_ENGINE=django.db.backends.<база данных> # указываем, какая база данных
- DB_NAME= <имя> # имя базы данных
- POSTGRES_USER= <логин> # логин для подключения к базе данных
- POSTGRES_PASSWORD= <пароль> # пароль для подключения к БД (установите свой)
- DB_HOST= <сервис> # название сервиса (контейнера)
- DB_PORT= <порт> # порт для подключения к БД 

### Описание команд для запуска приложения:

Скопируйте репозиторий:

```
git@github.com:Ka1las/yamdb_final.git
```

Комманда git push является триггером workflow (yamdb_workflow.yaml). При выполнении команды git push запускается набор блоков следующих команд:

- Тестирование проекта.
- Сборка и публикация образа.
- Автоматический деплой.
- Отправка уведомления в персональный чат.


В дальнейшем необходимо установить соединение с сервером и выполнить следующие команды:

- Запускаем в контейнере миграции:

```
sudo docker-compose exec web python manage.py migrate
```

- Создаем в контейнере суперпользователя:

```
sudo docker-compose exec web python manage.py createsuperuser
```
- Собираем статику:

```
docker-compose exec web python manage.py collectstatic --no-input 
```

### Примеры запросов к API:

GET запрос /api/v1/categories/

Пример ответа:

```json
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "name": "string",
        "slug": "string"
      }
    ]
  }
]
```

POST запрос /api/v1/titles/

Тело:

```json
{
"name": "string",
"year": 0,
"description": "string",
"genre": [
"string"
],
"category": "string"
}
```

Пример ответа:

```json
{
  "id": 0,
  "name": "string",
  "year": 0,
  "rating": 0,
  "description": "string",
  "genre": [
    {
      "name": "string",
      "slug": "string"
    }
  ],
  "category": {
    "name": "string",
    "slug": "string"
  }
}
```

GET запрос /api/v1/titles/{title_id}/reviews/

Пример ответа:

```json
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "id": 0,
        "text": "string",
        "author": "string",
        "score": 1,
        "pub_date": "2019-08-24T14:15:22Z"
      }
    ]
  }
]
```
