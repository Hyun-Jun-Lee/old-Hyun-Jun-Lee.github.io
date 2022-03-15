---
title:  "[Django] queryset"
excerpt: "DB 조회"

categories:
- Django

toc: True
toc_sticky: True

date: 2022-03-14
last_modified_at: 2022-03-14
---

# [Django] queryset

`queryset`은 DB에 정보를 요청하는 것을 뜻하고 python으로 작성한 코드가 sql로 매핑되어 `queryset`이라는 자료 형태로 넘어 온다.

## 다양한 조회 방법

- 조회 요청 방법
    - `User.objects.all()` : 모든 데이터 조회
    - `User.objects.filter()` : 특정 조건에 맞는 데이터만 조회. `필드명=조건값`이 들어가고 2개이상일 경우 Q를 사용해서 and로 묶어줘야한다. (`Post.objects.filter(Q(title="리뷰" | Q(comment="내용")))`)
    - `User.objects.exclude()` : 특정 조건을 제외한 데이터만 조회
    - `User.objects.get()` : `필드명=조건값`을 인자로 가지고 해당하는 조건의 데이터가 유일하게 존재할 때만 사용가능, 유일하지 않으면 에러
    - `User.objects.first() | .last()` : 첫번째와 마지막 데이터 조회

- `필드명__조건 = 조건값` 형태로도 조회 가능
  - `필드명__lt = 조건값` : 필드명 < 조건값
  - `필드명_gt = 조건값` : 필드명 > 조건값 

- 문자열 필드
  - `필드명__startwith = 조건값` : 조건값으로 시작하는 데이터 모두 조회(끝나는 데이터는 `필드명__endswith`)
  - `필드명__contatins = 조건값` : 조건값이 포함되는 데이터 모두 조회
  - i가들어가면 대소 문자 구분 X (`istartwith`, `iendswith`, ...)