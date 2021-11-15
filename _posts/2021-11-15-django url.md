---
title:  "[Django] django URL"
excerpt: "django URL Reverse 활용한 url 처리"

categories:
- Django

toc: True
toc_sticky: True

date: 2021-11-15
last_modified_at: 2021-11-15
---


<br>

# Django URL

<br>

## URL Reverse 함수

### url 템플릿 태그

- 내부적으로 reverse 함수 사용

```python
{% raw %}{% url "blog:post_detail" 100 %}{% endraw %}
{% raw %}{% url "blog:post_detail" pk=100 %}{% endraw %}
```

### reverse()

- 매칭 URL이 없으면 `NoReverseMatch` 예외 발생

```python
reverse('blog:post_detail', args=[10]) # '/blog/10/' args 인자로 리스트 지정 필요
reverse('blog:post_detail', kwargs={'pk': 10})
reverse('/hello/') # NoReverseMatch 오류 발생
```

### resolve_url()

- 매핑 URL이 없으면 "인자 문자열"을 그대로 리턴

```python
resolve_url('blog:post_detail', 100) # '/blog/100/'
resolve_url('blog:post_detail', pk=100)
resolve_url('/hello/') # '/hello/' 문자열 그대로 리턴
```

### redirect()

- view 함수 내에서 특정 url로 이동 하고자 할 때 사용
- `get_absolute_url` 함께 사용

```python
redirect('accounts:login')
redirect('/')
```

<br>

### get_absolute_url()

- `resolve_url(모델 인스턴스)`, `redirect(모델 인스턴스)` 를 통해서 모델 인스턴스의 get_absolute_url() 함수를 자동으로 호출
- 어떠한 모델에 대해서 detail 뷰를 만들게 되면 `get_absolute_url()` 함수를 사용하면 코드 간결
- `CreateView`/`UpdateView에`에서 success_url을 제공하지 않는 경우, 해당 model instance의 get_absolute_url 주소로 이동(생성/수정하고 나서 Detail화면으로 이동하는 것이 자연스러운 과정)

```python
class Post(models.Model):
    # ... (생략)
    def get_absolute_url(self):
        return reverse('blog:post_detail', args=[self.id])
```

<a href="getabsoluteurl">참고 blog</a>