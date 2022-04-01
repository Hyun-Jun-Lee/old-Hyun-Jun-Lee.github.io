---
title:  "Hash Table"
excerpt: "Data Strature with Python"

categories:
- Data Strature

toc: True
toc_sticky: True

date: 2022-04-01
last_modified_at: 2022-04-01
---

![image](https://user-images.githubusercontent.com/76996686/161204797-f017cf61-ecfe-4015-9ddb-b107dbc2355f.png)

# Hash Table

## Hash Table

해쉬는 Key-Value 쌍으로 이루어진 자료 구조, Python에서는 dictionary 타입이 해쉬 테이블과 같은 구조이다.

검색이 많이 필요한 경우 저장, 삭제, 읽기가 많은 경우, 캐쉬를 구현할 때 주로 사용된다.

![image](https://user-images.githubusercontent.com/76996686/161253510-4743a4b4-3e2c-4415-a00d-1195d1ad1455.png)

- 해쉬(Hash) : 임의 값을 고정 길이로 변환하는 것
- 해싱 함수(Hashing Function) : Key에 대해 산술 연산을 이용해 데이터 위치를 찾을 수 있는 함수
- 해쉬 값(Hash Value)/해쉬 주소(Hash Address) : Key를 해싱 함수로 연산해서 해쉬 값을 알아내고, 이를 기반으로 해쉬 테이블에서 해당 Key에 대한 데이터 위치를 일관성 있게 찾을 수 있음
- 슬롯(Slot) : 한 개의 데이터를 저장할 수 있는 공간

- 장점
  - 데이터 저장/검색 속도가 빠르다(Key를 이용해 검색)
- 단점
  - 저장 공간이 많이 필요함
  - 여러 키에 해당하는 주소가 동일할 경우 충돌을 해결하기 위한 별도의 방법 필요

- 시간복잡도
  - 일반적인 경우 `O(1)`
  - 충돌이 발생하는 경우 `O(N)`


> Key값이 중복되면 가장 뒤쪽의 Key-Value 쌍만 인정하고 기존의 쌍은 무시된다.
> Key값에는 리스트를 쓸수 없다, 변하지 않는 값만 가능

```python
class HashTable:
  def __init__(self):
    self.hash_talbe = list([0 for _ in range(10)])

  # 간단한 해쉬 함수, Division 방식(나머지 값을 사용하는 기법)
  def hash_func(self,key):
    return key % 4

  def insert(self, key, value):
    hash_value = self.hash_func(hash(key))
    self.hash_table[hash_value] = value
  
  def read(self, key):
    hash_value = self.hash_func(hash(key))
```

```python
ht = HashTable() 
ht.insert(1, 'a') 
ht.print() # [0, 'a', 0, 0, 0, 0, 0 ,0, 0, 0]
ht.insert('name', 'kang') 
ht.print() # [0, 'a', 'kang', 0, 0, 0, 0 ,0, 0, 0]
ht.insert(2, 'b') 
ht.print() # [0, 'a', 'b', 0, 0, 0, 0 ,0, 0, 0]
ht.insert(3, 'c') 
ht.print() # [0, 'a', 'b', 'c', 0, 0, 0 ,0, 0, 0]
ht.insert(4, 'd') 
ht.print() # [0, 'a', 'b', 'c', 'd', 0, 0 ,0, 0, 0]
```

충돌한 {'name':'kang'} 가 삭제됨

### 해쉬 테이블 충돌 해결 알고리즘

1. Chaining

해쉬테이블 저장 공간 외에 공간을 더 추가해서 아용하는 방법. 해시테이블에 이미 같은 키값의 데이터가 있다면, 노드를 추가하여 다음 노드를 가르키는 방식으로 구현

```python
class HashTable:
  def __init__(self):
    self.hash_talbe = list([0 for _ in range(10)])

  def hash_func(self,key):
    return key % 4

  def insert(self, key, value):
    index_key = hash(key)
    hash_value = self.hash_func(index_key)

    # 해당 인덱스를 이미 사용하고 있는 경우(충돌)
    if self.hash_table[hash_value] != 0:
      for i in range(len(self.hash_table[hash_value])):
        # 이미 같은 key 값이 존재하는 경우에는 value 교체 (0은 key, 1은 value 값이 존재하는 인덱스)
        if self.hash_table[hash_value][i][0] == index_key:
          self.hash_table[hash_value][i][1] = value
          return
      # 같은 키 값이 존재하지 않는 경우에는 [key, value]를 해당 인덱스에 삽입
      self.hash_table[hash_value].append([index_key, value])
    else:
      # 해당 인덱스를 사용하지 않고 있는 경우
      self.hash_table[hash_value] = [[index_key, value]]
  
  def read(self, key):
    index_key = hash(key)
    hash_value = self.hash_func(index_key)

    # 해당 인덱스를 이미 사용하고 있는 경우(충돌)
    if self.hash_table[hash_value] != 0:
      for i in range(len(self.hash_table[hash_value])):
        # 이미 같은 key 값이 존재하는 경우에는 해당 value retrun
        if self.hash_table[hash_value][i][0] == index_key:
          return self.hash)table[hash_value][i][1]
        # 동일한 key 가 없으면 None
        return None
    else:
      return None

  def print(self):
    print(self.hash_table)
```

```python
ht = HashTable() 
ht.insert(1, 'a') 
ht.print() # [0, [[1,'a']], 0, 0, 0, 0, 0 ,0, 0, 0]
ht.insert('name', 'kang') 
ht.print() # [0, [[1,'a'], [6319957083323, 'kang']], 0, 0, 0, 0, 0 ,0, 0, 0]
ht.insert(2, 'b') 
ht.print() # [0, [[1,'a'], [6319957083323, 'kang']], [[2,'b']], 0, 0, 0, 0 ,0, 0, 0]
ht.insert(3, 'c') 
ht.print() # [0, [[1,'a'], [6319957083323, 'kang']], [[2,'b']], [[3,'c']], 0, 0, 0 ,0, 0, 0]
ht.insert(4, 'd') 
ht.print() # [0, [[1,'a'], [6319957083323, 'kang']], [[2,'b']], [[3,'c']], [[4,'d']], 0, 0 ,0, 0, 0]
```

[key, value] 형태로 들어가고, 기존의 인덱스가 이미 사용중이라면 해당 인덱스의 리스트에 추가한다. 위에서는 [1, 'a']와 ['name', 'kang']이 같은 hash value를 가지는 것이고 해당 인덱스의 리스트에 함께 포함되어있는 것을 확인 할 수 있다.

changing 방식은 끝 없이 key,value 를 넣을 수 있지만, 공간 효율성이 떨어진다.

2. Linear Probing

충돌이 일어나면, 해당 hash value(hash address)의 다음 index부터 맨 처음 나오는 빈공간에 저장하는 기법(저장 공간 활용도의 증가)

```python
class HashTable:
  def __init__(self):
    self.hash_talbe = list([0 for _ in range(10)])

  def hash_func(self,key):
    return key % 4

  def insert(self, key, value):
    index_key = hash(key)
    hash_value = self.hash_func(index_key)

    # 해당 인덱스를 이미 사용하고 있는 경우(충돌)
    if self.hash_table[hash_value] != 0:
      # 해당 hash_value의 인덱스부터 마지막 인덱스 까지 돌면서 비어 있거나 key가 같은 값을 찾는다.
      for i in range(hash_value, len(self.hash_table)):
        # 해당 인덱스가 비어 있으면 index,value를 넣어줌
        if self.hash_table[i] == 0:
          self.hash_table[i] = [index_key, value]
          return
        # 이미 같은 key 값이 있으면 덮어쓰기
        elif self.hash_table[i][0] == index_key:
          self.hash_table[i][1] = value
          return
    else:
      # 해당 인덱스를 사용하지 않고 있는 경우
      self.hash_table[hash_value] = [[index_key, value]]
  
  def read(self, key):
    index_key = hash(key)
    hash_value = self.hash_func(index_key)

    # 해당 인덱스를 이미 사용하고 있는 경우(충돌)
    if self.hash_table[hash_value] != 0:
      # 해당 hash_value의 인덱스부터 마지막 인덱스 까지 돌면서 비어 있거나 key가 같은 값을 찾는다.
      for i in range(hash_value, len(self.hash_table)):
        # 해당 인덱스가 비어 있으면 None
        if self.hash_table[i] == 0:
          return None
        # key 값이 있으면 return
        elif self.hash_table[i][0] == index_key:
          return self.hash_table[i][1]
    else:
      None

  def print(self):
    print(self.hash_table)
```

```python
ht = HashTable() 
ht.insert(1, 'a') 
ht.print() # [0, [[1,'a']], 0, 0, 0, 0, 0 ,0, 0, 0]
ht.insert('name', 'kang') 
ht.print() # [0, [1,'a'], [6319957083323, 'kang'], 0, 0, 0, 0, 0 ,0, 0, 0]
ht.insert(2, 'b') 
ht.print() # [0, [1,'a'], [6319957083323, 'kang'], [2,'b'], 0, 0, 0, 0 ,0, 0, 0]
ht.insert(3, 'c') 
ht.print() # [0, [1,'a'], [6319957083323, 'kang'], [2,'b'], [3,'c'], 0, 0, 0 ,0, 0, 0]
ht.insert(4, 'd') 
ht.print() # [0, [1,'a'], [6319957083323, 'kang'], [2,'b'], [3,'c'], [4,'d'], 0, 0 ,0, 0, 0]
```

빈 공간을 찾아서 넣어주기 때문에 충돌이 일어나지 않지만, 미리 지정한 자릿수를 넘어가면 충돌이 일어나는 단점이 있다.

출처: https://davinci-ai.tistory.com/19?category=905792