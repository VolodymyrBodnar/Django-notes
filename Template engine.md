
Шаблоннізатор Django є потужним інструментом, який дозволяє створювати динамічні веб-сторінки в рамках фреймворку Django. Він сприяє розділенню представлення від бізнес-логіки додатку і дозволяє розробникам генерувати HTML-контент, об'єднуючи шаблони з даними зі сторони сервера.

## Основні функції Django Template Engine

### 1. Теги шаблонів

Django надає розширений набір тегів шаблонів, що дозволяють виконувати різноманітні операції всередині шаблонів. Наприклад:

```html
{% if user.is_authenticated %}
    <p>Ви увійшли в систему, {{ user.username }}!</p>
{% else %}
    <p>Будь ласка, увійдіть в систему.</p>
{% endif %}
```

Цей приклад використовує тег `{% if %}` для відображення відповідного повідомлення, в залежності від статусу аутентифікації користувача.

### 2. Фільтри шаблонів

Фільтри дозволяють трансформувати та форматувати дані перед їхнім відображенням в шаблонах. Наприклад:

```html
<p>Дата публікації: {{ article.pub_date|date:"d.m.Y" }}</p>
```

У цьому прикладі фільтр `date` використовується для форматування дати публікації статті.

### 3. Наслідування шаблонів

Django підтримує наслідування шаблонів, що дозволяє розробникам створювати базовий шаблон зі спільною структурою і наслідувати його від інших шаблонів. Це сприяє перевикористанню коду і забезпечує єдність сторінок.

```html
<!-- Базовий шаблон (base.html) -->
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}Мій сайт{% endblock %}</title>
</head>
<body>
    <div id="header">
        <!-- Заголовок сайту -->
    </div>
    <div id="content">
        {% block content %}{% endblock %}
    </div>
</body>
</html>

<!-- Шаблон сторінки (page.html) -->
{% extends "base.html" %}

{% block title %}Головна сторінка{% endblock %}

{% block content %}
    <!-- Вміст головної сторінки -->
{% endblock %}
```

У цьому прикладі шаблон `page.html` наслідується від базового шаблону `base.html`, дозволяючи зберігати єдність дизайну.

## Сценарії використання Django Template Engine

### Створення HTML-сторінок

Django Template Engine використовується для створення HTML-сторінок для вашого веб-сайту. Ви можете вставляти дані з бази даних, такі як статті, користувачі, інформація про товари, у HTML-шаблони та відображати їх на сторінках.

### Відображення Динамічних Даних

Ви можете використовувати шаблони для відображення динамічних даних, таких як нові повідомлення, коментарі, статистика користувачів тощо.

### Використання Контекстних Даних

Шаблони дозволяють передавати контекстні дані зі сторони сервера, що дозволяє відображати дані на сторінці. Наприклад, передача списку статей на сторінку для відображення.

```python
# Відображення списку статей у шаблоні
{% for article in articles %}
    <h2>{{ article.title }}</h2>
    <p>{{ article.content }}</p>
{% endfor %}
```
