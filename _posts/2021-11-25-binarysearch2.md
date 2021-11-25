---
title:  "[이진탐색] 떡볶이 떡 만들기"
excerpt: "난이도 ★★"

categories:
- Algorithm

toc: false
toc_sticky: false

date: 2021-11-25
last_modified_at: 2021-11-25
---

# [이진탐색] 떡볶이 떡 만들기

- 문제


<br>

- 입력 조건
  - 첫쨰줄에 떡의 개수 N과 요청한 떡의 길이 M
  - 둘째줄엔 떡의 개별 높이가 주어진다. 떡 높이의 총합은 항상 M 이상이므로, 손님이 필요한 양만큼 떡을 사갈 수 있다.

- 입력 예시

```
4 6
19 15 10 17
```

- 출력 조건
  - 적어도 M만큼의 떡을 집에 가져가기 위해 절단기에 설정할 수 있는 높이의 최댓값을 출력한다.

- 출력 예시

```
15
```

<br>

<hr>

<br>

<details>
<summary>내 풀이</summary>
<div markdown="1">
<br>

```python
n,m = list(map(int,input().split()))
# 떡 높이 
H =list(map(int,input().split()))

start = 0
end = max(H)

res= 0

while start <= end:
  dduck = 0
  mid = (start + end) // 2
  # mid로 자르고 남은 떡 길이의 합 -> dduck
  for x in H:
    if x > mid:
      dduck += x-mid
  # 자르고 남은 떡 길이 합이 m보다 클 경우 시작점 땡기기
  if dduck > m:
    start = mid+1
  else:
    end = mid-1
    if dduck ==m:
      res = mid
    

print(res)
```

</div>
</details>

<br>