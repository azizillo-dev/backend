# Bookstore Backend

Django, DRF, PostgreSQL va JWT (Simple JWT).

## Ishga tushirish

```bash
pip install -r requirements.txt
cp .env.example .env        # .env ichida DB_PASSWORD ni yozing
python manage.py migrate
python manage.py runserver
```

`bookstore` nomli PostgreSQL bazasi oldindan yaratilgan bo'lishi kerak.
tekshiring va bazada testuser yarating

## Endpointlar

- `POST /api/auth/login/` — login, token qaytaradi
- `GET /api/auth/me/` — joriy user (token kerak)
- `POST /api/auth/token/refresh/` — yangi access token
