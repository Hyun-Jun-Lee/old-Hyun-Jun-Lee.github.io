---
title:  "[문자열] 1316번 그룹 단어 체커"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-12
last_modified_at: 2022-01-12
---

# [문자열] 1316번 그룹 단어 체커

> 문제

그룹 단어란 단어에 존재하는 모든 문자에 대해서, 각 문자가 연속해서 나타나는 경우만을 말한다. 예를 들면, ccazzzzbb는 c, a, z, b가 모두 연속해서 나타나고, kin도 k, i, n이 연속해서 나타나기 때문에 그룹 단어이지만, aabbbccb는 b가 떨어져서 나타나기 때문에 그룹 단어가 아니다.

단어 N개를 입력으로 받아 그룹 단어의 개수를 출력하는 프로그램을 작성하시오.

> 입력

첫째 줄에 단어의 개수 N이 들어온다. N은 100보다 작거나 같은 자연수이다. 둘째 줄부터 N개의 줄에 단어가 들어온다. 단어는 알파벳 소문자로만 되어있고 중복되지 않으며, 길이는 최대 100이다.

> 출력

첫째 줄에 그룹 단어의 개수를 출력한다.

> 예제 입력

3
happy
new
year

> 예제 출력

3

<br>

> 풀이

```python
n = int(input())
group_word = 0

for _ in range(n):
    word = input()
    not_group_word = 0
    for index in range(len(word)-1):
        if word[index] != word[index+1]:
            new_word = word[index+1:]
            if new_word.count(word[index])>0:
                not_group_word += 1
    if not_group_word == 0:
        group_word += 1

print(group_word)

```

그룹 단어는 서로 다른 알파벳으로 이어진 단어로 같은 단어는 연속해서만 나올 수 있다. 같은 알파벳이 떨어져 있는 단어는 그룹 단어가 아니다.

```python
    for index in range(len(word)-1):  # 인덱스 범위 생성 : 0부터 단어개수 -1까지 
        if word[index] != word[index+1]:  # 연달은 두 문자가 다른 때,
            new_word = word[index+1:]  # 현재글자 이후 문자열을 새로운 단어로 생성
            if new_word.count(word[index]) > 0:  # 남은 문자열에서 현재 글자가 있있다면
                not_group_word += 1  # not_group_word 1씩 증가.
```

index번째 단어와 index+1번째 단어를 비교해야 하는데, 단어의 끝자리는 i+1이므로 반복의 범위는 `range(len(word)-1)` 까지해서 단어의 index로 활용.

연속 된 두 알파벳을 비교해서 서로 다른 경우, index+1 번째 단어를 new_word로 저장하고 count함수로 입력받은 word에 동일한 알파벳이 있는지 확인한다. 만약 동일한 알파벳이 있어서 count 함수가 0보다 큰 수를 반환하면 그룹 단어가 아니므로 not_group_word에 1 증가 

```python
    if not_group_word == 0:
        group_word += 1
```

count에서 0을 반환하면 그룹단어 이므로 group_word에 1 증가
