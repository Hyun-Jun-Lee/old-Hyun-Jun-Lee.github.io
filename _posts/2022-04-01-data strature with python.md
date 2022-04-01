---
title:  "Array, Queue, Stack, Linked List"
excerpt: "Data Strature with Python"

categories:
- Data Strature

toc: True
toc_sticky: True

date: 2022-04-01
last_modified_at: 2022-04-01
---

![image](https://user-images.githubusercontent.com/76996686/161204797-f017cf61-ecfe-4015-9ddb-b107dbc2355f.png)

# Array, Queue, Stack, Linked List

## Array

배열은 같은 종류의 데이터를 순차적으로 저장하는 자료구조. 

Python에서는 list로 구현됨

- 인덱스를 이용한 빠른 접근이 가능
- 데이터 추가시 공간이 많이 필요하며, 삭제 시 빈 공간이 생겨 관리의 어려움이 있다. 

```python
# 1차원 배열
L = [2,4,6,8]

# 2차원 배열
L2 = [[2,4,6], [1,3,5]]
```

ex) 특정 문자 빈도수 측정
```python
def alphabet(dataset, alphabet):
  cnt = 0
  for d in dataset:
    for i in range(len(d)):
      if d[i] == alphabet:
        cnt += 1
```

## Queue

제일 먼저 들어간 데이터를 가장 먼저 꺼내는 데이터 구조(FIFO: Firset-in, First-Out)

- enqueue : list의 append()와 같이 큐에 데이터를 넣는 기능
- dequeue : list의 pop(0)와 같이 데이터를 큐에서 꺼내는 기능

1. List로 구현

```python
queue = [1,2,3]
queue.append(4)
queue.pop(0)

## [2,3,4]
```

list 자료구조는 무작위 접근에 최적화된 자료구조이고 pop(0)의 시간 복잡도는 `O(N)`이기 때문에 N이 커질수록 매우 느려짐

2. deque

double-ended queue의 약자로 데이터를 양방향에서 추가하고 제거할 수 있는 자료구조이다. 

```python
from collections import deque

queue = deque([1,2,3])
queue.append(4)
queue.popleft()

## [2,3,4]
```

`deque`는 `popleft()`가 pop(0)과 같은 기능을 하고 `appendleft(x)`를 통해 데이터를 맨 앞에 삽입할 수 있다.

