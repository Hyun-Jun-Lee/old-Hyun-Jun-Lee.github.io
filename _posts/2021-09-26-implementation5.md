---
title:  "[구현] 문자열 재정렬"
excerpt: "난이도 ★"

categories:
- Algorithm

toc: false
toc_sticky: false

date: 2021-09-28
last_modified_at: 2021-09-28
---

# [구현] 문자열 재정렬

- 문제

알파벳 대문자와 숫자 0~9로만 구성된 문자열이 입력으로 주어진다. 이때 모든 알파벳을 오름 차순으로 정렬하여 이어서 출력한 뒤에, 그 뒤에 모든 숫자를 더한 값을 이어서 출력하시오
ex) K1KA5CB7이 들어오면 ABCKK13출력

<br>

- 입력 조건
  - 첫째 줄에 문자열 s가 주어짐


- 입력 예시
```
K1KA5CB7
```

- 출력 예시
```
 ABCKK13
```
<br>

<hr>

<br>

<details>
<summary>답</summary>
<div markdown="1">
<br>

```python
data = input()
result = []
value = 0

# 입력 받은 문자열에서 문자 하나씩 확인
for x in data:
  # 알파벳인 경우 리시트에 추가
  if x.isalpha():
    result.append(x)
  # 숫자 정수형으로 바꿔준 후 따로 더하기
  else:
    value += int(x)
breakpoint()
# 알파벳 정렬(default 오름차순)
result.sort()

# 숫자가 하나라도 존재하면 문자열로 바꾼 후 가장 뒤에 삽입
if value != 0:
  result.append(str(value))

# 리스트를 문자열로 변환하여 출력
print(''.join(result))
```

</div>
</details>

<br>