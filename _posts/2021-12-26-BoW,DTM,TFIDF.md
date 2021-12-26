---
title:  "BoW/DTM/TF-IDF"
excerpt: "Count based word representation"

categories:
- AIB2 Study

toc: True
toc_sticky: True

date: 2021-12-26
last_modified_at: 2021-12-26
---

# BoW/DTM/TF-IDF

## BoW(Bag of Words)

 단어들의 순서는 전혀 고려하지 않고, 단어들의 출현 빈도(frequency)에만 집중하는 텍스트 데이터의 수치화 표현 방법

 <br>

BoW는 각 단어가 등장한 횟수를 수치화하는 텍스트 표현 방법이므로 `주로 어떤 단어가 얼마나 등장했는지를 기준으로 문서가 어떤 성격의 문서인지를 판단`하는 작업에 주로 사용('달리기', '체력', '근력'과 같은 단어가 자주 등장하면 해당 문서를 체육 관련 문서로 분류)

 <br>

 ### Ex1) '정부가 발표하는 물가상승률과 소비자가 느끼는 물가상승률은 다르다.'

 ```python
from konlpy.tag import Oket

okt = Okt()

def build_bag_of_words(document):
  # 온점 제거
  document = document.replace('.', '')
  # 형태소 분석
  tokenized_document = okt.morphs(document)

  word_to_index = {}
  bow = []

  for word in tokenized_document:  
    if word not in word_to_index.keys():
      word_to_index[word] = len(word_to_index)  
      # BoW에 전부 기본값 1을 넣는다.
      bow.insert(len(word_to_index) - 1, 1)
    else:
      # 재등장하는 단어의 인덱스
      index = word_to_index.get(word)
      # 재등장한 단어는 해당하는 인덱스의 위치에 1을 더한다.
      bow[index] = bow[index] + 1

  return word_to_index, bow

doc1 = "정부가 발표하는 물가상승률과 소비자가 느끼는 물가상승률은 다르다."
vocab, bow = build_bag_of_words(doc1)

print('vocabulary :', vocab)
>>> vocabulary : {'정부': 0, '가': 1, '발표': 2, '하는': 3, '물가상승률': 4, '과': 5, '소비자': 6, '느끼는': 7, '은': 8, '다르다': 9}

# 인덱스 4에 해당하는 물가상승률은 두 번 언급되었기 때문에 인덱스 4에 해당하는 값이 2
print('bag of words vector :', bow)
>>> bag of words vector : [1, 2, 1, 1, 2, 1, 1, 1, 1, 1]
 ```

 <br>

 ### Ex2) CountVectorizer로 BoW 만들기

 ```python
from sklearn.feature_extraction.text import CountVectorizer

corpus = ['you know I want your love. because I love you.']
vector = CountVectorizer()

# 코퍼스로부터 각 단어의 빈도수를 기록
print('bag of words vector :', vector.fit_transform(corpus).toarray()) 
>>> bag of words vector : [[1 1 2 1 2 1]]

# 각 단어의 인덱스가 어떻게 부여되었는지를 출력
print('vocabulary :',vector.vocabulary_)
>>> vocabulary : {'you': 4, 'know': 1, 'want': 3, 'your': 5, 'love': 2, 'because': 0}
 ```

you와 love는 두 번씩 언급되었으므로 각각 인덱스 2와 인덱스 4에서 2의 값을 가지며, 그 외의 값에서는 1의 값을 가짐<br>
I가 사라진 이유는 CountVectorizer가 기본적으로 길이가 2이상인 문자에 대해서만 토큰으로 인식하기 때문

> CountVectorizer는 단지 띄어쓰기만을 기준으로 단어를 자르는 낮은 수준의 토큰화를 진행하고 BoW를 만든다(띄어쓰기가 잘 지켜지지 않는 한국어에서는 사용이 어려움)

<br>

## 문서 단어 행렬(Document-Term Matrix, DTM)

서로 다른 문서들의 BoW들을 결합한 표현 방법, 다수의 문서에서 등장하는 각 단어들의 빈도를 행렬로 표현한 것

![image](https://user-images.githubusercontent.com/76996686/147411916-04ab2c72-8ff2-49fc-a7b7-66c4b971945a.png)

<br>

### DTM의 한계점

1. 희소 표현(Sparse representation)

원-핫 벡터는 공간적 낭비와 계산 리소스를 증가시킬 수 있음, 만약 가지고 있는 전체 코퍼스가 방대한 데이터라면 문서 벡터의 차원은 수만 이상의 차원을 가질 수도 있다. 또한, 은 문서 벡터가 대부분의 값이 0을 가질 수도 있다.

원-핫 벡터나 DTM과 같은 대부분의 값이 0인 표현을 희소 벡터(sparse vector) 또는 희소 행렬(sparse matrix)라고 부르는데, 희소 벡터는 많은 양의 저장 공간과 높은 계산 복잡도를 요구하기 때문에, 전처리를 통해 단어 집합의 크기를 줄이는 것은 중요하다.

> 단어 집합 크기 줄이는 방법 : 구두점, 빈도수가 낮은 단어, 불용어 제거, 어간/표제어 추출 등

2. 단순 빈도 수 기반 접근

어에 대해서 DTM을 만들었을 때, 불용어인 the는 어떤 문서이든 자주 등장할 수 밖에 없기에 비교하고 싶은 문서1, 문서2, 문서3에서 동일하게 the가 빈도수가 높다고 해서 이 문서들이 유사한 문서라고 판단해서는 안된다.

이런 문제를 해결하기 위해 불용어와 중요한 단어에 대해 가중치를 부여한 방법이 TF-IDF

<br>

## TF-IDF(Term Frequency-Inverse Document Frequency)

단어의 빈도와 역 문서 빈도(문서의 빈도에 특정 식을 취함)를 사용하여 DTM 내의 각 단어들마다 중요한 정도를 가중치로 주는 방법

<br>

TF-IDF는 주로 문서의 유사도를 구하는 작업, 검색 시스템에서 검색 결과의 중요도를 정하는 작업, 문서 내에서 `특정 단어의 중요도`를 구하는 작업에 주로 사용

- 문서를 d, 단어를 t, 문서의 총 개수를 n이라고 표현할 때 TF, DF, IDF 정의

1. tf(d,t) : 특정 문서 d에서의 특정 단어 t의 등장 횟수(DTM의 값)
2. dt(t) : 특정 단어 t가 등장한 문서의 수
3. idf(d, t) : df(t)에 반비례하는 수

$$idf(d,t) = \log(\frac{n}{1+df(t)})$$

IDF는 DF의 역수로, 총 문서의 수 n이 커질 수록 IDF의 값이 기하급수적으로 커지기 때문에 log 사용, log를 사용하지 않으면 희귀 단어에 엄청난 가중치가 부여되기 때문<br>
+1을 해주는 이유는 특정 단어가 전체 문서에서 등장하지 않을 경우에 분모가 0이 되는 상황을 방지 위함. 
 
<br>

TF-IDF는 모든 문서에서 자주 등장하는 단어는 중요도가 낮다고 판단하고, 특정 문서에서만 자주 등장하는 단어는 중요도가 높다고 판단. TF-IDF 값이 낮으면 중요도가 낮은 것이며, TF-IDF 값이 크면 중요도가 큰 것

### 사이킷런을 이용한 DTM과 TF-IDF 실습

- DTM

```python
from sklearn.feature_extraction.text import CountVectorizer

corpus = [
    'you know I want your love',
    'I like you',
    'what should I do ',    
]

vector = CountVectorizer()

# 코퍼스로부터 각 단어의 빈도 수를 기록한다.
print(vector.fit_transform(corpus).toarray()) 
>>> [[0 1 0 1 0 1 0 1 1]
    [0 0 1 0 0 0 0 1 0]
    [1 0 0 0 1 0 1 0 0]]

# 각 단어의 인덱스가 어떻게 부여되었는지를 보여준다.
print(vector.vocabulary_) 
>>> {'you': 7, 'know': 1, 'want': 5, 'your': 8, 'love': 3, 'like': 2, 'what': 6, 'should': 4, 'do': 0}
```

- TfidfVectorizer

```python
from sklearn.feature_extraction.text import TfidfVectorizer

corpus = [
    'you know I want your love',
    'I like you',
    'what should I do ',    
]

tfidfv = TfidfVectorizer().fit(corpus)

print(tfidfv.transform(corpus).toarray())
>>>
[[0.         0.46735098 0.         0.46735098 0.         0.46735098 0.         0.35543247 0.46735098]
 [0.         0.         0.79596054 0.         0.         0.         0.         0.60534851 0.        ]
 [0.57735027 0.         0.         0.         0.57735027 0.         0.57735027 0.         0.        ]]

print(tfidfv.vocabulary_)
>>> {'you': 7, 'know': 1, 'want': 5, 'your': 8, 'love': 3, 'like': 2, 'what': 6, 'should': 4, 'do': 0}
```