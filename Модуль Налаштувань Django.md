
Модуль налаштувань Django (`settings.py`) є одним із найважливіших компонентів кожного Django-проекту. Він містить налаштування для всього, від бази даних до статичних файлів та багато іншого. Давайте розглянемо його детальніше.

## Налаштування Бази Даних

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

- `DATABASES`: Ця змінна визначає параметри підключення до бази даних. Ви можете використовувати різні типи баз даних, такі як SQLite, MySQL, PostgreSQL тощо.

## Налаштування Мови та Часового Поясу

```python
LANGUAGE_CODE = 'en-us'
TIME_ZONE = 'UTC'
```

- `LANGUAGE_CODE`: Визначає мову, яку використовує ваш додаток.
- `TIME_ZONE`: Визначає часовий пояс для вашого додатку.

## Налаштування URL

```python
ROOT_URLCONF = 'myproject.urls'
```

- `ROOT_URLCONF`: Вказує головний файл URL-шляхів для вашого проекту.

## Налаштування Статичних Файлів

```python
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / "static"]
```

- `STATIC_URL`: Вказує URL-шлях для статичних файлів, таких як CSS та JavaScript.
- `STATICFILES_DIRS`: Вказує шлях до каталогу зі статичними файлами в вашому проекті.

## Налаштування Шаблонів

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
        'APP_DIRS': True,
    },
]
```

- `TEMPLATES`: Визначає налаштування для обробки шаблонів, включаючи шляхи до каталогів і налаштування движка шаблонів.

## Налаштування Автентифікації та Авторизації

```python
AUTHENTICATION_BACKENDS = (
    'django.contrib.auth.backends.ModelBackend',
    'allauth.account.auth_backends.AuthenticationBackend',
)
```

- `AUTHENTICATION_BACKENDS`: Визначає список способів автентифікації, які використовуються в вашому додатку.

## Налаштування Email

```python
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_PORT = 587
EMAIL_USE_TLS = True
EMAIL_HOST_USER = 'your_email@gmail.com'
EMAIL_HOST_PASSWORD = 'your_email_password'
```

- `EMAIL_BACKEND`: Вказує, який бекенд використовувати для відправлення email-повідомлень.
- `EMAIL_HOST`: Визначає хост-сервер для відправлення email.
- `EMAIL_PORT`: Визначає порт для відправлення email.
- `EMAIL_USE_TLS`: Вказує, чи використовувати TLS для безпечного з'єднання.
- `EMAIL_HOST_USER` і `EMAIL_HOST_PASSWORD`: Логін і пароль для автентифікації на сервері email.

Це лише декілька прикладів налаштувань, які містяться в файлі `settings.py` Django-проекту. Цей файл має багато інших параметрів, які дозволяють вам налаштовувати різні аспекти вашого додатку. Важливо правильно налаш