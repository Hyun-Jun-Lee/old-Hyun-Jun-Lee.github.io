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

배열은 `같은 종류의 데이터를 순차적으로 저장`하는 자료구조. 

Python에서는 list로 구현됨

- 인덱스를 이용한 빠른 접근이 가능
- 데이터 추가시 공간이 많이 필요하며, 삭제 시 빈 공간이 생겨 관리의 어려움이 있다. 

```python
# 1차원 배열
L = [2,4,6,8]

# 2차원 배열
L2 = [[2,4,6], [1,3,5]]
```

- `.extend(list)` : list에 입력된 값을 배열 맨 끝에 붙임
- `.insert(index,obj)` : index 위치에 obj 삽입
- `del A[index]` : index 위치 원소 삭제하고 나머지를 좌측으로 땡김
- `.remove(obj)` : obj와 동일한 첫번째 원소 삭제

ex) 특정 문자 빈도수 측정
```python
def alphabet(dataset, alphabet):
  cnt = 0
  for d in dataset:
    for i in range(len(d)):
      if d[i] == alphabet:
        cnt += 1
```

- 장점
  - 빠른 접근 가능
- 단점
  - 추가/ 삭제의 어려움
  - 미리 최대 길이 지정해야함

## Queue

제일 먼저 들어간 데이터를 가장 먼저 꺼내는 데이터 구조(FIFO: Firset-in, First-Out)

프로세스 스케쥴링을 구현하는데 주로 사용됨.

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

`popleft()`, `appendleft(x)` 메서드는 모두 `O(1)`의 시간 복잡도를 가지기 때문에 list 보다 성능이 좋다. 그러나 내부적으로 linked list를 사용하고 있어서 N번째 데이터에 접근하려면 N번의 순회가 필요하다.

3. Queue

`deque`와 달리 방향성이 없이 깨둠에 데이터 추가와 삭제가 하나의 메서드로 처리된다.

- `Queue()` : 일반적인 Queue 자료구조
- `LifoQueue()` 나중에 입력된 데이터가 먼저 출력되는 구조(Stack)
- `PriorityQueue()` : 데이터 마다 우선순위를 부여해서, 우선순위가 높은 순으로 출력

```python

# Queue()
from queue import Queue
que = Queue()
# 데이터 추가
que.put(1)
# 데이터 삭제
que.get()

# PriorityQueue()
import queue

data_queue = queue.PriorityQueue()

data_queue.put((3, 1))
data_queue.put((2, "seunghye"))
data_queue.put((4, True))

# 우선순위에 따라 출력
print(data_queue.get()) # (2, 'seunghye')
print(data_queue.get()) # (3, 1)
print(data_queue.get()) # (4, True)
```

## Stack

마지막에 들어간 데이터가 먼저 나가는 데이터 구조(LIFO)

스택은 한 쪽에서만 데이터를 넣거나 뺄 수 있고 컴퓨터 내부의 프로세스 구조의 함수 동작 방식으로 활용됨

```python
class ListStack:
  def __init__(self):
    self.my_list = list()
  def push(self,data):
    self.my_list.append(data)
  def pop(self,data):
    return self.my_list.pop()
```

- 장점
  - 구조가 단순하고 구현 쉬움
  - 데이터 저장하고 불러오는 속도가 빠름
- 단점
  - 데이터 최대 갯수를 사전에 정의해야 함
  - 저장 공간 낭비 발생

- 시간 복잡도
  - 삽입, 삭제 `O(N)` (맨 위에 있는 데이터를 삽입, 삭제 하기 때문에 항상 O(1))
  - 검색 `O(N)` (특정 데이터를 찾을 때 까지 작업하므로 O(N))

## Linked List

링크드리스트는 배열과 달리 연결되지 않고 떨어진 곳에 존재하는 데이터를 경로로 지정하여 관리하는 자료구조, Python은 리스트 타입이 링크드리스트의 긴으을 모두 지원한다.

![image](https://user-images.githubusercontent.com/76996686/161221471-86b4918d-7dd2-4c82-9d5a-e36e4246ebbd.png)

- Node : 데이터 저장 단위로 데이터 값 + 포인터로 구성
- Pointer : 각 노드에서 다음이나 이전 노드의 주소를 가지는 값

- 장점
  - 미리 데이터 공간을 확보할 필요 없음
- 단점
  - 연결을 위한 별도의 데이터 공간 필요
  - 중간 데이터를 삭제하려면, 앞 뒤 노드 모두를 고려하는 코드 구성해야함


- 시간 복잡도
  - 삽입, 삭제 `O(N)`
  - 중간 삽입이 없으면 `O(1)`
  - 특정 원소를 찾을 때, 처음부터 원소에 도달 할 때까지 찾는 순차접근방식 `O(N)`

> 삽입 삭제가 많은 작업 -> Linked List / 데이터 접근이 많은 작업 -> Array

```python
class Node:
  def __init__(self, data):
    self.data = data
    self.next = None

class SingleLinkdedList:

  def __init__(self,data):
    new_node = Node(data)

    if not self.head:
      self.head = new_node
    else: # head가 이미 있다면 
      node = self.head
      # node의 next가 없을 때 까지 가서 new_node를 next에 지정
      while node.next:
        node = node.next
      node.next = new_node
  
  def delete(self, data):
    node = self.head

    if node.data == data:
      self.head = node.next
      del node
    else:
      while node.next:
        next_node = node.next
        if next_node.data == data:
          node.next = next_node.next
          del next_node
        else:
          node = node.next

  def find(self,data):
    node = self.head

    while node:
      if node.data == data:
        return node
      else:
        node = node.next
```

- Double Linked List

![image](https://user-images.githubusercontent.com/76996686/161228415-bc4dad24-11c9-4b89-a928-4b65f0a391c3.png)

이중 연결 리스트로 양방향 노드의 주소 값을 모두 가지고 있어서 양방향으로 탐색이 가능한 링크드 리스트

기존의 Single Linked List에서 `prev`라는 이전의 노드를 가리키는 변수를 추가하면 됨

```python
class Node:
  def __init__(self, data):
    self.data = data
    self.next = None
    self.prev = None

class DoubleLinkedList:
  def __init__(self,data):
    self.head = None
    self.tail = self.head
  
  def add(self, data):
    new_node = Node(data)

    if not self.head:
      self.head = new_node
      self.tail = self.head
    else:
      node = self.head
      while node.next:
        node = node.next
      new_node.prev = node
      node.next = new_node
      self.tail = new_node
```

`add`함수에 tail 변수를 고려해주는거 말고는 Single Linked List와 같은 코드