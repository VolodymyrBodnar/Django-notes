
## Крок 1: Встановлення PostgreSQL

Спочатку переконайтеся, що PostgreSQL встановлено на вашому сервері або комп'ютері. Ви можете завантажити та встановити PostgreSQL з [офіційного сайту](https://www.postgresql.org/download/). Або використовувати [докер](https://hub.docker.com/_/postgres)

## Крок 2: Встановлення бібліотеки psycopg2

Для того, щоб Django міг взаємодіяти з PostgreSQL, встановіть бібліотеку `psycopg2`, яка є адаптером бази даних для PostgreSQL. Ви можете це зробити за допомогою pip:

```shell
pip install psycopg2
```

## Крок 3: Налаштування Django проекту

В вашому Django проекті відредагуйте файл `settings.py` [[Модуль Налаштувань Django]], щоб налаштувати підключення до PostgreSQL.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'назва_бази_даних',
        'USER': 'користувач',
        'PASSWORD': 'пароль',
        'HOST': 'localhost',  # Адреса сервера PostgreSQL (зазвичай localhost)
        'PORT': '',           # Порт для підключення (зазвичай залишається порожнім)
    }
}
```

Замініть `'назва_бази_даних'`, `'користувач'`, та `'пароль'` на відповідні дані вашої бази даних PostgreSQL.
	
Інколи при підключенні через докер 'HOST': 'localhost', може не працювати:  [розвязок потенційних проблем з підключенням](https://stackoverflow.com/questions/31249112/allow-docker-container-to-connect-to-a-local-host-postgres-database)

або ви можете знайти адресу вашої бази через
```
docker inspect my-postges-image-name
```
## Крок 4: Застосування Міграцій

Після налаштування бази даних виконайте міграції для створення таблиць у базі даних:

```shell
python manage.py makemigrations
python manage.py migrate
```

## Крок 5: Перевірка Підключення

Запустіть сервер Django та переконайтеся, що підключення до бази даних PostgreSQL працює правильно.

Тепер ваш Django проект повинен бути налаштований для використання бази даних PostgreSQL. Ви можете створювати та опрацьовувати дані у PostgreSQL з використанням Django ORM.