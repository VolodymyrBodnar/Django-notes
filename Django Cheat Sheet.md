
## Створення та Конфігурація Проекту

### Створити новий проект
```
django-admin startproject projectname
```

### Створити нову додатку (аплікацію)
```
python manage.py startapp appname
```

### Запустити локальний сервер
```
python manage.py runserver
```

### Виконати міграції бази даних
```
python manage.py makemigrations
python manage.py migrate
```

## Робота з Моделями та Базою Даних

### Створити нову модель
```python
class ModelName(models.Model):
    field1 = models.CharField(max_length=100)
    field2 = models.IntegerField()
```

### Створити міграцію для моделі
```
python manage.py makemigrations appname
```

### Провести міграції для моделі
```
python manage.py migrate appname
```

### Створити адміністративний розділ для моделі
```python
from django.contrib import admin
from .models import ModelName

admin.site.register(ModelName)
```

### Виконати запити до бази даних через Django Shell
```
python manage.py shell
```

### Створити новий об'єкт моделі
```python
obj = ModelName(field1='value1', field2=42)
obj.save()
```

### Отримати всі об'єкти моделі
```python
objects = ModelName.objects.all()
```

### Фільтрація об'єктів за певною умовою
```python
filtered_objects = ModelName.objects.filter(field1='value')
```

### Оновлення об'єкта моделі
```python
obj.field1 = 'new_value'
obj.save()
```

### Видалення об'єкта моделі
```python
obj.delete()
```

## Робота з URL та Відображеннями

### Додати URL-шлях до відображення
```python
from django.urls import path
from . import views

urlpatterns = [
    path('myview/', views.my_view, name='my-view'),
]
```

### Створити функційне відображення
```python
from django.http import HttpResponse

def my_view(request):
    return HttpResponse("Hello, World!")
```

### Перенаправлення на іншу сторінку
```python
from django.shortcuts import redirect

def redirect_view(request):
    return redirect('my-view')
```

### Передача параметрів в URL
```python
path('article/<int:article_id>/', views.article_detail, name='article-detail')
```

### Отримання параметрів з URL
```python
def article_detail(request, article_id):
    # Використання параметра article_id
```

## Робота з Адміністративним Розділом

### Створення суперкористувача
```
python manage.py createsuperuser
```

### Додати модель до адміністративного розділу
```python
from django.contrib import admin
from .models import ModelName

admin.site.register(ModelName)
```

Цей "Cheat Sheet" містить основні команди та приклади коду для створення, налаштування та роботи з Django проектами. Ви можете використовувати це як зручний довідник для розвитку вашого Django-додатку.