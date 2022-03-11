---
title:  "2953번 나는 요리사다"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-02-19
last_modified_at: 2022-02-19
---

# 2953번 나는 요리사다

> 문제

"나는 요리사다"는 다섯 참가자들이 서로의 요리 실력을 뽐내는 티비 프로이다. 각 참가자는 자신있는 음식을 하나씩 만들어오고, 서로 다른 사람의 음식을 점수로 평가해준다. 점수는 1점부터 5점까지 있다.

각 참가자가 얻은 점수는 다른 사람이 평가해 준 점수의 합이다. 이 쇼의 우승자는 가장 많은 점수를 얻은 사람이 된다.

각 참가자가 얻은 평가 점수가 주어졌을 때, 우승자와 그의 점수를 구하는 프로그램을 작성하시오.

> 입력

총 다섯 개 줄에 각 참가자가 얻은 네 개의 평가 점수가 공백으로 구분되어 주어진다. 첫 번째 참가자부터 다섯 번째 참가자까지 순서대로 주어진다. 항상 우승자가 유일한 경우만 입력으로 주어진다.



> 출력

첫째 줄에 우승자의 번호와 그가 얻은 점수를 출력한다.


> 예제 입력

```
5 4 4 5
5 4 4 4
5 5 4 4
5 5 5 4
4 4 4 5
```

> 예제 출력

'''
4 19

'''

<br>

> 풀이

```python

# 1
score = [list(map(int,input().split())) for _ in range(5)]

score_sum = [0] * 5
max_score = 0

for i in range(5):
    temp = 0
    for j in range(4):
        temp += score[i][j]
    score_sum[i] = temp
    max_score = max(max_score, temp)

for i in range(5):
    if score_sum[i] == max_score:
        print(i+1, max_score)
        break

#2

score = []
for i in range(5):
    score.append(sum(map(int,input().split())))

print(score.index(max(score)+1), max(score))
```

- queue의 가장 앞을 뺀 후 최대값인지 확인
- 최댓값이면 빠진 상태로 두고 빠진 숫자의 개수 하나씩 세기
- 원하는 숫자가 빠져나가면 몇번째로 나갔는지 확인

