---
title:  "[구현] 왕실의 나이트"
excerpt: "난이도 ★"

categories:
- Algorithm

toc: false
toc_sticky: false

date: 2021-09-27
last_modified_at: 2021-09-27
---

# [구현] 왕실의 나이트

- 문제

왕실 정원은 체스판과 같은 8 x 8 좌표 평면이다. 왕실 정원의 특정 한 칸에 나이트가 서있는데, 나이트는 L자 형태로만 이동할 수 있고 정원 밖으로는 나갈 수 없다. 나이트는 다음의 2가지 경우로 이동할 수 있다.

1. 수평으로 두 칸 이동한 뒤에 수직으로 한 칸 이동하기
2. 수직으로 두 칸 이동한 뒤에 수평으로 한 칸 이동하기

나이트가 이동 할 수 있는 경우의 수를 출력하는 프로그램을 작성하시오. 이 때 정원의 행 위치를 표현할 때는 1~8, 열 위치는 a~h로 표현한다.

<br>

- 입력 조건
  - 첫째 줄에 8 x 8 평면상 현재 나이트가 위치한 곳의 좌표를 나타내는 두 문자로 구성된 문자열 입력

- 입력 예시
```
a1
```

- 출력 예시
```
2
```
<br>

<hr>

<br>

<details>
<summary>답</summary>
<div markdown="1">
<br>

```python
data = input()

# 입력 받응 위치 행, 열 나누기
row = int(data[1])
column = int(ord(data[0])) - int(ord('a')) +1

# 나이트가 갈 수 있는 방향
steps = [(-2,-1),(-1,-2),(1,-2),(2,-1),(2,1),(1,2),(-1,2),(-2,1)]

result = 0
for step in steps:
  # 이동
  next_row = row + step[0] # step[0] = [-2,-1,1 ....]
  next_column = column + step[1]
  # 이동 한 범위가 정원 안 이면 result +1
  if next_row >= 1 and next_row <= 8 and next_column >= 1 and next_column <= 8:
    result +=1

print(result)
```

</div>
</details>

<br>