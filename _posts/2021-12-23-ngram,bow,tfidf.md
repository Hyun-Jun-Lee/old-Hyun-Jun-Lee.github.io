---
title:  "언어모델/N-gram/perplexity"
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

<br>

## 통계적 언어 모델(Statistical Language Model, SLM)

### 조건부 확률

- 두 확률 P(A),P(B)에 대한 관계
  - $P(B|A) = \frac{P(AnB)}{P(A)}$
  - $P(AnB) = P(A)P(B|A)$

- n개의 확률이 조건부 확률의 관계를 가질 때
  - $P(x_1,x_2,x_3,...,x_n) = P(x_1)P(x_2|x_1)P(x_3|x_1,x_2)...P(x_n|x_1...x_{n-1})$
  - 이것을 조건부 확률의 `연쇄 법칙(chain rule)` 이라고 함

<br>

### 조건부 확률의 연쇄법칙 이용해 문장의 확률 구하기

ex) '안녕하세요 저는 이현준 입니다'

$P(안녕하세요 저는 이현준 입니다) = P(안녕하세요) * P(저는|안녕하세요) * P(이현준|안녕하세요 저는) * P(입니다|안녕하세요 저는 이현준)$

문장의 확률은 각 단어들이 이전 단어가 주어졌을 때 다음 단어로 등장할 확률의 곱

<br>

### 카운트 기반 접근

문장의 확률을 구하기 위해 다음 단어에 대한 예측 확률을 모두 곱한다<br>
이전 단어로부터 다음 단어에 대한 확률은 카운트에 기반하여 계산한다.

ex) '안녕하세요 저는 이현준'이 나왔을 때, 다음에 '입니다'가 나올 확률<br>

$$P(입니다|안녕하세요 저는 이현준) = \frac{count(안녕하세요 저는 이현준 입니다)}{count(안녕하세요 저는 이현준)}$$

만약 학습한 corpus data에서 '안녕하세요 저는 이현준'이 100번 등장하고, '입니다'가 30번 등장햇다면 $P(입니다|안녕하세요 저는 이현준)$ 는 30%가 된다.

<br>

### 한계점

- 희소 문제(Sparsity Problem)

count 기반 접근을 하려면 방대한 양의 corpus data가 필요하다(위의 예에서 '안녕하세요 저는 이현준'이 corpus data에 없다면 확률은 0이 되어 버림)

<br>

## N-gram

카운트에 기반한 통계적 접근을 사용하고 있는 SLM의 일종으로, 모든 단어를 고려하는 것이 아니라 일부 단어만 고려하여 예측<br>

SLM은 corpus data에 확률을 계산하려는 문장이 없을 수 있는 것이 한계점인데 이것을 극복하기 위해 참고하는 단어 카운트를 줄인다.

예를 들어, '안녕하세요 저는 이현준'가 나왔을 때 '입니다'가 나올 확률을 계산 할 때, corpus data에 '안녕하세요 저는 이현준'이 있을 확률보다 '이현준 입니다' 라는 더 짧은 단어 시퀀스가 존재할 가능성이 더 높다. 

<br>

- 'An adorable little boy is spreading smiles'이라는 문장의 n-gram
  - unigrams(n=1) : an, adorable, little, boy, is, spreading, smiles
  - bigrams(n=2) : an adorable, adorable little, little boy, boy is, is spreading, spreading smiles
  - trigrams(n=3) : an adorable little, adorable little boy, little boy is, boy is spreading, is spreading smiles
  - 4-grams(n=4) : an adorable little boy, adorable little boy is, little boy is spreading, boy is spreading smiles

N-gram에서 다음 단어의 예측은 n-1개의 단어에만 의존(n=4라면, 앞의 3개의 단어만 고려)

<br>

### 한계점

- 희소 문제(Sparsity Problem)
  - 일부 단어만을 보는 것으로 현실적으로 코퍼스에서 카운트 할 수 있는 확률을 높일 수는 있었지만, n-gram 언어 모델도 여전히 n-gram에 대한 희소 문제가 존재
- n을 선택하는 것은 trade-off 문제
  - n을 크게 설정
    - corpus data에 해당 n-gram을 카운트할 수 있는 확률이 적어져서 희소 문제가 커지고 모델 사이즈가 커짐
  - n을 작게 설정
    - corpus data에서 카운트는 잘되지만 정확도 떨어짐(권장 n은 5 이하)