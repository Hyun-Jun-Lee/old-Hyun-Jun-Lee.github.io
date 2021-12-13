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

1. One to Many
- image captioning : 이미지 데이터에서 설명글 출력
- language model

2. Many to One
- Sentiment Classification : 텍스트의 감정이 긍정/부정 인지 분류
- 시계열 예측 : 과거 정보 바탕으로 미래 결과 예측

3. Many to Many
- Machine Translation : 영어문장 한글로 번역
- Name Entity Recognition : 개체명 인식, 텍스트에서 언급된 사람, 회사 등의 개체를 인식하여 출력

<br>

## RNN(Recurrent Netural Networks)

![image](https://user-images.githubusercontent.com/76996686/145819650-2c8210b5-469e-4661-a3c9-f42dbb2340e1.png)

x(1)으로 부터 h(1)을 얻고, 다음 스텝에서 h(1)과 x(2)를 이용해 과거정보와 현재 정보 모두 반영
은닉층 노드 값을 t+1 시점으로 넘겨주고, 넘겨 받은 노드의 값과 t+1 시점의 입력값을 계산하는 작업을 반복적으로 진행하기 때문에 `Recurrent`