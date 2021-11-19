---
title:  "[Section4] GAN"
excerpt: "AIB 컨텐츠 복습 챌린지"

categories:
- AIB2 Study

toc: True
toc_sticky: True

date: 2021-11-19
last_modified_at: 2021-11-19
---
# [Section4] GAN

<br>

```
1. GAN의 개념과 원리를 설명할 수 있다.
2. GAN에서 생성자와 판별자의 공통된 모듈이 어디에 있는 지 파악할 수 있다.
3. 이 외의 다른 종류의 GAN 하나씩 포스팅
4. GAN의 한계는?
```

## GAN

- 비지도 학습 모델
- 생성자와 식별자가 서로 경쟁(Adversarial)하며 데이터를 생성(Generative)하는 모델(Network)
- ex) GAN으로 인물 사진을 생성해 낸다면, 인물 사진을 만들어내는 것을 Generator(생성자)/만들어진 인물 사진을 평가하는 것을 Discriminator(구분자)라고 함. 생성자와 구분자가 서로 대립하며(Adversarial:대립하는) 서로의 성능을 점차 개선해 나가는 쪽으로 학습이 진행되는 것이 주요 개념

<br>

![image](https://user-images.githubusercontent.com/76996686/142619677-a8edac56-c552-4b22-ad30-d4503a136d6a.png)

<br>

## GAN 구조

![image](https://user-images.githubusercontent.com/76996686/142620400-37be36c5-f742-4f5d-9342-3ee89c92f598.png)

- Generator : 생성된 z를 받아 실제 데이터와 비슷한 데이터를 만들어내도록 학습
- Discriminator : 실제 데이터와 Generator가 생성한 가짜 데이터를 구별하도록 학습

Generator는 입력 데이터의 분포(distribution)를 알아내도록 학습. 이 분포를 재현하여 원 데이터의 분포와 차이가 없도록 하고 Discriminator는 실데이터인지 가짜 데이터인지 구별해서 각각에 대한 확률을 추정한다.

<br>

`실제 데이터의 분포에 가까운 데이터를 생성`하는 것이 GAN이 가진 궁극적인 목표
생성자(Generator)는 구분자(Discriminator)가 거짓으로 판별하지 못하도록 가짜 데이터를 진짜 데이터와 가깝게 생성하도록 노력하고, 이 과정을 통해 생성자(Generator)와 구분자(Discriminator)의 성능이 점차 개선되고 궁극적으로는 `구분자(Discriminator)가 실제 데이터와 가짜 데이터를 구분하지 못하게 만드는 것`

<br>

## GAN 학습

![image](https://user-images.githubusercontent.com/76996686/142622661-d3c29504-49a3-4ebe-b9aa-4bcbcad5d0af.png)

처음 학습이 진행되기 이전에 Real데이터의 확률분포, Generator의 확률분포, Discriminator의 확률분포의 그림이 (a)입니다. Discriminator는 Generator와 기존 확률 분포가 얼마나 다른지 판단합니다. 그리고 Generator는 Real 확률분포에 맞춰 Discriminator를 속이기 위한 쪽으로 생성모델을 수정해 나가고 궁극적으로 Generator의 확률분포가 Real데이터의 확률분포와 차이를 줄여나가는 과정을 가지게 됩니다.(D(x)=0.5 파란선)

<br>

### JSD, KLD

- 확률 분포간 차이 계산하기 위해 `JSD` 사용(JSD는 두개의 KLD로 구성)

- KLD(Kullback Leibler Divergence)
  - 같은 확률변수 x에 대한 2개의 확률 분포 P(x)와 Q(x)가 있을 때, 이 두 분포사이의 차이를 의미<br>
  ![image](https://user-images.githubusercontent.com/76996686/142623433-1700c943-7912-45c5-a7ee-47f9bbdf943d.png)

<br>

- JSD
  - KLD의 문제는 asymmetric하다는 것. 'KL(P|Q)KL(P|Q)'와 'KL(Q|P)KL(Q|P)'의 값이 서로 다르기 때문에 이를 “거리”라는 척도로 사용하기에는 애매한 부분이 존재하며 JSD는 이러한 문제를 해결할 수 있는 방법.<br>
  ![image](https://user-images.githubusercontent.com/76996686/142623578-872efcbb-8d06-4022-80a6-88548bc13e1e.png)
  - P : 실제 확률 분포
  - Q : Generator 확률 분포
  - M : 실제 확률 분포와 Q의 평균
  - P와 M과 / Q와 M을 각각 KLD하여 두 분포의 차이에서 평균 값을 구해 두 확률 분포 간의 차이를 구함.

<br>

이러한 발산 과정을 통해, 실제 데이터의 확률분포가 Generator가 생성한 확률분포인 Q 와의 JSD가 0이 되면 두 분포간 차이가 없다는 것으로 학습이 완료되며 GAN의 궁극적인 목표에 도달하게 된다.

<br>

## DCGAN(Deep Convolutional GAN)

![image](https://user-images.githubusercontent.com/76996686/142624801-282c1538-10be-40be-8c94-1be456fa1d50.png)

<br>

CNN구조로 판별자 D와 생성자 G를 구성한 GAN. <br>
판별자 D는 이미지(예 28x28x3)를 입력으로 받아 binary classification을 수행하므로 CNN구조를, 생성자 G는 random vector z(예 (100,1))를 입력으로 받아 이미지(28x28x3)을 생성해야므로 deconvolutional network구조를 갖게 된다.

<a href="https://blog.naver.com/laonple/221201915691">블로그 참고</a>

<br>

### DCGAN 특징

- Max-plloing layer 없애고 strided convolution/fractional-strided convol 사용해 featrue map 크기 조절
- Batch normalization 적용
- FC hidden layer 제거
- Generator의 output layer 활성함수로 tanh 사용, 나머지는 ReLu 사용
- Discriminator의 활성 함수로 LeakyReLu 사용

