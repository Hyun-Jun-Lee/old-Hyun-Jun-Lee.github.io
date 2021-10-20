---
title:  "[구현] 게임 개발"
excerpt: "난이도 ★★"

categories:
- Algorithm

toc: false
toc_sticky: false

date: 2021-09-28
last_modified_at: 2021-09-28
---

# [구현] 게임 개발

- 문제

캐릭터가 있는 장소는 1 x 1크기의 정사각형으로 이루어진 N x N 크기의 직사각형으로 각각의 칸은 육지 또는 바다이다. 맵의 각 칸은 (A,B)로 나타낼 수 있고, A는 북쪽으로부터 떨어진 칸의 개수, B는 서쪽으로 부터 떨어진 칸의 개수.
캐릭터는 상하좌우 이동 가능하고 바다로는 갈 수 없다.

1. 현재 위치에서 현재 방향을 기준으로 왼쪽 방향부터 차례대로 갈곳을 정한다.
2. 캐릭터의 왼쪽에 아직 가지 않은 칸이 존재한다면, 왼쪽 방향으로 회전한 다음 한칸 전진한다. 왼쪽 방향에 가보지 않은 칸이 없다면 왼쪽 방향으로 회전만 하고 1단계로 돌아간다
3. 만약 네 방향 모두 이미 가본 칸이거나 바다로 되어 있는 경우에는, 바라보는 방향을 유지한 채로 한칸 뒤로가고 1단계로 돌아간다. 단, 이때 뒤쪽 방향이 바다인 칸이라 뒤로 갈 수 없는 경우에는 움직임을 멈춘다.

위의 메뉴얼에 따라 캐릭터를 이동 시킨 뒤에 캐릭터가 방문한 칸의 수를 출력하는 프로그램을 만드시오

<br>

- 입력 조건
  - 첫째 줄에 맵의 세로크기 N과 가로크기 M을 공백으로 구분하여 입력
  - 둘째 줄에 캐릭터가 있는 칸의 좌표 (A,B)와 바라보는 방향 d가 공백으로 구분하여 입력. d의 값은 다음 4가지가 잇다.
    - 0:북
    - 1:동
    - 2:남
    - 3:서
  - 셋째 줄부터 맵이 육지인지 바다인지에 대한 정보가 주어진다. N개의 줄에 맵의 상태가 북쪽부터 남쪽 순서대로, 각 줄의 데이터는 서족부터 동쪽 순서대로 주어진다. 맵의 외각은 항사 바다이다.
    - 0 : 육지
    - 1 : 바다

- 입력 예시

```
4 4 # 4x4 맵 생성
1 1 0 # (1,1)에서 북쪽(0)을 바라보고 캐릭터가 서 있음
1 1 1 1 # 첫 줄은 모두 바다
1 0 0 1 # 바다 / 육지 / 육지 / 바다
1 1 0 1 # 바다 / 바다 / 육지 / 바다
1 1 1 1 # 모두 바다
```

- 출력 예시


```
3
```
<br>

<hr>

<br>

<details>
<summary>답</summary>
<div markdown="1">
<br>

```python
n, m = map(int, input().split())

# # 현재 캐릭터의 위치 및 바라보는 방향
x, y, direction = map(int, input().split())
# 맵을 생성하여 모두 0으로 초기화
d = [[0] * m for _ in range(n)]
# 현재 좌표 방문 처리
d[x][y] = 1

# 바다, 육지 전체 맵 정보 입력
array = []
for i in range(n):
  array.append(list(map(int,input().split())))

# 서, 북, 동, 남 방향 정의(왼쪽 바라 볼땐 북동남서)
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

# 메뉴얼 따라 왼쪽으로 회전
def turn_left():
  global direction
  direction -= 1 # 반시계 방향 회전
  if direction == -1:
    direction = 3 # 3:바라보는 방향 서쪽

# 시뮬레이션 시작
count = 1
turn_time = 0
while True:
  # 왼쪽으로 회전
  turn_left()
  nx = x + dx[direction]
  ny = y + dy[direction]
  # 회전 한 후 가보지 않은 칸이 존재하는 경우 이동
  if d[nx][ny] == 0 and array[nx][ny] == 0:
    d[nx][ny] = 1
    x = nx
    y = ny
    count += 1
    turn_time = 0
    continue
  # 회전 한 후 가보지 않은 칸이 없거나 바다인 경우
  else : 
    turn_time += 1
  # 네 방향 모두 갈 수 없는 경우
  if turn_time == 4:
    nx = x - dx[direction]
    ny = y - dy[direction]
    # 뒤로 갈 칸이 있으면 이동
    if array[nx][ny] == 0:
      x = nx
      y = ny
    # 뒤로 갈 칸 없는 경우
    else:
      break
    turn_time = 0

print(count)
```

</div>
</details>

<br>