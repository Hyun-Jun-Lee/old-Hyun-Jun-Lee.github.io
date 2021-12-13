---
title:  "RNN & LSTM"
excerpt: "AIB2 Study"

categories:
- AIB2 Study

toc: True
toc_sticky: True

date: 2021-12-12
last_modified_at: 2021-12-12
---
# RNN & LSTM

<br>


## Sequence

- `순서`가 있는 data를 sequence라고 함
  - ex)text에는 문맥의 순서, 시계열 데이터에는 시간이라는 순서
- sequence data를 다루는 model은 대표적으로 `RNN,LSTM,GRU` 

기존에는 모든 input이 독립적이라고 가정하지만, 순서가 있는 정보에서는 과거 정보를 반영해야 함

<br>

### Sequence Model 종류

![image](https://user-images.githubusercontent.com/76996686/145823877-6b60422c-7a99-47c4-b41f-26b5b07da463.png)

- One to One : 은닉층이 1인 신경망 모형
- One to Many : image 속 대상에 이름 붙이는 모형
- Many to One : word sequence를 입력받아 감정 분류를 해주는 모형
- Many to Many : 번역 머신 모형, word sequence를 입력받아 workd sequence를 출력
- Many to Many : 비디오의 frame 입력 받아 frame 속 대상에 이름 붙이는 모형

<br>

## RNN(Recurrent Netural Networks)

![image](https://user-images.githubusercontent.com/76996686/145819650-2c8210b5-469e-4661-a3c9-f42dbb2340e1.png)

- 가중치
  - U : 입력층 -> 은닉층
  - W : t 시점의 은닉층 -> t+1 시점 은닉층
  - V : 은닉층 -> 출력층

x(1)으로 부터 h(1)을 얻고, 다음 스텝에서 h(1)과 x(2)를 이용해 과거정보와 현재 정보 모두 반영<br>
은닉층 노드 값을 t+1 시점으로 넘겨주고, 넘겨 받은 노드의 값과 t+1 시점의 입력값을 계산하는 작업을 반복적으로 진행하기 때문에 `Recurrent`

- ex) 다음 단어를 예측하는 RNN (hello-o, kin-g)

![image](https://user-images.githubusercontent.com/76996686/145820539-9c35f17f-f0a1-4a49-a926-c74cf8a5fc74.png)

RNN은 시간의 길이 T에 유연하기 때문에, 즉 같은 가중치를 곱해주고 은닉층에 단어의 과거 정보가 포함되기 때문에 단어의 길이와 무관하게 같은 모형을 적용할수 있다.

<br>

### RNN 동작 원리

![image](https://user-images.githubusercontent.com/76996686/145824453-c1b8c3ea-c365-468a-bf5a-ccade10dfb15.png)

1. 은닉층
  - x(t)와 h(t-1) 필요
  - `h(t) = T(W*h(t-1) + U*x(t))` 
  - T : hyperbolic tangent / bias는 제외

2. 출력층
  - `o(t) = softmax(V*h(t))`

