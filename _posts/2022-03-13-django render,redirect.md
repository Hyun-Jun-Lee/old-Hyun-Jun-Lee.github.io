---
title:  "[Django] django render vs redirect"
excerpt: "render 와 redirect 의 차이"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-03-13
last_modified_at: 2022-03-13
---

# [Django] django render vs redirect

## render

> render 파라미터

```python
render(request, template_name, context=None, content_type=None, status=None, using=None)
```

- `request`와 `template_name`은 필수
- `context` 를 이용하여 View에서 사용하던 변수를 html 템플릿으로 넘길 수 있다.

```python
# views.py

from django.shortcuts import render

def my_view(request):
    name = "name"
    return render(request, 'core/index.html', {
        'name': name,
    }
```

## redirect

```python
redirect(to, permanent=False, *args, **kwargs)
```

- `to` : 이동할 url(urls.py에서 정한 name으로 주로 사용)