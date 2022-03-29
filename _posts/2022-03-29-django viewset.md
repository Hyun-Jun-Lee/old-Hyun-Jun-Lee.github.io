---
title:  "[DRF] ViewSet & Router"
excerpt: "ViewSet & Router"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-03-29
last_modified_at: 2022-03-29
---

# [DRF] ViewSet & Router

## ViewSet

```python
# views.py

from rest_framework import generics
from .models import Post
from .serializers import PostSerializer

class PostListGenericAPIView(generics.ListCreateAPIView):
    queryset = Post.objects.all()
    serializer_class = PostSerializer

class PostDetailGenericAPIView(generics.RetrieveUpdateDestroyAPIView):
    queryset = Post.objects.all()
    serializer_class = PostSerializer
```

`generics APIView`로 코드를 많이 줄일 수 있지만 위 코드를 보면 `queryset`과 `serializer_class`가 공통인데도 코딩해줘야 한다. `ViewSet`을 활용하면 이를 한번에 처리 할 수 있다.

`ViewSet`은 헬퍼클래스이고 2 종류가 있다.

- `viewsets.ReadOnlyModelViewSet` : 목록 조회 및 detail
- `viewsets.ModelViewSet` : 목록 조회, detail, CRUD 모두 지원

```python
# views.py

from .models import Post
from .serializers import PostSerializer
from rest_framework import viewsets

class PostViewSet(viewsets.ModelViewSet):
    queryset = Post.objects.all()
    serializer_class = PostSerializer
```

## Router

`ViewSet`은 CBV가 아닌 헬퍼 클래스이기 때문에 `as_view`로 뷰를 만들지 않고 Router를 통해 하나의 url로 처리한다.

```python
#. urls.py

from django.urls import path, include
from . import views
from rest_framework.routers import DefaultRouter

router = DefaultRouter()
router.register('viewset',views.PostViewSet)

urlpatterns = [
    path('',include(router.urls)),
]
```