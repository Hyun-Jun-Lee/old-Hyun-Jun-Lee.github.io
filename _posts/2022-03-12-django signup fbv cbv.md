---
title:  "[Django] django SignUp FBV vs CBV"
excerpt: "SignUp 예시로 FBV CBV 차이 알아보기"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-03-12
last_modified_at: 2022-03-12
---

# [Django] django SignUp FBV vs CBV

## SignUp by FBV

FBV 방식에서는 `GET` method 요청이 오면 page를 보여주고, `POST` method 요청은 client로 부터 온 data를 처리한다.

> users/views.py

```python
from django.shortcuts import render, redirect, reverse
from django.core.exceptions import ValidationError
from . import models

def SignUp(request):
    if request.method == "GET":
        genders = models.User.GENDER_CHOICES
        languages = models.User.LANGUAGE_CHOICES
        currencies = models.User.CURRENCY_CHOICES

        choices = {
            "genders": genders,
            "languages": languages,
            "currencies": currencies,
        }

        return render(request, "templates/users/signup.html", context={**choices})
    elif request.method == "POST":
        email = request.POST.get("email")
        if email is None:
            return redirect(reverse("users:signup"))

        try:
            # if email alredy exists raise Error with message
            models.User.objects.get(email=email)
            raise ValidationError("User already exists")
        except models.User.DoesNotExist:
            password = request.POST.get("password")
            if password is None:
                return redirect(reverse("users:signup"))

            password1 = request.POST.get("password1")
            if password1 is None:
                return redirect(reverse("users:signup"))

            if password != password1:
                raise ValidationError("Password confirmation does not match")
            user = models.User.objects.create_user(
                username=email, email=email, password=password1
            )
```

### FBV with Form

> usrs/forms.py

`forms.ModelForm`을 상속받아 사용하기 위해서는 `class Meta`에 있는 `model`과 `fields` 필드의 정의가 `반드시 필요`하다.

```python
from django import forms
from . import models

class SignUpForm(forms.ModelForm):
    class Meta:
        model = models.User
        fields = ("first_name", "last_name", "email")
        # wigets은 만들어진 필드에 속성 등을 추가하는 기능
        widgets = {
            "first_name": forms.TextInput(attrs={"placeholder": "First Name"}),
            "last_name": forms.TextInput(attrs={"placeholder": "Last Name"}),
            "email": forms.EmailInput(attrs={"placeholder": "Email Name"}),
        }

    # 유효성 검사
    def clean_email(self):
        email = self.cleaned_data.get("email")
        try:
            models.User.objects.get(email=email)
            raise forms.ValidationError("User already exists with that email")
        except models.User.DoesNotExist:
            return email
```

> users/views.py (with Form)

```python
from django.shortcuts import render, redirect, reverse
from django.contrib.auth import authenticate
from . import forms

def SignUp(request):
    if request.method == "GET"L
    form = froms.SignUpForm
    return render(request, "templates/usrs/signup.html")
    elif request.method == "POST":
        form = mroms.SignUpForm

        if form.is_valid():
            form.save()
            email = form.cleaned_data.get("email")
            password = form.cleaned_data.get("password")
            # authenticate() : 자격증명이 유효하면 usr 객채 생성, 유효하지 않으면 None
            user = authenticate(request, username=email, password=password)
            user.save()
            return redirect(reverse("core:home"))
        else:
            return redirect(reverse("users:home"))
```

## SignUp by CBV

CBV 방식에서는 django에서 제공하는 다양한 View를 이용한다.
FormView를 상속받아 사용하고 여러가지 attribute와 funcition이 있다.

- `form_class` : forms.py에서 만든 form으로 지정
- `success_url` : class가 성공했을 때 이동할 url(get_success_url)
- `template_name` : html 템플릿 지정
- `form_valid()` : form의 유효성 검사

```python
from django.contrib.auth import authenticate
from django.views.generic import FormView
from django.db.utils import IntegrityError
from django.shortcuts import redirect, reverse
from django.urls import reverse_lazy
from . import forms


class SignUpView(FormView):
    form_class = forms.SignUpForm
    success_url = reverse_lazy("core:home")
    template_name = "pages/users/signup.html"

    def form_valid(self, form):
        try:
            form.save()
            email = form.cleaned_data.get("email")
            password = form.cleaned_data.get("password")
            authenticate(self.request, username=email, password=password)
            return super().form_valid(form)
        except IntegrityError as error:
            print(error)
            return redirect(reverse("users:signup"))
```