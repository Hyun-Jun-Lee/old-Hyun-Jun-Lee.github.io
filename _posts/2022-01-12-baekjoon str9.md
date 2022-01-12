---
title:  "[문자열] 2941번 크로아티아 알파벳"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-12
last_modified_at: 2022-01-12
---

# [문자열] 2941번 크로아티아 알파벳

> 문제

> 입력

첫째 줄에 최대 100글자의 단어가 주어진다. 알파벳 소문자와 '-', '='로만 이루어져 있다.

단어는 크로아티아 알파벳으로 이루어져 있다. 문제 설명의 표에 나와있는 알파벳은 변경된 형태로 입력된다.

> 출력

입력으로 주어진 단어가 몇 개의 크로아티아 알파벳으로 이루어져 있는지 출력한다.

> 예제 입력

ljes=njak

> 예제 출력

6

<br>

> 풀이

```python
word = input()
cro_alpha = ['c=','c-','dz=','d-','lj','nj','s=','z=']

for alpha in cro_alpha:
    word = word.replace(alpha, 'x')

print(len(word))
```

크로아티아 알파벳은 2,3글자로 이루어져 있는데, 이 것을 한글자로 변환하고 나서 총 글자수를 세면 됨.

```python
>>> cro_alpha = ['c=','c-','dz=','d-','lj','nj','s=','z=']
>>> for i in cro_alpha :
>>>     word = word.replace(i, '*')
>>>     print(word)
>>> print(len(word))

ljes=njak
ljes=njak
ljes=njak
ljes=njak
*es=njak
*es=*ak
*e**ak
*e**ak
6
```