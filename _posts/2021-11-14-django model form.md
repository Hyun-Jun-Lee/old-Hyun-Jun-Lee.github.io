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

## 

- forms.Form : 직접 필드 정의, 위젯 설정 필요

```python
class PostForm(forms.Form):
  title = forms.CharField()
  content = forms.CharField(widget=forms.Textarea)
```

- forms.ModelForm : 모델과 필드를 지정하면 모델폼이 자동으로 폼 필드를 생성

```python
class PostForm(forms.ModelForm):
	class Meta:
		model = Post
		fields = ['title', 'content']
```

<br>

## Django Form style

- 하나의 URL(하나의 view)에서 2가지 역할 수행
  - 빈 form 보여주기
  - form에 입력된 값 검증 및 저장

<br>

- GET 요청
  - New/Edit 입력폼을 보여줌
- POST 요청
  - 데이터 입력 받아(resuset.POST, request.FILES) 유효성 검사
    - 검사 성공 -> 데이터 저장 후 Success url로 이동
    - 검사 실패 -> error message + 입력폼 다시 보여줌

```python
def post_new(request):
    if request.method	==	'POST':
      form	=	PostForm(request.POST,	request.FILES)
      if form.is_valid(): #유효성 검사 성공 시
        post	=	Post(**self.cleaned_data)
        post.save()
        return redirect(post)

    else: # GET 요청일 때
      form	=	PostForm()

    return render(request,	'blog/post_form.html',	{
      'form':	form,
    })
```

<br>

## Form 구현 순서

### 1. Form/ModelForm class 정의

```python
# app/forms.py
class PostForm(forms.Form):
    title = models.CharField(max_length=100)
    content = models.TextField()
```

### 2. fields 별로 유효성 검사 

```python
# app/forms.py
def min_length_3_validator(value):
    if len(value) < 3:
      raise forms.ValidationError('3글자 이상 입력해주세요')

class PostForm(forms.Form):
	  title = forms.CharField(validators=[min_length_3_validator])
    content = models.TextField()
```

<br>

- but model에 validators 정의하는 것이 좋음
  - admin 사이트에서도 동작
  - Model Form에 그대로 적용 가능

```python
# app/models.py
def min_length_3_validator(value):
    if len(value) < 3:
      raise forms.ValidationError('3글자 이상 입력해주세요')

class Post(models.Model):
	  arField(max_length=100, validators=[min_length_3_validator])
```

<br>

### 3. 함수 내에서 form 인스턴스 생성

```python
# app/views.py
def post_new(request):
    if request.method == 'POST':
      form = PostForm(request.POST, request.FILES) # 인자 순서주의 POST, FILES
    else:
      form = PostForm()
    return render(request, 'dojo/post_form.html',{
      'form': form,
    })
```

<br>

### 4. POST 요청은 입력값 유효성 검사

```python
if request.method	==	'POST':
    #	POST인자는 request.POST와 request.FILES를 제공받음.
    form	=	PostForm(request.POST,	request.FILES)

    #	인자로 받은 값에 대해서,	유효성 검증 수행
    if form.is_valid():	#	검증이 성공하면	True	리턴
        #	검증에 성공한 값들을 사전타입으로 제공받음
        form.cleaned_data
        # 필요에 따 이 값을 DB에 저장
        post	=	Post(**form.cleaned_data)
        # 필요에 따 이 값을 DB에 저장
        post.save()
        # Model 클래스에 정의된 get_absolute_url() 메소드 호출
        return redirect('/success_url/')

    else:	#	검증에 실패하면,	form.errors와 form.각필드.errors	에 오류정보를 저장
        form.errors

else: #	GET	요청일 때
    form	=	PostForm()
    return render(request,	'myapp/form.html',	{'form':	form})
```

<br>

### 5. 템플릿 통해 HTML 폼 생성 

- GET 요청일 때
  - 유저가 Form 입력 후 Submit -> POST 요청
- POST 요청이지만, 유효성 검증 실패일 때
  - Form 인스턴스 통해 HTML 폼 출력(오류메세지도 같이 출력)
  - 유저가 Form 채우고 Submit -> POST 재요청

```html
<form action="" method="post">
    {% csrf_token %}
    <table>
      {{ form.as_table }}
    </table>
    <input type="submit">
</form>
```

## Form Fields

- Models Fields : DB fields를 python 클래스화
- Form Fields : HTML Form fields를 python 클래스화