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