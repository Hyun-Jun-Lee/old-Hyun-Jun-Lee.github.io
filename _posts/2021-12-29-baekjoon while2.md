---
title:  "[While] 10951번 A+B-4"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2021-12-29
last_modified_at: 2021-12-29
---

# [While] 10951번 A+B-4

> 문제

두 정수 A와 B를 입력받은 다음, A+B를 출력하는 프로그램을 작성하시오.

> 입력

입력은 여러 개의 테스트 케이스로 이루어져 있다.

각 테스트 케이스는 한 줄로 이루어져 있으며, 각 줄에 A와 B가 주어진다. (0 < A, B < 10)

> 출력

각 테스트 케이스마다 A+B 출력

<br>

> 풀이

```python
while True:
    try:
        a,b = map(int,input().split())
        print(a+b)
    except:
        break
```

- `While True`로 while문을 무한루프로
- 테스트 케이스의 총 수가 따로 주어지지 않았으니까 `try-expect` 활용
  - try : a,b에 int형 입력 받고 a+b 출력
  - except : try에 에러가 발생한 경우(더이상 입력값이 없는 경우, int형이 아닌 값이 입력된 경우) break
