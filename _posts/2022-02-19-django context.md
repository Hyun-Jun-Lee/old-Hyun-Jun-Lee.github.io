---
title:  "[Django] context 확장"
excerpt: "django context"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-02-19
last_modified_at: 2022-02-19
---

# [Django] context 확장

## context 수정하기

Django에서는 기본적으로 `object_list` 변수를 만들어 그 안에 객체를 넣어 보내준다. (paginator 등이 포함되어있음)

이 때, `context_object_name` 속성을 사용하면 다른 변수를 설정할 수 있다.


```python
# views.py
from django.views.generic import ListView
from books.models import Publisher

class PublisherList(ListView):
    model = Publisher
    context_object_name = 'my_favorite_publishers'
```

## context 추가

context에 다른 객체를 추가하고 싶다면 `get_context_data` 메서드 구현으로 해결할 수 있다.

```python
from django.views.generic import DetailView
from books.models import Publisher, Book

class PublisherDetail(DetailView):
    # model=Publisher로 설정하는 것은 queryset=Publisher.objects.all()을 축약한 것
    model = Publisher

    def get_context_data(self, **kwargs):
        # 기본 구현을 호출해 context를 가져온다.
        context = super(PublisherDetail, self).get_context_data(**kwargs)
        # 모든 책을 쿼리한 집합을 context 객체에 추가한다.
        context['book_list'] = Book.objects.all()
        return context 
```