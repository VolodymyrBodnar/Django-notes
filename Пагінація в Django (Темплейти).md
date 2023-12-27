Пагінація дозволяє поділити великі набори даних на сторінки для зручності користувачів. В Django ви можете використовувати пагінацію для створення сторінок з результатами запиту або списком об'єктів. Ось як це зробити.

## Крок 1: Налаштування Пагінації

Ваш Django проект вже має встановлену пагінацію за замовчуванням. У файлі `settings.py` переконайтеся, що параметр `PAGINATION_SETTINGS` налаштований на використання пагінації:

```python
# settings.py

INSTALLED_APPS = [
    # ...
    'django.core.context_processors.request',
    # ...
]

TEMPLATES = [
    {
        'OPTIONS': {
            'context_processors': [
                # ...
                'django.core.context_processors.request',
                # ...
            ],
        },
    },
]

PAGINATION_SETTINGS = {
    'PAGE_RANGE_DISPLAYED': 10,
    'MARGIN_PAGES_DISPLAYED': 2,
    'SHOW_FIRST_PAGE_WHEN_INVALID': True,
}
```

## Крок 2: Додавання Пагінації до Темплейта

Відредагуйте темплейт, в якому ви відображаєте список об'єктів, щоб додати пагінацію. Використовуйте тег `{% for %}` для ітерації через сторінки і `{% if %}` для відображення лінків на попередню та наступну сторінки:

```html
<!-- template.html -->

{% for object in object_list %}
    <!-- Відображення об'єктів списку -->
{% endfor %}

<div class="pagination">
    <span class="step-links">
        {% if objects.has_previous %}
            <a href="?page=1">&laquo; first</a>
            <a href="?page={{ objects.previous_page_number }}">previous</a>
        {% endif %}

        <span class="current-page">
            Сторінка {{ objects.number }} із {{ objects.paginator.num_pages }}.
        </span>

        {% if objects.has_next %}
            <a href="?page={{ objects.next_page_number }}">next</a>
            <a href="?page={{ objects.paginator.num_pages }}">last &raquo;</a>
        {% endif %}
    </span>
</div>
```

## Крок 3: Налаштування URL

Вкажіть URL для вашого вигляду, який підтримує пагінацію. В цьому вигляді ви повинні визначити, як обробляти параметр `page` у запитах.

```python
# views.py

from django.core.paginator import Paginator
from django.shortcuts import render
from .models import YourModel

def your_view(request):
    object_list = YourModel.objects.all()
    paginator = Paginator(object_list, 10)  # Розбити на сторінки по 10 об'єктів на кожну

    page = request.GET.get('page')
    objects = paginator.get_page(page)

    return render(request, 'template.html', {'objects': objects})
```

Тепер ваш Django проект має пагінацію для сторінок з результатами запиту або списком об'єктів. Ви можете налаштувати кількість об'єктів на сторінці, вигляд кнопок та інші параметри за вашими потребами.

Для налаштування пагінації в форматі рест див [[Пагінація в Django REST Framework (DRF)]]
