---
title:  "[Django] Custom User Model"
excerpt: "abstractuser, baseusermanager, ..."

categories:
- Django

toc: True
toc_sticky: True

date: 2022-04-02
last_modified_at: 2022-04-02
---

# [Django] Custom User Model

- 소스코드 : https://github.com/django/django/blob/main/django/contrib/auth/models.py

Django는 기본적으로 User model을 제공 하지만, 이 것만 가지고는 서비스를 만들기 어렵고 custom model을 만들기 위해서는 주로 `BaseUserManager`, `AbstractBaseUser` 클래스를 사용한다.

## BaseUserManager

```python
from django.contrib.auth.models import BaseUserManager
from django.db import models

class UserManager(BaseUserManager):
    def _create_user(self, email, username, password, gender = 1, **extra_fields):
        if not email :
            raise ValueError('The given email mist be set')
        email = self.normalize_email(email)
        username = self.model.normalize_username(username)
        user = self.model(email = email, username = username, gender=gender, **extra_fields)
        user.set_password(password)
        user.save (using = self._db)
        return user

    def create_user(self, email, username = '', password = None, **extra_fields):
        extra_fields.setdefault('is_staff', False)
        extra_fields.setdefault('is_superuser', False)
        return self._create_user(email, username, password, **extra_fields)
    
    def create_superuser(self, email, password, **extra_fields):
        extra_fields.setdefault('is_staff', True)
        extra_fields.setdefault('is_superuser', True)

        if extra_fields.get('is_staff') is not True:
            raise ValueError('Superuser must have is_staff = True')
        if extra_fields.get('is_superuser') is not True:
            raise ValueError('Superuser must have is_superuser = True')

        return self._create_user(email, username, password, **extra_fields)
```

`BaseUserManager` class는 유저를 생성 할 때 주로 사용하는 Helper class이고 실제 모델은 `AbstractBaseUser`를 상속 받아 생성한다.

- `create_user()` : is_staff, is_superuser 값에 False를 줘서 그냥 일반 사용자임을 지정, 필드값을 지정하고 `_create_user`로 보낸다.
- `create_superuser()` : is_staff, is_superuser 값에 True를 줘서 권한을 모두 주도록 한다.
- `_create_user()` : 파라미터로 전달 받은 필드 값들을 user 객체에 저장하고 DB에 저장한다.

## AbstractBaseUser

```python
class User(AbstractUser):
    email = models.EmailField(verbose_name = "email", max_length = 255, unique = True)
    username = models.CharField(max_length=30)
    gender = models.SmallIntegerField(choices = GENDER_CHOICES)

    objects = UserManager()

    # username 필드를 email 필드로 지정
    USERNAME_FIELD = 'email'
    # 필수 필드 지정
    REQUIRED_FIELDS = []
```

- `AbstractUser`을 상혹할 때는 `settings.py`에서 `AUTH_USER_MODEL = '폴더명.클래스명'`을 추가해야 migrate가 된다.
- User Model을 보면 `name`,`email` 등 필드가 있고 원하는 필드를 더 추가 할 수 있다.
- `AbstractUser`는 'username', 'first_name', 'last_name', ... 등의 필드를 기본으로 제공