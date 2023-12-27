
1. **Визначте URL-шаблони:** У файлі `urls.py` вашого Django-проекту імпортуйте види і використовуйте список `urlpatterns` для визначення URL-шаблонів. Кожен URL-шаблон повинен вказувати рядок URL-шаблону та відповідний видовий функціонал або клас.

```python
from django.urls import path
from . import views

urlpatterns = [
    path('приклад/', views.ExampleView.as_view(), name='example'),
    path('інше/', views.OtherView.as_view(), name='other'),
]
```

2. **Включіть URL-шаблони Додатків:** Якщо у вас є кілька додатків у вашому Django-проекті, ви можете включити їх URL-шаблони, використовуючи функцію `include`.

```python
from django.urls import include, path

urlpatterns = [
    path('додаток1/', include('додаток1.urls')),
    path('додаток2/', include('додаток2.urls')),
]
```


**Маршрутизація в DRF:**

1. **Визначте Роутери:** Використовуйте роутери DRF для автоматичного створення URL-шаблонів для ваших наборів видів. DRF надає роутери `DefaultRouter`, `SimpleRouter` та `NestedSimpleRouter`. Для простих випадків використовуйте `DefaultRouter`.

```python
from rest_framework import routers
from . import views

router = routers.DefaultRouter()
router.register(r'елементи', views.ItemViewSet)

urlpatterns = [
    path('api/', include(router.urls)),
]
```

2. **Включіть URL-шаблони Додатків:** Схоже на маршрутизацію в звичайному Django, ви можете включити URL-шаблони, специфічні для додатку, у файлі `urls.py` вашого проекту.

