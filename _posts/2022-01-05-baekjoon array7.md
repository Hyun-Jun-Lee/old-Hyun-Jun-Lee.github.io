---
title:  "[1차원배열] 4344번 평균은 넘겠지"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-05
last_modified_at: 2022-01-05
---

# [1차원배열] 4344번 평균은 넘겠지

> 문제

대학생 새내기들의 90%는 자신이 반에서 평균은 넘는다고 생각한다. 당신은 그들에게 슬픈 진실을 알려줘야 한다.


> 입력

첫째 줄에는 테스트 케이스의 개수 C가 주어진다.

둘째 줄부터 각 테스트 케이스마다 학생의 수 N(1 ≤ N ≤ 1000, N은 정수)이 첫 수로 주어지고, 이어서 N명의 점수가 주어진다. 점수는 0보다 크거나 같고, 100보다 작거나 같은 정수이다.

> 출력

각 케이스마다 한 줄씩 평균을 넘는 학생들의 비율을 반올림하여 소수점 셋째 자리까지 출력한다.

<br>

> 풀이

```python
n = int(input())

for _ in range(n):
    arr = list(map(int, input().split()))
    avg = sum(arr[1:])/arr[0]
    over_avg = 0
    for score in arr[1:]:
        if score > avg:
            over_avg +=1
    res = over_avg/arr[0] * 100
    print(f'{res:.3f}%')
```

'5 50 50 70 80 100' 와 같이 입력이 되므로 `arr[0]` = 학생수 / `arr[1]` = 점수

두번째 for문에서 학생의 점수가 avg 이상이라면 over_avg에 +1씩 누적시켜서 카운트

f-string으로 소수 세번째 자리 까지 출력 되로록
