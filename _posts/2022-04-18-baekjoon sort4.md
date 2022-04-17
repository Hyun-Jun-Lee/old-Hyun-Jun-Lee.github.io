---
title:  "[sort] 2108번 통계학"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-04-18
last_modified_at: 2022-04-18
---

# [sort] 2108번 통계학

> 문제

수를 처리하는 것은 통계학에서 상당히 중요한 일이다. 통계학에서 N개의 수를 대표하는 기본 통계값에는 다음과 같은 것들이 있다. 단, N은 홀수라고 가정하자.

- 산술평균 : N개의 수들의 합을 N으로 나눈 값
- 중앙값 : N개의 수들을 증가하는 순서로 나열했을 경우 그 중앙에 위치하는 값
- 최빈값 : N개의 수들 중 가장 많이 나타나는 값
- 범위 : N개의 수들 중 최댓값과 최솟값의 차이

N개의 수가 주어졌을 때, 네 가지 기본 통계값을 구하는 프로그램을 작성하시오.

> 입력

첫째 줄에 수의 개수 N(1 ≤ N ≤ 500,000)이 주어진다. 단, N은 홀수이다. 그 다음 N개의 줄에는 정수들이 주어진다. 입력되는 정수의 절댓값은 4,000을 넘지 않는다.

> 출력

첫째 줄에는 산술평균을 출력한다. 소수점 이하 첫째 자리에서 반올림한 값을 출력한다.

둘째 줄에는 중앙값을 출력한다.

셋째 줄에는 최빈값을 출력한다. 여러 개 있을 때에는 최빈값 중 두 번째로 작은 값을 출력한다.

넷째 줄에는 범위를 출력한다.

> 예제 입력

```
5
-1
-2
-3
-1
-2
```

> 예제 출력

'''
-2
-2
-1
2
'''

<br>

> 풀이

```python
import sys
from collections import Counter

n = int(sys.stdin.readline())
num = []

for _ in range(n):
    num.append(int(sys.stdin.readline()))

# 평균값
print(round(sum(num)/len(num)))

# 중앙값
num.sort()
print(num[len(num)//2])

# 최빈값
cnt = Counter(num).most_common(2)

if len(num)>1:
    # 최빈 수가 같을 때 두번째로 작은 수 출력
    if cnt[0][1] == cnt[1][1]:
        print(cnt[1][0])
    else:
        print(cnt[0][0])
else:
    print(cnt[0][0])

# 범위
print(max(num) - min(num))
```

- 최빈값

```python
# 최빈값
cnt = Counter(num).most_common(2)

if len(num)>1:
    # 최빈 수가 같을 때 두번째로 작은 수 출력
    if cnt[0][1] == cnt[1][1]:
        print(cnt[1][0])
    else:
        print(cnt[0][0])
else:
    print(cnt[0][0])
```

> Counter 함수 예시

```python
cnt = Counter(num)
print(cnt)
# Counter({-2:2, -1:2, -3:1})

# Counter(a).most_common(n)   : a의 요소를 세어, 최빈값 n개를 반환합니다. (리스트에 담긴 튜플형태로)
cnt = Counter(num).most_common(2)
print(cnt)
# [(-2,2), (-1,2)]
```

- Counter를 쓰지않을 때 참고 코드

```python
# 최빈값

# zip(key,value)로 dict 구성
cnt_dict = dict(zip(num, [0]*len(num)))

# 등장 횟수 check(+1)
for n in nums:
    cnt_dict[n] +=1

# k : Key값(최빈수), v : Values값(등장횟수)
cnt = [k for k, v in cnt_dict.items() if v == max(cnt_dict.values())]
print(cnt)
```

