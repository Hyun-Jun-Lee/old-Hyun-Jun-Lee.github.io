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

- `viewsets.ReadOnlyModelViewSet` : 'list'와 'retrieve' action을 제공
- `viewsets.ModelViewSet` : 'list', 'create', 'retrive', 'update', 'destroy' action 제공

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

`ViewSet`은 CBV가 아닌 헬퍼 클래스이기 때문에 URL conf를 직접 디자인 하지도,  `as_view`로 뷰를 만들지도 않고 Router를 통해 하나의 url로 처리한다.

- `router.register()`
  - prefix : 라우터에 적용할 url prefix
  - viewset : viewset 클래스
  - basename : 생성된 url 이름, default 값은 viewset의 쿼리셋에 따라 자동으로 생성된다.

```python

# views.py

class PostViewSet(ModelViewSet):
    queryset = Post.objects.all()
    serializer_class = PostSerializer   

post_list = PostViewSet.as_view({
    'get': 'list',
    'post': 'create',
})

post_detail = PostViewSet.as_view({
    'get': 'retrieve',
    'put': 'update',
    'patch': 'partial_update',
    'delete': 'destroy',
})

# urls.py

from django.urls import path, include
from . import views

urlpatterns = [
    path('post/', views.post_list),
    path('post/<int:pk>/', views.post_detail),
]
```

위의 코드를 router를 활용해 아래처럼 간단하게 해결할 수 있다.

```python
#. urls.py

from django.urls import path, include
from . import views
from rest_framework.routers import DefaultRouter

router = DefaultRouter()
router.register(r'viewset',views.PostViewSet)

urlpatterns = [
    path('',include(router.urls)),
]
```

- `DefaultRouter` 
  - list route
    - url = '/prefix/'
    - GET : list
    - POST : create
  - detail route
    - url = '/prefix/pl'
    - GET : retrieve
    - PUT : update
    - PATCH : partial_update
    - DELETE : destroy

## decorator action

Router에서 제공하는 기본 url 외로 추가적인 url route가 필요할 때는 `ViewSet`에서 멤버 함수로 구현한 후 `action decorator`를 붙여주면 된다.

```python
class PostViewSet(ModelViewSet):
    queryset = Post.objects.all()
    serializer_class = PostSerializer   

    # 자동으로 url 매핑(ex. url : post/public_list/) , detail = True일 경우 pk 지정해줘야 함
    @action(detail=False)
    def public_list(self, request):
        qs = self.queryset.filter(is_public=True)
        serializer = self.get_serializer(qs, many=True)
        return Response(serializer.data)
```