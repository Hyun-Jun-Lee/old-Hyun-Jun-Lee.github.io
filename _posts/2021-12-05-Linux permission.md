---
title:  "[LINUX] Linux Permission"
excerpt: "Permission 명령어"

categories:
- Linux

toc: True
toc_sticky: True

date: 2021-12-04
last_modified_at: 2021-12-04
---

# Linux permission

<br>

## 권한 조회

```bash
ls -al
```

![image](https://user-images.githubusercontent.com/76996686/144702327-4396074c-a757-4bea-8ab6-24a05d7e48b7.png)

접근권한 표시

- 1번째 자리는 파일 유형
- 2~4번째는 소유자 권한
- 5~7번째는 그룹 권한
- 8~10번째는 게스트 권한 

ex) `drwxrwxrwx`
- 디렉토리(d)
- 소유자에게 읽기(r)/쓰기(w)/실행(x) 권한이 있음
- 그룹에게 읽기(r)/쓰기(w)/실행(x) 권한이 있음
- 게스트에게 읽기(r)/쓰기(w)/실행(x) 권한이 있음

<br>

## 접근권한 문자열

- 접근권한(permission)
  - r : 읽기
  - w : 쓰기
  - x : 실행
- 연산
  - + : 권한 추가
  - - : 권한 제거
  - = : 권한 부여
- 사용자
  - u : user, 소유자
  - g : group, 그룹
  - o : other, 일반 사용자
  - a : all

ex)
- ug+x : '소유자'오 '그룹에' '실행' 권한 추가
- +x : '모든 사용자'에게 '실행' 권한 추가
- u=rx : '소유자'에게 '읽기', '쓰기' 권한 부여

<br>

## 접근권한 숫자열

![image](https://user-images.githubusercontent.com/76996686/144702725-029ed5f0-5722-4b98-9cce-eaba631e07a9.png)
