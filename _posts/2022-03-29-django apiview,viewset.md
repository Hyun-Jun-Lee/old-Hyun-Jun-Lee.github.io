---
title:  "[DRF] APIView, Mixins, generics APIView"
excerpt: "APIView, Mixins, generics APIView"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-03-29
last_modified_at: 2022-03-29
---

# [DRF] APIView, Mixins, generics APIView

## Serializer

```python
# serializers.py

class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = Post
        fields = '__all__'
        
# views.py

serializer = PostSerializer(data=request.POST)
if serializer.is_valid():
    serializer.save()
    return JsonResponse(serializer.data, status=201)
return JsonResponse(serializer.errors, status=400)
```

DRF의 serializer는 기존 Django Form과 유사하고 Modelserializer는 ModelForm과 유사하다. 

차이점은 `Form은 HTML`을 생성하고 `Serizlizer는 JSON 문자열`을 생성 한다는 것!

## APIView, @api_view

`APIView`는 CBV 방식으로 class에 상속 받아 사용하고
`@api_view` 는 FBV 방식으로 데코레이터로 사용

### APIView

- Example
  - /post/
    - get : 포스팅 리스트
    - post : 새로운 포스트 생성
  - /post/<int:pk>/
    - get : pk번 포스팅 detail
    - put : pk번 포스팅 수정
    - delete : pk번 포스팅 삭제

```python
# views.py

from rest_framework.response import Response
from rest_framework.views import APIView
from django.shortcuts import get_post_or_404
from .models import Post
from .serializers import PostSerializer

# 포스팅 리스트 및 생성
class PostListAPIView(APIView):
    # 포스팅 리스트
    def get(self, request):
        serializer = PostSerializer(Post.objects.all(), many=True)
        return Response(serializer.data)
    # 새 포스팅 생성
    def post(self, request):
        serializer = PostSerializer(data=request.data)
        if serializer.is_valid(): # 유효성 검사
          	serializer.save()
            return Response(serializer.data, status=201)
        return Response(serializer.errors, status=400)  
      

class PostDetailAPIView(APIView):
    def get_post(self, pk):
        try:
            post = Post.objects.all(pk=pk)
            return post
        except:
            return None
    
    # 포스팅 리스트
    def get(self, request, pk, format=None):
        post = self.get_post(pk)
        serializer = PostSerializer(post)
        return Response(serializer.data)
    
    # 포스팅 수정
    def put(self, request, pk):
      	post = self.get_post(pk)
        serializer = PostSerializer(post, data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    # 포스팅 삭제  
    def delete(self, request, pk):
        post = self.get_post(pk)
        post.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

```python
# urls.py

from django.urls import path, include
from . import views

urlpatterns = [
    path('post', views.PostListAPIView.as_view()),
    path('post/<int:pk>/', views.PostDetailAPIView.as_view()),
]
```

### @api_view

- `api_view()`의 인자로 해당 함수에서 가능한 http method를 리스트 형태로 지정

```python
# views.py

from rest_framework.response import Response
from rest_framework.views import APIView
from .models import Post
from .serializers import PostSerializer
from rest_framework.decorators import api_view

@api_view(['GET','POST'])
def post_list(request):
    if request.method == 'GET':
        qs = Post.objects.all()
        serializer = PostSerializer(qs, many=True)
        return Response(serializer.data)
    else:
        serializer = PostSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=201)
        return Response(serializer.errors, status=400)

@api_view(['GET','PUT','DELETE'])
def post_detail(request, pk):
    post = get_object_or_404(Post, pk=pk)
    if request.method == 'GET':
        serializer = PostSerializer(post)
        return Response(serializer.data)
    elif request.method == 'PUT':
        serializer = PostSerializer(post, data=reqeust.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
    else:
        post.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

## Mixins

`APIView`는 각 Http method 마다 직접 serializer 처리를 해주는데 rest_framework.mixins에서는 이런 기능을 미리 구현해 두었고 `queryset`과 `serializer_class`를 지정해주기만 하면 됨.

- `CreateModelMixin` : Provides `a .list(request, *args, **kwargs)` method, that implements listing a queryset.
- `ListModelMixin` : Provides a `.create(request, *args, **kwargs)` method, that implements creating and saving a new model instance.
- `RetrieveModelMixin` : Provides a `.retrieve(request, *args, **kwargs)` method, that implements returning an existing model instance in a response.
- `UpdateModelMixin` : Provides a `.update(request, *args, **kwargs)` method, that implements updating and saving an existing model instance.
- `DestroyModelMixin` : Provides a `.destroy(request, *args, **kwargs)` method, that implements deletion of an existing model instance.

> 위의 APIView를 상속받은 class들과 같은 기능

```python
# views.py

from rest_framework.response import Response
from rest_framework import generics
from rest_framework import mixins
from .models import Post
from .serializers import PostSerializer

class PostListMixins(mixins.ListModelMixin, mixins.CreateModelMixin,generics.GenericAPIView):
    queryset = Post.objects.all()
    serializer_class = PostSerializer

    def get(self, request, *args, **kwargs):
        return self.list(request)
    
    def post(self, request, *args, **kwargs):
        return self.create(request)

class PostDetailMixins(mixins.RetrieveModelMixin, mixins.UpdateModelMixin, mixins.DestroyModelMixin, generics.GenericAPIView):
    queryset = Post.objects.all()
    serializer_class = PostSerializer

    def get(self, request, *args, **kwargs):
        return self.retrieve(request, *args, **kwargs)

    def put(self, request, *args, **kwargs):
        return self.update(request, *args, **kwargs)
        
    def delete(self, request, *args, **kwargs):
        return self.delete(request, *args, **kwargs)
```

## generics APIView

`rest_framework.mixins` 덕분에 코드를 많이 줄엿지만, 여러 클래스를 상속하다 보니 가독성이 떨어진다. rest_framework에서는 mixins을 상속한 새로운 클래스들이 정의되어 있다.

- `generics.CreateAPIView` : 생성
- `generics.ListAPIView` : 목록
- `generics.RetrieveAPIView` : 조회
- `generics.DestroyAPIView` : 삭제
- `generics.UpdateAPIView` : 수정
- `generics.RetrieveUpdateAPIView` : 조회/수정
- `generics.RetrieveDestroyAPIView` : 조회/삭제
- `generics.ListCreateAPIView` : 목록/생성
- `generics.RetrieveUpdateDestroyAPIView` : 조회/수정/삭제

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