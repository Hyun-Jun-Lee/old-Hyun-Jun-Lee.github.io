---
title:  "[문자열] 1157번 단어 공부"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-09
last_modified_at: 2022-01-09
---

# [문자열] 1157번 단어 공부

> 문제

알파벳 대소문자로 된 단어가 주어지면, 이 단어에서 가장 많이 사용된 알파벳이 무엇인지 알아내는 프로그램을 작성하시오. 단, 대문자와 소문자를 구분하지 않는다.

> 입력

첫째 줄에 알파벳 대소문자로 이루어진 단어가 주어진다. 주어지는 단어의 길이는 1,000,000을 넘지 않는다.

> 출력

첫째 줄에 이 단어에서 가장 많이 사용된 알파벳을 대문자로 출력한다. 단, 가장 많이 사용된 알파벳이 여러 개 존재하는 경우에는 ?를 출력한다.

<br>

> 풀이

```python
words = input().upper()
unique_words = list(set(words))  # 입력받은 문자열에서 중복값을 제거

cnt_list = []
for x in unique_words :
    cnt = words.count(x)
    cnt_list.append(cnt)  # count 숫자를 리스트에 append

if cnt_list.count(max(cnt_list)) > 1 :  # count 숫자 최대값이 중복되면
    print('?')
else :
    max_index = cnt_list.index(max(cnt_list))  # count 숫자 최대값 인덱스(위치)
    print(unique_words[max_index])
```

입력 받는 문자를 `.upper()` 함수로 모두 대문자로 변환하고 words에 저장, 중복 제거한 값을 unique_words에 리스트 형태로 저장하여 알파벳이 몇번 사용되는지 확인하는 용도로 사용한다.

```python
cnt = words.count(x)
cnt_list.append(cnt)
```

입력 받은 문자열에 같은 알파벳이 몇 개 있는지 카운트해서 cnt_list에 추가

```python
if cnt_list.count(max(cnt_list)) > 1 : 
    print('?')
else :
    max_index = cnt_list.index(max(cnt_list))
    print(unique_words[max_index])
```

숫자 리스트에서 알파벳이 사용된 개수 중 가장 큰 수를 찾고서 해당 숫자가 1보다 크면 물음표를 출력

최댓값이 하나라면 숫자 리스트에서 가장 큰 수의 위치를 index 함수로 찾고서 unique_words 리스트에서 같은 인덱스에 위치한 문자열을 출력

