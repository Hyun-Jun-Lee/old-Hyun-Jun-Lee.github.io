---
title:  "[함수] 1065번 한수"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-07
last_modified_at: 2022-01-07
---

# [함수] 1065번 한수

> 문제

어떤 양의 정수 X의 각 자리가 등차수열을 이룬다면, 그 수를 한수라고 한다. 등차수열은 연속된 두 개의 수의 차이가 일정한 수열을 말한다. N이 주어졌을 때, 1보다 크거나 같고, N보다 작거나 같은 한수의 개수를 출력하는 프로그램을 작성하시오. 

> 입력

첫째 줄에 1,000보다 작거나 같은 자연수 N이 주어진다.

> 출력

첫째 줄에 1보다 크거나 같고, N보다 작거나 같은 한수의 개수를 출력한다.

<br>

> 풀이

```python
n = int(input())

cnt = 0
for i in range(1,n+1):
    num_list = list(map(int,str(i)))
    if i < 100:
        cnt += 1
    elif num_list[0] - num_list[1] == num_list[1] - num_list[2]:
        cnt += 1

print(cnt)
```

- 등차수열 : 연속된 두 개의 수의 차이가 일정한 수열

i를 str형으로 바꿔서 각 자리수 별로 num_list에 넣는다.

이 문제에서 두 자리 숫자는 등차수열인지 비교대상이 없기 때문에 모두 한수이고 세자리 숫자는 각 자리의 숫자 간격이 동일하면 한수이다. 

'연속된 두개 수의 차이'가 같다면 등차수열 -> `num_list[0] - num_list[1] == num_list[1] - num_list[2]`