---
title:  "[DRF] JWT"
excerpt: "DRF with JWT"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-03-26
last_modified_at: 2022-03-26
---

# [Django] JWT

## JWT

JWT는 개방형 표준으로 당사자간에 정보를 JSON 객체로 안전하게 전송하기 위한 간결하고 독립적인 방법이다. 

- JSON 형태를 사용하는 이유?
  - 인코딩 후 크기가 작아져 HTML,HTTP 환경에서 전달하기 좋다
  - 공개/개인 키 쌍을 사용할 수 있다.

- 동작 방식
  1. 클라이언트에서 id, pw 정보를 서버로 보냄
  2. 서버에서 id, pw 정보를 이용하여 JWT token 을 생성함
  3. 서버에서 클라이언트로 JWT token 을 보냄
  4. 클라이언트에서 서버로 서비스 요청시, JWT token 을 같이 보냄.
  5. 서버에서 서비스 처리시, JWT token 을 검증, 일치하면 서비스를 동작시켜 클라이언트로 응답


- 구성
  - Header : 토큰 타입 및 해싱 알고리즘 지정(ex. 토큰 타입 = JWT, 해싱 알고리즘 = SHA256)
  - Payload : 토큰에 담을 정보(클레임)이 들어 있음
  - Signature : 헤더의 인코딩 값과 정보의 인코딩 값을 합친 후 비밀키로 해쉬하여 생성

- 장점
  - 사용자 인증에 필요한 정보가 토큰 자체에 포함되서 별도의 인증 저장소가 필요 없음(DB,서버에 의존 X)
  - 쿠키를 전달하지 않아도 되서 발생하는 취약점 예방 가능
  - REST 서비스로 제공 가능
- 단점
  - 토큰 자체에 정보를 담고 있어서 양날의 검
  - 정보가 많아질수록 토큰의 길이가 늘어나 네트워크에 부하 줄 수 있음
  - Payload 자체가 암호화 된것이 아니라서 중간에 탈취하여 데이터를 볼수도 있기 때문에 중요한 데이터를 넣으면 안됨

## DRF with JWT

### settings.py

- 필요 패키지
  - `django-allauth`
  - `django-rest-auth`
  - `djangorestframework-jwt`

```python

INSTALLED_APPS = [
    ...,

    'rest_auth.registration',
    'rest_framework.authtoken', 
    'rest_auth',
    
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'django.contrib.sites',
    ...,
]

## DRF 
REST_FRAMEWORK = {
    # 권한 지정
    'DEFAULT_PERMISSION_CLASSES': (
        'rest_framework.permissions.IsAuthenticated', # 인증된 사용자만 접근 가능
        'rest_framework.permissions.IsAdminUser', # 관리자만 접근 가능
        'rest_framework.permissions.AllowAny', # 누구나 접근 가능
    ),
	
    # 기본 인증 방식 JWT로 설정
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_jwt.authentication.JSONWebTokenAuthentication',
    ),
}

# 추가적인 JWT_AUTH 설젇
JWT_AUTH = {
    'JWT_SECRET_KEY': SECRET_KEY,
    'JWT_ALGORITHM': 'HS256', # 암호화 알고리즘
    'JWT_ALLOW_REFRESH': True, # refresh 사용 여부
    'JWT_EXPIRATION_DELTA': datetime.timedelta(days=7), # 유효기간 설정
    'JWT_REFRESH_EXPIRATION_DELTA': datetime.timedelta(days=28), # JWT 토큰 갱신 유효기간
    # 인자로 받은 payload를 secret key 또는 public/private key 를 이용하여 인코딩을 진행
    'JWT_ENCODE_HANDLER': 'rest_framework_jwt.utils.jwt_encode_handler',
    # 유저의 정보를 딕셔너리 형태의 payload로 만들어줌
    'JWT_PAYLOAD_HANDLER': 'rest_framework_jwt.utils.jwt_payload_handler',
    'JWT_DECODE_HANDLER': 'rest_framework_jwt.utils.jwt_decode_handler',
}
```

### serializers.py

<a href="https://jpadilla.github.io/django-rest-framework-jwt/">공식 document</a>

```python
from rest_framework import serializers
from rest_framework import status
from django.contrib.auth import get_user_model
from django.contrib.auth.models import update_last_login
from django.contrib.auth import authenticate
from rest_framework_jwt.settings import api_settings
from .models import User

# JWT 사용을 위한 설정
JWT_PAYLOAD_HANDLER = api_settings.JWT_PAYLOAD_HANDLER
JWT_ENCODE_HANDLER = api_settings.JWT_ENCODE_HANDLER

class UserLoginSerializer(serializers.Serializer):
    username = serializers.CharField(max_length=30)
    password = serializers.CharField(max_length=128, write_only=True)
    token = serializers.CharField(max_length=255, read_only=True)

    def validate(self, data):
        username = data.get("username")
        password = data.get("password", None)
        user = authenticate(username=username, password=password)

        if user is None:
            raise serializers.ValidationError("is Not Found")
        try:
            payload = JWT_PAYLOAD_HANDLER(user) # payload 생성
            jwt_token = JWT_ENCODE_HANDLER(payload) # jwt token 생성
            # user의 'last_login' 필드를 현재 시간으로 update
            update_last_login(None, user)

        except User.DoesNotExist:
            raise serializers.ValidationError(
                'User with given username and password does not exist'
            )
        return {
            'id':user.id,
            'token': jwt_token
        }
```

### views.py

```python
from rest_framework.response import Response
from rest_framework import status
from rest_framework import generics
from .serializers import UserRegistrationSerializer, UserLoginSerializer

class UserLoginView(GenericAPIView):

    # permission_classes를 지정하지 않으면, settings.py에서 정한 permission default 값이 작동되어 에러
    permission_classes = (AllowAny,)
    serializer_class = UserLoginSerializer

    def post(self, request):
        serializer = self.serializer_class(data=request.data)

        if not serializer.is_valid():
            return Response({"message": "It's Not Valid"}, status = status.HTTP_400_BADREQUEST)

        serializer.is_valid(raise_exception=True)
        response = {
            "success": "True",
            "status_code": status.HTTP_200_OK,
            "message": "User Logged in successfully",
            # is_valid()로 입력된 data의 token을 불러옴
            "token": serializer.data['token'],
        }

        return Response(response, status=status.HTTP_200_OK)
```