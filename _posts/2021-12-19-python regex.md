---
title:  "Python 정규표현식"
excerpt: "정규 표현식 기초, 반복"

categories:
- Python

toc: True
toc_sticky: True

date: 2021-12-19
last_modified_at: 2021-12-19
---

# 정규표현식

## 문자클래스

- `\d` : 숫자 매치, [0-9]와 동일
- `\D` : 숫자 외의 것 매치, [^0-9]
- `\s` : whitespace와 매치, [ \t\n\r\f\v]와 동일(맨 앞의 빈 칸은 공백(space)를 의미)
- `\S` : whitespace가 아닌 것과 매치, [^ \t\n\r\f\v]와 동일
- `\w` : 문자+숫자(alphanumeric)와 매치, [a-zA-Z0-9_]와 동일
- `\W` : 문자+숫자(alphanumeric)가 아닌 문자와 매치, [^a-zA-Z0-9_]와 동일

<br>

## 반복

- `*` : `*` 앞에 있는 문자가 무한 반복 될 수 있다는 것을 의미
  - ex1) 문자열='caaat', 정규식=`ca*t` -> 'a'가 3번 반복되어 매치

- `+` : chlth 1qjsdltkd qksqhr
  - ex1) 문자열='ct', 정규식=`ca+t` -> 'a'가 3번 반복되어 매치
