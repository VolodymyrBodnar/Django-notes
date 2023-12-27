Пагінація в Django REST Framework (DRF) дозволяє обробляти та відображати великі набори даних у вашому API, поділяючи їх на сторінки для зручності користувачів. Ось як це зробити.

## Крок 1: Налаштування Пагінації

DRF має вбудовану підтримку пагінації, і ви можете вибрати з різних видів пагінації, таких як `PageNumberPagination`, `LimitOffsetPagination`, або `CursorPagination`. Налаштуйте пагінацію у вашому файлі `settings.py`.

```python
# settings.py

REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10,  # Кількість об'єктів на сторінці
}
```

## Крок 2: Додавання Пагінації до Вигляду View

В вашому view DRF додайте пагінацію до запиту. Виберіть пагінатор, який вам підходить, і передайте його у вигляді через атрибут `pagination_class`. Також, ви можете отримувати номер сторінки та кількість об'єктів на сторінці з запиту.

```python
# views.py

from rest_framework import generics
from .models import YourModel
from .serializers import YourModelSerializer
from rest_framework.pagination import PageNumberPagination

class YourModelListView(generics.ListAPIView):
    queryset = YourModel.objects.all()
    serializer_class = YourModelSerializer
    pagination_class = PageNumberPagination  # Використовуйте PageNumberPagination або інший пагінатор за потребою
```

## Крок 3: Налаштування URL

В вашому файлі `urls.py` налаштуйте URL для вигляду (view) з пагінацією.
Включіть його у вигляді шляху (path) або у першому аргументі функції `url`. Не забудьте вказати URL-параметр `page` для вказівки номера сторінки.
[[Django Routing]]

```python
# urls.py

from django.urls import path
from .views import YourModelListView

urlpatterns = [
    path('api/your-model/', YourModelListView.as_view(), name='your-model-list'),
]
```

Тепер ваше API, створене з використанням DRF, підтримує пагінацію. Користувачі можуть отримувати обмежену кількість об'єктів на сторінці та переходити між сторінками, додавши `?page=N` до URL.