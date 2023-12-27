
Django REST Framework (DRF) - це бібліотека для створення веб-серверів API на базі Django. DRF спрощує створення RESTful API і надає ряд інструментів для цього. У цій нотатці ми розглянемо основні функції DRF та надамо приклади коду.

Приклад проекту з лекції можна глянути тут: https://github.com/VolodymyrBodnar/DjangoExampleWarehouse
## Основні Функції DRF

### 1. Серіалізація Данних

DRF надає інструменти для серіалізації та десеріалізації об'єктів. Серіалізація допомагає перетворювати дані в формати, які легко обмінювати через API. Давайте розглянемо приклад:

```python
from rest_framework import serializers

class MyModelSerializer(serializers.ModelSerializer):
    class Meta:
        model = MyModel
        fields = '__all__'
```

У цьому прикладі ми використали `serializers.ModelSerializer` для автоматичної серіалізації моделі `MyModel`.

### 2. Views

View в DRF визначає, як дані передаються до та отримуються з API. Вони також включають логіку обробки запитів та відповідей. Ось приклад view:

```python
from rest_framework import viewsets
from .models import MyModel
from .serializers import MyModelSerializer

class MyModelViewSet(viewsets.ModelViewSet):
    queryset = MyModel.objects.all()
    serializer_class = MyModelSerializer
```

У цьому прикладі ми використали `viewsets.ModelViewSet` для автоматичного створення CRUD-операцій для моделі `MyModel`.

### 3. Маршрутизація

DRF надає простий спосіб визначити URL-шляхи для вашого API. Ось приклад визначення маршруту:

```python
from rest_framework import routers
from .views import MyModelViewSet

router = routers.DefaultRouter()
router.register(r'mymodels', MyModelViewSet)
```

Цей код встановлює маршрути для перегляду `MyModelViewSet`, що дозволяє виконувати операції на URL `/mymodels`.

### 4. Authentication та Authorization

DRF, як і джанго, має вбудовану підтримку автентифікації і авторизації. Ви можете використовувати різні методи, такі як автентифікація через токени або OAuth. Ось приклад конфігурації автентифікації:

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
		'rest_framework.authentication.BasicAuthentication',
        'rest_framework.authentication.SessionAuthentication',
    ),
    'DEFAULT_PERMISSION_CLASSES': (
        'rest_framework.permissions.IsAuthenticated',
    ),
}
```

У цьому прикладі ми використовуємо автентифікацію через токени та обмежуємо доступ до авторизованих користувачів.

### 5. Пагінація

DRF дозволяє легко налаштовувати пагінацію для списків результатів запитів. Ось приклад налаштування пагінації:

```python
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10,
}
```

Це дозволяє вам обмежувати кількість результатів, які повертаються у відповіді API.

### 6. Документація

DRF надає підтримку для створення документації API. Ви можете використовувати інструменти, такі як Swagger, для автоматичної генерації документації.

### 7. Підтримка Валідації

DRF дозволяє використовувати валідацію для перевірки коректності даних, що передаються через API. Ось приклад використання валідації:

```python
from rest_framework import serializers

class MyModelSerializer(serializers.ModelSerializer):
    class Meta:
        model = MyModel
        fields = '__all__'

    def validate_my_field(self, value):
        if value < 0:
            raise serializers.ValidationError("Значення не може бути від'ємним.")
        return value
```

У цьому прикладі ми використовуємо метод `validate_my_field` для валідації поля моделі.
