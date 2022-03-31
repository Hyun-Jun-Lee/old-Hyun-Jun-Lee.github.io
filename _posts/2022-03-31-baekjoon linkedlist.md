---
title:  "[Linkedlist] AddTwoNumber"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-03-31
last_modified_at: 2022-03-31
---

# [Linkedlist] AddTwoNumber

> 문제

음이 아닌 두 개의 정수를 나타내는 두 개의 비어 있지 않은 linked lists가 제공됩니다. 자릿수는 역순으로 저장되며 각 노드에는 한 자리가 포함됩니다. 두 숫자를 더하고 합계를 링크 리스트로 반환하세요.

입력 예시

```
l1 = [2,4,3]
l2 = [5,6,4] 
```

출력 예시

```
[7,0,8] 
```

> 풀이 코드

```python

class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        l1_val = 0
        l2_val = 0

        place_num = 1
        while l1:
            l1_val += l1.val * place_num
            l1 = l1.next
            place_num *= 10

        place_num = 1
        while l2:
            l2_val += l2.val * place_num
            l2 = l2.next
            place_num *= 10

        sum_val = l1_val + l2_val

        head=None
        tail=None
        for val in str(sum_val):
            if not head:
                head=ListNode(int(val))
                tail=head
            else:
                curNode=ListNode(int(val), tail)
                tail=curNode
        
        return tail
```

- 두 링크드리스트를 더한 하나의 링크리스트를 반환하면 된다.

```python
place_num = 1
while l1:
    l1_val += l1.val * place_num
    l1 = l1.next
    place_num *= 10
```

`place_num` 은 일의자리, 십의 자리 등을 나타내는 수로 while문이 l1을 한번 씩 돌때마다 10씩 곱해줘서 자리수를 체크한다. 이 과정에서 역순으로 정렬된다.


```python
head=None
tail=None
for val in str(sum_val):
    if not head:
        head=ListNode(int(val))
        tail=head
    else:
        curNode=ListNode(int(val), tail)
        tail=curNode
```

l1 값과 l2 값을 합한 sum_val을 돌며 head가 비어 있다면 현재 val 값을 head에 넣어준다. head가 지정 되있다면, 현재 val값과 tail을 연결시켜준다.
그리고 else문으로 링크드리스트를 연결해준다.

입력 예시로 보면, sum_val은 '243 + 564 = 807'이다. 처음에 head 값이 None이기 때문에 str 타입으로 변환된 '8'이 head이자 tail이 된다. 다음으로 '0'은 `ListNode(int(0), 8)` 로 '0->8' 과 같은 형태로 tail에 저장된다. 마지막으로 '7'은 `ListNode(int(7), (0,8))`로 '7->0->8' 과 같이 된다.
