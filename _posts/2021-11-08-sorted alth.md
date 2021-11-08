---
title:  "[정렬] 정렬 알고리즘"
excerpt: "난이도 ★"

categories:
- Algorithm

toc: false
toc_sticky: false

date: 2021-11-08
last_modified_at: 2021-11-08
---

# [정렬] 정렬 알고리즘

<br>

## 선택 정렬

```python
array = [7,5,9,0,3,1,6,2,4,8]

for i in range(len(array)):
  min_index = i
  for j in range(i+1, len(array)):
    if array[min_index] > array[j]: # j번째 값이 i번째 값보다 작으면 min_indx=j
      min_index = j
  # Swap
  array[i], array[min_index] = array[min_index], array[i]
```

<br>

## 삽입 정렬

```python
array = [7,5,9,0,3,1,6,2,4,8]

for i in range(1, len(array)):
  for j in range(i,0,-1): # i부터 1까지 감소
    if array[j] < array[j-1]: # 왼쪽에 있는 숫자보다 j가 작다면
      # 한칸 씩 왼쪽으로 이동
      array[j], array[j-1] = array[j-1], array[j]
    else: # j보다 작은 수 만나면 break
      break
```

<br>

## 퀵 정렬

```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    lesser_arr, equal_arr, greater_arr = [], [], []
    for num in arr:
        if num < pivot:
            lesser_arr.append(num)
        elif num > pivot:
            greater_arr.append(num)
        else:
            equal_arr.append(num)
    return quick_sort(lesser_arr) + equal_arr + quick_sort(greater_arr)
```

<br>

## 버블 정렬

```python
def bubble_sort(arr):
    for i in range(len(arr) - 1, 0, -1):
        for j in range(i):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
```