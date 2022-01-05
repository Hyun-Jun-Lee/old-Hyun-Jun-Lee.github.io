---
title:  "[1차원배열] 8958번 OX퀴즈"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-05
last_modified_at: 2022-01-05
---

# [1차원배열] 1546번 평균

> 문제

"OOXXOXXOOO"와 같은 OX퀴즈의 결과가 있다. O는 문제를 맞은 것이고, X는 문제를 틀린 것이다. 문제를 맞은 경우 그 문제의 점수는 그 문제까지 연속된 O의 개수가 된다. 예를 들어, 10번 문제의 점수는 3이 된다.

"OOXXOXXOOO"의 점수는 1+2+0+0+1+0+0+1+2+3 = 10점이다.

OX퀴즈의 결과가 주어졌을 때, 점수를 구하는 프로그램을 작성하시오.

> 입력

첫째 줄에 테스트 케이스의 개수가 주어진다. 각 테스트 케이스는 한 줄로 이루어져 있고, 길이가 0보다 크고 80보다 작은 문자열이 주어진다. 문자열은 O와 X만으로 이루어져 있다.

> 출력

각 테스트 케이스마다 점수를 출력한다.

<br>

> 풀이

```python
n = int(input())

for i in range(n):
    arr = list(input())
    score = 0
    sum_score = 0
    for j in arr:
        if j == 'O':
            score += 1
            sum_score += score
        else:
            score=0
    print(sum_score)
```

for문으로 arr에서 하나씩 꺼내서 'O'가 연속해서 나올 경우 score를 1씩 증가 시키고 sum_score에 더한다. 

'O'가 아닐 경우 `else`구문으로 가서 score를 0으로 만들어줌