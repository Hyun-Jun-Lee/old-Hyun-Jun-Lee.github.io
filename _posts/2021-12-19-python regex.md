---
title:  "Dictionary"
excerpt: "python"

categories:
- DB

toc: True
toc_sticky: True

date: 2021-12-17
last_modified_at: 2021-12-17
---

# Dictionary

## 특징

- {key:value} 형태, 각각의 쌍은 ','로 구분
- key는 중복 x, 이미 사용중인 key 사용하면 그 전 key는 무시
- value에 리스트 이용하여 여러 값 넣기 가능({'A':['a','b']})
- key에 리스트 형태 X, 튜플 형태는 가능

<br>

# 출력

- value 출력

```python
a = {'A':['b','c'], 'B':['a','e']}

# 슬라이싱
a['A']

# get
a.get('A')

# 모든 value
a.values()
```

- Key 출력

```python
a = {'A':['b','c'], 'B':['a','e']}

a.keys()
```

- Key, Value 출력

```python
a = {'A':['b','c'], 'B':['a','e']}

a.items()

for key,value in a.items():
  print(key,value)
```