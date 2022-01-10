---
title:  "[Django] django static"
excerpt: "django에서 css/js, media 파일 처리"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-01-10
last_modified_at: 2021-01-10
---

# [Django] django static

<br>

## Static & Media

- Static 파일
  - 개발 리소스의 정적인 파일(css, js, image 등)
  - app, project 단위로 저장 및 서빙

- Media 파일
  - FileField/ImageField를 통해 저장한 모든 파일
  - DB에는 '저장경로'를 저장하고, 실제 파일은 파일 스토리지에 저장
  - project 단위로 저장 및 서빙

<br>

## Static

### Static 경로

django는 하나의 Project에 다수의 App 구조로, 하나의 App을 위한 static 파일을 `app/static/app` 경로에 저장.

Project 전반적으로 사용되는 static 파일은 `settings.STATICFILES_DIRS`에 지정된 경로에 저장함.

다수의 디렉토리에 저장된 static 파일은 `python manage.py collectstatic` 명령어를 통해, `settings.STATIC_ROOT`에서 지정한 경로로 복사해서 서비스에 사용.