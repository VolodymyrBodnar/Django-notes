
Django, як потужний веб-фреймворк, надає можливість визначати та використовувати зв'язки між моделями для структурування даних вашого додатку. Однією з найбільш поширених типів зв'язків є Foreign Key та Many-to-Many зв'язки. Давайте розглянемо ці два типи зв'язків.

## Foreign Key (Зовнішній Ключ)

Foreign Key - це спосіб вказати зв'язок між двома моделями, де одна модель посилається на іншу. Це дозволяє вам створювати зв'язки між таблицями бази даних, що реалізується за допомогою стовпця з індексом у відповідній таблиці. Приклад визначення зовнішнього ключа в моделі Django:

```python
from django.db import models

class Author(models.Model):
    name = models.CharField(max_length=100)

class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
```

У цьому прикладі ми визначили дві моделі: `Author` та `Book`. Модель `Book` має зовнішній ключ `author`, який посилається на модель `Author`. Це дозволяє нам встановлювати зв'язок між книгою та її автором.

## Many-to-Many (Багато-до-Багатьох)

Many-to-Many зв'язок використовується, коли багато записів однієї моделі може відповідати багатьом записам іншої моделі та навпаки. Приклад визначення багато-до-багатьох зв'язку в моделі Django:

```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)

class Course(models.Model):
    title = models.CharField(max_length=200)
    students = models.ManyToManyField(Student)
```

У цьому прикладі ми визначили дві моделі: `Student` та `Course`. Модель `Course` має поле `students`, яке є багато-до-багатьох зв'язком з моделлю `Student`. Це дозволяє нам вказувати, які студенти зареєстровані на кожний курс, і навпаки.


Щоб ефективніше отримувати дані зв'язаних таблиць ознайомтесь із [[Пов'язані запити (Select Related і Prefetch Related) в Django ORM]]