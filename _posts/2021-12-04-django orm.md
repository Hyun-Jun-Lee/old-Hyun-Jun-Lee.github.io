---
title:  "[Django] django ORM으로 DB CURD 구현"
excerpt: "django ORM으로 DB CURD 구현"

categories:
- Django

toc: True
toc_sticky: True

date: 2021-12-04
last_modified_at: 2021-12-04
---


<br>

## QuerySet, Model Manager

QuerySet을 이용해서 별도로 SQL을 작성할 필요 없이 DB로 부터 데이터를 가져오고 추가, 수정, 삭제 등이 가능

- Post.objects.all() : SELECT * FROM post~ 와 같은 SQL문 생성.
- Post.objects.create() : INSERT INTO post VALUES(~)와 같은 SQL문 생성.

## Models.py

```python
class Menu(models.Model):
    name = models.CharField(max_length=30)

class Category(models.Model):
    menu = models.ForeignKey('Menu', on_delete=models.CASACADE)
    name = models.CharField(max_length=30)
```

## DB 데이터 추가(CREATE)

- Menu 추가

```bash
# django shell 실행
python manage.py shell

# models.py 불러오기
>>> from products.models import Menu

# create()
>>> Menu.objects.create(name='Coffe')
# bluk_create() : 하나의 query로 여려개의 object 생성 가능

>>> a1 = Menu(name='상품')
>>> a2 = Menu(name='카드')
>>> Menu.objects.bulk_create([a1, a2])
```

<br>

- Category 추가

```bash
>>> from products.models import Category

# Menu의 id를 확인하고 추가('Coffe' 메뉴에 추가)
>>> Category.objects.create(name='아메리카노', menu=Menu(id=1))
```

<br>

## DB 데이터 읽기 (READ)

```bash
# 테이블 데이터 전체 출력
>>> Category.objects.all()

# Category 데이터 중 Coffe Menu를 참조하고 있는 데이터만 출력
>>> Category.objects.filter(menu_id=1) # Category.objects.filter(menu__name='음료')

# Coffe Menu를 참조하는 모든 데이터의 name 값을 출력
>>> for category in Category.objects.filter(menu__name='Coffe'):
 print(category.name)

### Coffe Menu를 참조하는 모든 카테고리 출력
>>> a1 = Menu.objects.get(name='Coffe')
>>> a1.category_set.all()

### Coffe Menu를 참조하는 모든 카테고리 개수 출력
>>> a1 = Menu.objects.get(name='Coffe')
>>> a1.category_set.count()

### 아메리카노 카테고리가 참조하고 있는 메뉴의 name값 출력
>>> a2 = Category.objects.get(name='아메리카노')
>>> a2.menu.name
```

<br>

## DB 데이터 수정 (UPDATE)

```bash
# filter() 메소드로 아메리카노를 카페라떼로 변경, 한번에 여러 데이터 수정 가능
>>> Category.objects.filter(name='아메리카노').update(name='카페라떼')
```

<br>

## DB 데이터 삭제 (DELETE)

```bash
### 단일 삭제
>>> data = Category.objects.get(name='카페라떼')
>>> data.delete()

### 다중 삭제
>>> Category.objects.filter(name='카페라떼').delete()
```