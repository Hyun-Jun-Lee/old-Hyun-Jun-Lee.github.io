---
title:  "Python 정규표현식 Grouping"
excerpt: "Grouping"

categories:
- Python

toc: True
toc_sticky: True

date: 2021-12-20
last_modified_at: 2021-12-20
---

# 정규표현식

## Grouping

- 그룹을 만들어주는 메타문자 `()`

```python
p = re.compile('(ABC)+')
m = p.search('ABCABCABC OK?')

print(m)
>>> <re.Match object; span=(0, 9), match='ABCABCABC'>

print(m.group())
>>> ABCABCABC
```

- 매치된 문자열 중 특정 부분의 문자열만 뽑아내기

```python
# \w+\s+\d+[-]\d+[-]\d+ : 이름 + " " + 전화번호 형태의 문자열을 찾는 정규식
p = re.compile(r"(\w+)\s+\d+[-]\d+[-]\d+")
m = p.search("park 010-1234-1234")

# group(0) : 매치된 전체 문자열
# group(n) : n 번째 그룹에 해당되는 문자열

# 이름만
print(m.group(1))
>>> park

# 전화번호
print(m.group(2))
>>> 010-1234-1234
```

- grouping 중복으로 국번만 뽑아내기

```python
p = re.compile(r"(\w+)\s+((\d+)[-]\d+[-]\d+)")
m = p.search("park 010-1234-1234")

print(m.group(3))
>>> 010
```