---
title:  "[구현] 상하좌우"
excerpt: "난이도 ★"

categories:
- Algorithm

toc: false
toc_sticky: false

date: 2021-09-26
last_modified_at: 2021-10-17
---

# [구현] 상하좌우

- 문제

A는 N x N 크기의 정사각형 공간에 있다. 각 위치의 좌표는 (N,N)이고 A는 상하좌우 방향으로 움직일 수 있다. 
시작 좌표는 항상 (1,1)이다. 계획서에는 L, R, U, D가 적혀있고 각 방향으로 한칸 이동한다.
계획서가 주어졌을 때, A가 최종적으로 도착할 지점의 좌표를 출력하는 프로그램을 작성하시오

<br>

- 입력 조건
  - 첫째 줄에 공간의 크기를 나타내는 N이 주어짐
  - 둘째 줄에 A가 이동할 계획서가 주어짐

- 입력 예시
```
5
R R R U D D
```

- 출력 예시
```
3 4
```
<br>

<hr>

<br>

<details>
<summary>답</summary>
<div markdown="1">
<br>
n = map(int, input().split())
data = list(map(str, input().split()))

x, y = 1, 1

for i in data:
  if i=='L':
    y -=1
  elif i=='R':
    y +=1
  elif i=='U':
    x -= 1    
  elif i=='D':
    x += 1
    

print(x,y)

</div>
</details>

<br>

<details>
<summary>답</summary>
<div markdown="1">
<br>

```python
n = int(input())
x, y = 1, 1
plans = input().split()

# L, R, U, D 이동 방향 설정
move_type = ['L', 'R', 'U', 'D']
dx = [0,0,-1,1]
dy = [-1,1,0,0]

# plans 하나 씩 확인
for plan in plans:
  # 이동 후 좌표
  for i in range(len(move_type)):
    if plan == move_type[i]:
      nx = x + dx[i]
      ny = y + dy[i]
  # 공간 벗어나면 무시
  if nx < 1 or ny < 1 or nx > n or ny > n:
    continue
  # 이동
  x, y = nx,ny

print(x,y)
```

</div>
</details>

<br>