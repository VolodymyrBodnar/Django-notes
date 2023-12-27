
Аутентифікація та авторизація є важливими аспектами будь-якого API. Django REST Framework (DRF) надає засоби для простої аутентифікації через логін та пароль.
## Authentication

Аутентифікація - це процес перевірки ідентичності користувача. DRF надає декілька способів аутентифікації, і одним з них є стандартна аутентифікація Django.

### Стандартна Аутентифікація Django

1. Спершу встановіть `'rest_framework.authtoken'` у вашому файлі налаштувань Django:

    ```python
    INSTALLED_APPS = [
        # ...
        'rest_framework.authtoken',
        # ...
    ]
    ```

2. Потім виконайте міграції, щоб створити таблиці для аутентифікаційних токенів:

    ```bash
    python manage.py migrate
    ```

3. Додайте `'rest_framework.authentication.TokenAuthentication'` до списку аутентифікацій в налаштуваннях DRF:

    ```python
    REST_FRAMEWORK = {
        'DEFAULT_AUTHENTICATION_CLASSES': [
            'rest_framework.authentication.TokenAuthentication',
        ],
        # ...
    }
    ```

Це дозволить користувачам аутентифікуватися через відправку запиту з логіном і паролем. Після аутентифікації їм буде наданий токен, який вони повинні включити у заголовок кожного подальшого запиту для авторизації.

## Authorization

Авторизація - це процес визначення, які дії користувачі можуть виконувати після аутентифікації.

### Встановлення Прав Доступу

DRF надає можливість встановлення прав доступу до вашого API за допомогою класів. Визначте правила доступу у вашому серіалізаторі або відображенні.

```python
from rest_framework import permissions

class MyModelViewSet(viewsets.ModelViewSet):
    queryset = MyModel.objects.all()
    serializer_class = MyModelSerializer
    permission_classes = [permissions.IsAuthenticated]
```

У цьому прикладі ми використовуємо `permissions.IsAuthenticated`, щоб обмежити доступ до перегляду даних тільки для аутентифікованих користувачів.

### Використання Декораторів

Ви також можете використовувати декоратори для встановлення прав доступу до конкретних видів. Наприклад:

```python
from rest_framework.decorators import permission_classes
from rest_framework.permissions import IsAuthenticated

@permission_classes([IsAuthenticated])
def my_view(request):
    # Ваш код
```

## Використання Логіну та Пароля

Якщо ви хочете додати форму для логіну та паролю на вашому веб-сайті або додатку, використовуйте вбудовані сторінки DRF для аутентифікаці

ї. Додайте такі шляхи до вашого файлу `urls.py`:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    # ...
    path('api-auth/', include('rest_framework.urls', namespace='rest_framework')),
    # ...
]
```

Ці шляхи нададуть вам сторінки для введення логіну та паролю та отримання аутентифікаційних токенів.
