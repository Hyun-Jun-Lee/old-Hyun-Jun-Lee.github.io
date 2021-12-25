---
title:  "언어모델/N-gram"
excerpt: "Languagel Model, SLM, N-gram"

categories:
- AIB2 Study

toc: True
toc_sticky: True

date: 2021-12-25
last_modified_at: 2021-12-25
---

# 언어모델/N-gram

## 언어 모델

word sequence, sentence에 확률을 할당하는 모델

<br>

전통적 방식인 '통계를 이용한 방법'과 '인공신경망'을 이용한 방법(GPT, BERT)이 있음

### 이전 단어로 다음 단어 예측하기

단어 시퀀스에 확률을 할당하기 위해서 가장 보편적으로 사용하는 방법

<br>

- 단어 시퀀스의 확률
  - 하나의 단어를 w, 단어 시퀀스가 W라면 n개의 단어가 등장하는 단어 시퀀스 W의 확률
  - $$P(W)=P(w_1,w_2,w_3,w_4,...,w_n)$$

- 다음 단어의 등장 확률
  - $P(w_n|w_1,w_2,...,w_{n-1})$
  - n-1개의 단어가 나열된 상태에서 n번째 단어의 확률
  - ex) 5번째 단어의 확률 = $P(w_5|w_1,w_2,w_3,w_4)$
  - `|` 는 조건부 확률 -> $P(B|A) =\frac{P(AnB)}{P(A)}$

## N-gram

- 통계적 언어 모델(Statistical Language Model, SLM)

