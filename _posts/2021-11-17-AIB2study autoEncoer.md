---
title:  "[Section4] Auto Encoder"
excerpt: "AIB 컨텐츠 복습 챌린지"

categories:
- AIB2 Study

toc: True
toc_sticky: True

date: 2021-11-17
last_modified_at: 2021-11-17
---
# [Section4] Auto Encoder

<br>

## Auto Encoder

- 입력 데이터를 압축시켜 압축시킨 데이터로 축소한 후 다시 확장하여 결과 데이터를 입력 데이터와 동일하도록 만드는 일종의 딥 뉴럴 네트워크 모델

<br>

![image](https://user-images.githubusercontent.com/76996686/142186400-159915a2-56d5-4bc4-82a4-64e76481fc22.png)

<br>

- 입력 데이터인 784개의 뉴런들을 500개, 300개, 2개로 압축시킴으로써 입력 데이터의 대표적인 특성을 추출
- 이를 기반으로 다시 대칭적인 구조로 300개, 500개 뉴런으로 확장시킨 후 최종적으로 입력 데이터와 똑같은 사이즈인 784개의 뉴런 개수로 최종 값을 출력

<br>

## vs PCA

![image](https://user-images.githubusercontent.com/76996686/142186804-b2b8c61d-38ce-409e-b665-860814768355.png)

- PCA는 선형적으로 데이터 차원 감소 / Auto Encoder는 비선형적으로 데이터 차원 감소

- PCA는 Kernel PCA를 활용해 비선형적으로 데이터를 축소할 수 있긴 하지만 보통 선형적으로 데이터 차원을 축소하고 비선형적으로 데이터를 축소하기 위해서는 Auto Encoder를 사용

<br>

## AutoEncoder 구조

![image](https://user-images.githubusercontent.com/76996686/142187163-a6f29cc5-806a-4566-9a54-c7dbf05a754b.png)

- 입력데이터와 Encoder 부분, Decoder와 출력데이터 부분이 대칭적인 구조
- Encoded Layer
  - input layer의 입력 데이터를 압축시켜 가장 대표적인 특성을 추츨하는 층
  - 결과 데이터가 입력 데이터와 얼마나 동일하게 출력할 것인가를 좌지우지 하는 역할
  - 하이퍼파라미터로서 Encoded Layer의 노드 개수 설정이 매우 중요, 만약 출력 데이터가 입력 데이터와 동일하지 않게 출력된다면 Encoded Layer의 노드 개수가 적은 것이 원인일 가능성이 큼