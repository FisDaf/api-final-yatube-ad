# Yatube API

REST API для социальной сети Yatube — сервиса для публикации личных дневниковых записей.

Проект реализован на Django REST Framework и позволяет:
- публиковать посты с изображениями и привязкой к тематическим группам;
- комментировать посты других пользователей;
- подписываться на авторов;
- получать данные через REST API с пагинацией, поиском и JWT-аутентификацией.

## Установка

Клонируйте репозиторий и перейдите в него в командной строке:

\`\`\`bash
git clone https://github.com/ваш-логин/api-final-yatube-ad.git
cd api-final-yatube-ad
\`\`\`

Создайте и активируйте виртуальное окружение:

\`\`\`bash
python3 -m venv venv
source venv/bin/activate
\`\`\`

Установите зависимости из файла requirements.txt:

\`\`\`bash
pip install -r requirements.txt
\`\`\`

Выполните миграции:

\`\`\`bash
cd yatube_api
python manage.py migrate
\`\`\`

Запустите проект:

\`\`\`bash
python manage.py runserver
\`\`\`

## Примеры запросов

### Получение JWT-токена

\`\`\`
POST /api/v1/jwt/create/
\`\`\`

Тело запроса:
\`\`\`json
{
    "username": "anton",
    "password": "your_password"
}
\`\`\`

Ответ:
\`\`\`json
{
    "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
    "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9..."
}
\`\`\`

### Получение списка постов

\`\`\`
GET /api/v1/posts/
\`\`\`

Ответ:
\`\`\`json
{
    "count": 123,
    "next": "http://127.0.0.1:8000/api/v1/posts/?page=2",
    "previous": null,
    "results": [
        {
            "id": 1,
            "text": "Текст поста",
            "author": "anton",
            "image": null,
            "group": 1,
            "pub_date": "2026-08-15T10:00:00Z"
        }
    ]
}
\`\`\`

### Создание поста

Требуется передать JWT-токен в заголовке `Authorization: Bearer <ваш_токен>`.

\`\`\`
POST /api/v1/posts/
\`\`\`

Тело запроса:
\`\`\`json
{
    "text": "Новый пост",
    "group": 1
}
\`\`\`

### Подписка на автора

\`\`\`
POST /api/v1/follow/
\`\`\`

Тело запроса:
\`\`\`json
{
    "following": "anton"
}
\`\`\`

Ответ:
\`\`\`json
{
    "user": "your_username",
    "following": "anton"
}
\`\`\`