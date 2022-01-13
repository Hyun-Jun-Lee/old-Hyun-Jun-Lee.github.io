---
title:  "[수학] 1193번 분수 찾기"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-12
last_modified_at: 2022-01-12
---

# [수학] 1193번 분수 찾기

> 문제

![image](https://user-images.githubusercontent.com/76996686/149324032-34041a2d-094a-4ebb-bd39-88eada5c3e78.png)

> 입력

첫째 줄에 X(1 ≤ X ≤ 10,000,000)가 주어진다.

> 출력

첫째 줄에 분수를 출력한다.

> 예제 입력

2

> 예제 출력

1/2

<br>

> 풀이

```python
input_num = int(input())

line = 0 
end_index = 0 # 입력된 숫자가 있는 라인에서 마지막 인덱스

while input_num > end_index:
    line += 1  
    end_index += line  

# 입력 받은수의 인덱스
gap = end_index - input_num

if line %2 ==0: # 짝수번째 라인일 때
    top = line-gap
    under = gap+1
else: # 홀수번째 라인일 때
    top = gap+1
    under = line - gap

print(f'{top}/{under}')

```

![image](https://user-images.githubusercontent.com/76996686/149324203-b323f687-9920-46a9-9f69-e59f039c0d01.png)

위와 같은 방향으로 진행되고 이 문제의 규칙은

'짝수 라인'은 오른쪽 끝에서 왼쪽 아래 사선 방향으로 갈수록 `분자+1/분모-1`
'홀수 라인'은 왼쪽 끝에서 오른쪽 위 사선 방향으로 갈수록  `분자-1/분모+1`

구하고자 하는 수가 몇번 째 라인에 있는지를 찾고, 마지막 인덱스에 입력받은 수의 인덱스를 빼서 인덱스 위치를 찾으면 된다. 

> 이런 수학 문제는 이해가 안되면 직접 손으로 예시로 풀어보면서 규칙을 찾아보는게 이해에 도움이 된다.