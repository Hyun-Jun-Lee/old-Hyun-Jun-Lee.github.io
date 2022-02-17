---
title:  "[Django] FBV vs CBV"
excerpt: "django FBV vs CBV"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-02-17
last_modified_at: 2022-02-17
---

# FBV vs CBV

클라이언트는 url 주소를 통해 서버에 request를 보내고, Django는 urls.py를 참고하여 해당 url에 매핑된 뷰를 찾아 실행한다. 이때 실행되는 뷰의 종류에는 클래스 기반 뷰(class-based view)와 함수 기반 뷰(function-based view)가 있다.

## FBV(Function Based View)

함수를 직접 만들어 원하는 기능을 구현하는 방법

```python
## urls.py
urlpatterns = [
    path('',views.index, name='index'),
]

## views.py
def index(request):
    if request.method == "POST":
        #######
    else:
        #######
```

## CBV

Django에서 제공하는 클래스를 활용해 구현하는 방법으로 반복적으로 많이 구현하는 것들을 클래스로 미리 구현해서 사용자에게 제공한다.

```python
#urls.py
urlpatterns = [
    path('', IndexView.as_view()),
]

#views.py
from django.views.generic import View


class IndexView(View):
    model = 사용할 모델이 있다면

    def get(self, request):
        # Get 리퀘스트 일경우
    def post(self, request):
        # POST 리퀘스트 일경우
```

### 주요 Generic Views

- Base View
  - View : 최상위 부모 제너릭 뷰 클래스
  - TemplateView : 장고 HTML 템플릿을 보여줄 때
  - RedirectView : 주어진 URL로 리다이렉트

- Generic Display View
  - DetailView : 조건에 맞는 하나의 객체 출력
  - ListView : 조건에 맞는 객체 목록 출력

- Generic Edit View
  - FormView : 폼이 주어지면 해당 폼 출력
  - CreateView : 객체를 생성하는 폼 출력
  - UpdataView : 기존 객체를 수정하는 폼 출력
  - DeleteView : 기존 객체를 삭제하는 폼 출력


> View attributes 모아둔 사이트

- <a href="https://ccbv.co.uk/projects/Django/3.0/django.views.generic.list/ListView/">ccbv</a>

## 장단점

CBV vs FBV|장점|단점|
|------|---|---|
|CBV|- 재사용 및 확장 용이</br>- 다중상속 minxin 사용가능</br>- Generic Class View 제공|- 상속,믹스 되면 코드 이해를 위해 찾아다녀야함</br>- 데코레이터 사용시 별도로 import하거나 생성|
|FBV|- 직관적인 코드</br>- 데코레이터 사용 간단</br>- 구현이 간단|- 확장 및 재사용 어려움|
