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

<br>

## LSTM(Long Short-Term Memory)

- RNN의 Long-Term dependency문제를 해결한 모델
  - Long-Term dependency : 은닉층의 과거 정보가 마지막까지 전달되지 못하는 현상
  - ex) "i grew up in france and want to be a plumber who the best is in the world and i speak fluent french"에서 `french`를 예측하기 위해선 앞의 `france`가 핵심이지만, 너무 초반에 있어서 뒤산까지 전달되기 어려움

<br>

### LSTM의 구조

RNN은 이전 은닉층 값 h(t-1)과 현재 입력값 x(t)에 각각 가중치 곱하고 tanh 함수에 넣은 출력 값을 해당 순번, t의 은닉층 값 h(t)로 계산하는 과정 반복

- LSTM

![image](https://user-images.githubusercontent.com/76996686/145826965-dcea85e2-f454-4daf-9758-40350e074435.png)

![image](https://user-images.githubusercontent.com/76996686/145827112-f41e1acc-c376-42f4-91c2-2fe19416f150.png)

LSTM은 이전 단계의 정보를 memory cell에 저장하여 흘려보냄.<br>
과거의 내용을 얼마나 지울지 곱해주고, 그 결과에 현재의 정보를 더해서 다음 시점으로 전달

#### Forget Gate(망각 게이트)

![image](https://user-images.githubusercontent.com/76996686/145827870-5fdb7619-c718-4bac-9ff1-d6b77dfab15a.png)

현 시점의 정보 x(t)와 과거 은닉층의 값 h(t-1)에 각각 가중치를 곱하고 더한 후, sigmoid 함수 적용하여 해당 시점의 memory cell에 곱해줌<br>
sigmoid 함수는 (0,1) 사이 값을 출력하므로, 1에 가깝다면 과거정보를 많이 활용할 것이고 0에 가까우면 과거 정보를 많이 잃게 됨.

- 수식

![image](https://user-images.githubusercontent.com/76996686/145828275-a42039ab-cde4-4053-805f-9e2f22c45f8e.png)

<br>

#### Input Gate & Candidate

- Input Gate : 현 시점의 정보를 cell에 입력할 크기를 정해주는 역활
- Candidate : 현 시점의 정보를 계산하는 역활

![image](https://user-images.githubusercontent.com/76996686/145828575-73decfb4-5adf-4394-b7cc-333318a841bc.png)

<br>

#### Memory Cell 계산

앞서 계산한 Forget gate, Input gate, Candidate 이용하여 memory cell에 저장하는 단계

![image](https://user-images.githubusercontent.com/76996686/145829116-751ad812-a25c-4f10-a732-c3ce87fda822.png)

<br>

과거의 정보를 Forget gate에서 계산 된 만큼 지우고<br>
현 시점의 정보 candidate에 input gate의 중요도를 곱해준 것을 더하여 현 시점의 memory cell 계산

- 수식

![image](https://user-images.githubusercontent.com/76996686/145829168-26723115-e85b-4ddd-abcc-ee91ad5ceb92.png)

<br>

#### Output Gate

계산이 완료된 현 시점의 memory cell을 현 시점의 은닉층 값으로 출력할 양 결정

![image](https://user-images.githubusercontent.com/76996686/145829386-3bd00029-5625-4946-bb1e-9b1eeca2efc2.png)

- 수식

![image](https://user-images.githubusercontent.com/76996686/145829439-26faa6f4-1d56-4de5-b088-9450763e36a6.png)



> 참고 블로그 : https://yjjo.tistory.com/17?category=881892
