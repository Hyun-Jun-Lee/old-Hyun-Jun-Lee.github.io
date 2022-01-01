---
title:  "[1차원배열] 3052번 나머지"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-01
last_modified_at: 2022-01-01
---

# [1차원배열] 3052번 나머지

> 문제

두 자연수 A와 B가 있을 때, A%B는 A를 B로 나눈 나머지 이다. 예를 들어, 7, 14, 27, 38을 3으로 나눈 나머지는 1, 2, 0, 2이다. 

수 10개를 입력받은 뒤, 이를 42로 나눈 나머지를 구한다. 그 다음 서로 다른 값이 몇 개 있는지 출력하는 프로그램을 작성하시오.

> 입력

첫째 줄부터 열번째 줄 까지 숫자가 한 줄에 하나씩 주어진다. 이 숫자는 1,000보다 작거나 같고, 음이 아닌 정수이다.

> 출력

첫째 줄에, 42로 나누었을 때, 서로 다른 나머지가 몇 개 있는지 출력한다.

<br>

> 풀이

```python
a = int(input())
b = int(input())
c = int(input())

num = list(str(a * b * c)) # [1,7,0,3,7,3,0,0]

for i in range(10):
    print(num.count(str(i)))
```

- a,b,c를 입력 받고 곱한 후 str형으로 변환 후 list로 묶어주기
- `count()` 메서드 