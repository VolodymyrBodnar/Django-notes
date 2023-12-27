
Реєстрація нового користувача є важливою частиною будь-якого веб-додатку. У Django REST Framework (DRF) ви можете створити своє власне API для реєстрації користувачів. Нижче наведено кроки, які вам потрібно виконати для цього.
```
Note: В повноцінних production проектах для авторизації використовують окремі сервіси, замість вбудовування реєстрації та авторизації в сам проект
```
## Крок 1: Створення Серіалізатора

Спершу створіть серіалізатор для реєстрації користувача. У цьому серіалізаторі ви можете вказати, які атрибути повинні бути включені у запит для створення нового користувача. 

Усі доступні атрибути користувача можна переглянути або в [документації джанго](https://docs.djangoproject.com/en/5.0/ref/contrib/auth/) де описано дефолтну модель користувача, або ж це будуть поля вашої кастомної моделі користувача.

```python
# serializers.py

from rest_framework import serializers
from django.contrib.auth.models import User

class UserRegistrationSerializer(serializers.ModelSerializer):
    password = serializers.CharField(write_only=True)

    class Meta:
        model = User
        fields = ['username', 'password', 'email', 'first_name', 'last_name']
```

## Крок 2: Створення view

Далі створіть view, яке дозволить користувачам реєструватися. Для цього ви можете використовувати вбудовані класи DRF.

```python
# views.py

from rest_framework import generics
from django.contrib.auth.models import User
from rest_framework.permissions import AllowAny
from .serializers import UserRegistrationSerializer

class UserRegistrationView(generics.CreateAPIView):
    queryset = User.objects.all()
    serializer_class = UserRegistrationSerializer
    permission_classes = [AllowAny]
```

## Крок 3: Налаштування route

Додайте маршрут для вашого API, який вказує на відображення реєстрації.

```python
# urls.py

from django.urls import path
from .views import UserRegistrationView

urlpatterns = [
    # ...
    path('api/register/', UserRegistrationView.as_view(), name='user-registration'),
    # ...
]
```
детальніше [[Django Routing|тут]] 
## Крок 4: Використання API для Реєстрації

Тепер ваше API для реєстрації готове до використання. Користувачі можуть реєструватися, надсилаючи POST-запит на URL `/api/register/` з необхідними даними, такими як логін, пароль та інші поля.

```http
POST /api/register/
Content-Type: application/json

{
    "username": "новий_користувач",
    "password": "пароль123",
    "email": "новий_користувач@example.com",
    "first_name": "Ім'я",
    "last_name": "Прізвище"
}
```

API поверне відповідь, яка підтвердить створення нового користувача.
