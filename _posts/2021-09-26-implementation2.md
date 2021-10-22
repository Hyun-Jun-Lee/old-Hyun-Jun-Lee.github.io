---
title:  "[구현] 시각"
excerpt: "난이도 ★"

categories:
- Algorithm

toc: false
toc_sticky: false

date: 2021-09-27
last_modified_at: 2021-09-27
---

# [구현] 시각

- 문제

정수 N이 입력되면 00시 00분 00초부터 N시 59분 59초까지의 모든 시각 중에서 3이 하나라도 포함되는 모든 경우의 수를 구하는 프로그램을 작성하시오 

<br>

- 입력 조건
  - 첫째 줄에 정수 N

- 입력 예시
```
5
```

- 출력 예시
```
11475
```
<br>

<hr>

<br>

<details>
<summary>내 풀이</summary>
<div markdown="1">
<br>

```python
n= int(input())

cnt = 0

for i in range(n+1):
  for j in range(60):
    for k in range(60):
      res =  str(i) + str(j) + str(k)
      if '3' in res:
        cnt +=1

print(cnt)
```

</div>
</details>

<br>

<details>
<summary>답</summary>
<div markdown="1">
<br>

```python
n = int(input())

count = 0
for i in range(n+1): # 시
  for j in range(60): # 분
    for k in range(60): # 초
      # 3이 포함되면 count 증가
      if '3' in str(i) + str(j) + str(k):
        count += 1

print(count)
```

</div>
</details>

<br>