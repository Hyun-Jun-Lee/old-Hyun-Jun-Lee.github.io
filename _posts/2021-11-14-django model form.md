---
title:  "[Django] django ModelForm"
excerpt: "django Form"

categories:
- Django

toc: True
toc_sticky: True

date: 2021-11-14
last_modified_at: 2021-11-14
---


<br>

# Django ModelForm

- django Form을 상속
- 지정된 Model로 부터 정보를 받아 Form Fields 세팅
- 유효성 검사 통과한 값들을 save 지원(`ModelForm.save(commit=True,False)`)
- model과 관련된 폼은 ModelForm사용 권장

<br>

## View에서 ModelForm 처리

- New

```python
def post_new(request):
    if request.method	==	'POST':
        form	=	PostModelForm(request.POST,	request.FILES)
    if form.is_valid():
        post	=	form.save()
        return redirect(post)
    else:
        form	=	PostModelForm()
    return render(request,	'myapp/post_form.html',	{
        'form':	form,
    })
```

- Edit

```python
def post_edit(request, id):
	post = get_object_or_404(Post, id=id)

	if request.method == 'POST':
		form = PostModelForm(request.POST, request.FILES, instance=post) # instance : 인자(수정대상) 지정
		if form.is_valid():
			post = form.save()
			return redirect(post) # post 인스턴스의 get_absolute_url 메소드 호출!
	else:
		form = PostModelForm(instance=post)
	return render(request, 'myapp/post_form.html',{
		'form': form,
	})
```

<br>

### save(commite=False) 예시

```python
# app/models.py
class Comment(models.Model):
    author	=	models.CharField(max_length=20)
    message	=	models.TextField()
    ip	=	models.CharField(max_length=15)

# app/forms.py
class CommentForm(forms.ModelForm):
    class Meta:
        model	=	Comment
        #	ip필드는 유저로부터 입력받지 않고,	프로그램으로 채워넣을 것이기에 제외
        fields	=	['author',	'message']

# app/views.py
def comment_new(request):
    if request.method	==	'POST':
        form	=	CommentForm(request.POST,	request.FILES)
    if form.is_valid():
        comment	=	form.save(commit=False) # 필수필드인 ip 값을 아직 안채웟으니 false
        comment.ip	=	request.META['REMOTE_ADDR']		#	IP를 기록하고
        comment.save()	#	save()
        return redirect('/')
    else:
        form	=	CommentForm()
    return render(request,	'myapp/comment_form.html',	{'form':	form})
```

<br>

### request.POST[‘key’] 보다는 form.cleaned_data[‘key’]사용하기

- request.POST 데이터는 초기 데이터로 변경될 가능성이 잇음

```python
# BAD case
form = CommentForm(request.POST)
if form.is_valid():
    # request.POST : 폼 인스턴스 초기 데이터
    message = request.POST['message']
    comment = Comment(message=message)
    comment.save()
    return redirect(post)

# Good case
form = CommentForm(request.POST)
if form.is_valid():
    # form.cleaned_data : 폼 인스턴스 내에서 clean 함수를 통해 변환되었을 수도 있을 데이터
    message = form.cleaned_data['message']
    comment = Comment(message=message)
    comment.save()
    return redirect(post)
```