---
title:  "Python 정규표현식 Grouping, 전방탐색"
excerpt: "Grouping, 전방탐색"

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

<br>

- 그루핑된 문자열에 이름 붙이기

```python
(?P<name>\w+)\s+((\d+)[-]\d+[-]\d+)
```

앞서 사용한 이름과 전화번호를 추출하는 정규식과 같지만 `(?P<name>\w+)`, 즉 `(\w)`라는 그룹에 name을 붙임

```python
p = re.compile(r"(?P<name>\w+)\s+((\d+)[-]\d+[-]\d+)")
m = p.search("park 010-1234-1234")

# 'name' 이라는 그룹이름으로 참조
print(m.group("name"))
>>>park
```

<br>

## 전방탐색 

```python
p = re.compile(".+:")
m = p.search("http://google.com")

# 정규식 .+:과 일치하는 문자열로 http: 반환
print(m.group())
>>> http:
```

> :제외하고 http만 출력하려면?

- 긍정형 전방 탐색(`(?=...)`) : ... 에 해당되는 정규식과 매치되어야 하며 조건이 통과되어도 문자열이 소비되지 않는다.

```python
p = re.compile(".+(?=:)")
m = p.search("http://google.com")

print(m.group())
>>> http
```

정규식 중 `:`에 해당하는 부분에 긍정형 전방 탐색 기법을 적용하여 `(?=:)`으로 변경하였다. 이렇게 되면 기존 정규식과 검색에서는 동일한 효과를 발휘하지만 : 에 해당하는 문자열이 정규식 엔진에 의해 소비되지 않아(검색에는 포함되지만 검색 결과에는 제외됨) 검색 결과에서는 :이 제거된 후 돌려주는 효과가 있다.

<br>

```python
.*[.].*$
```

이 정규식은 `파일이름 + . + 확장자` 를 나타냄( foo.bar, autoexec.bat, sendmail.cf 같은 형식의 파일과 매치)

- 확장자가 bat인 파일은 제외하기

```python
.*[.]([^b]..|.[^a].|..[^t])$
```

이 정규식은 `|` 메타 문자를 사용하여 확장자의 첫 번째 문자가 b가 아니거나 두 번째 문자가 a가 아니거나 세 번째 문자가 t가 아닌 경우를 의미. 'foo.bar'은 제외하지 않지만, 'sendmail.cf'처럼 확장자의 문자 개수가 2개인 케이스를 포함하지 못하는 오동작

```python
.*[.]([^b].?.?|.[^a]?.?|..?[^t]?)$
```

확장자의 문자 개수가 2개여도 통과되는 정규식

<br>

- 부정형 전방 탐색(`(?!...)`) : ...에 해당되는 정규식과 매치되지 않아야 하며 조건이 통과되어도 문자열이 소비되지 않는다.

```python
.*[.](?!bat$).*$
```

확장자가 bat가 아닌 경우에만 통과