---
title:  "[Django] ModelForm"
excerpt: "commit=False, clean_data"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-03-14
last_modified_at: 2022-03-14
---

# [Django] ModelForm

`ModelForm`은 form을 상속받아 form처럼 동작하고 model과도 쉽게 연결지을 수 있다. 지정한 model로 부터 field를 불러와서 세팅할 수 있다. 

```python
#forms.py

class UserForm(forms.ModelForm):
  class Meta:
    model = User
    fields = '__all__'
```

## ModelForm을 활용한 create, edit 예시

```python
# views.py

def post_create(request):
    if request.method == "POST":
        form = PostForm(request.POST, request.FILES)
        if form.is_valid():
            post = form.save()
            return redirect('home')
    else:
        form = PostForm()
    context = {
        'form' : form
    }
    return render(request, 'core/post_form.html', context)


def post_edit(request, pk):
    post = get_object_or_404(Post,pk=pk)
    if request.method == "POST":
        form = PostForm(request.POST, request.FILES, instance=post)
        if form.is_valid():
            post = form.save()
            return redirect(home)
    else:
        form = PostForm(instance=post)
    context = {
        'form': form,
    }
    return render(request, 'core/post_form.html', context)
```

## commit = False

form을 통해 사용자에게 입력받은 내용을 저장하여 새로운 인스턴스를 만들수도 있지만, view에서 새로운 값을 넣을 수도 있다. 

```python
# models.py
class Post(models.Model):
    title = models.CharField(max_length=10)
    content = models.TextField()
    ip = models.CharField(max_length=20)

    def __str__(self):
        return self.title

# forms.py
class PostForm(forms.ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'content']
```

Model과 Form 위와 같을 때 `ip` field를 view에서 지정해주기 위한 코드는 아래와 같다. 

```python
# views.py
def post_create(request):
    if request.method == "POST":
        form = PostForm(request.POST, request.FILES)
        if form.is_valid():
            post = form.save(commit=False)
            post.ip = request.META['REMOTE_ADDR']
            post.save()
            return redirect('home')
    else:
        form = PostForm()
    context = {
        'form' : form
    }
    return render(request, 'core/post_form.html', context)
```

`commit=False`를 통해 잠시 저장을 미룬 후에 post를 받아와서 `ip` field를 채워준 후 다시 `save()`한다.

## cleand_data

form은 `request`로 부터 받아온 값을 유효성 검사 후에 `cleand_data`에 저장 해둔다. 그래서 form을 활용한다면 `request.POST` 보다 `cleand_data`를 이용하는 것이 더 좋다

```python
if request.method == "POST":
        form = PostForm(request.POST, request.FILES)
        if form.is_valid():
            # title = request.POST['title']
            title = form.cleand_data['title']
            return redirect('home')
```