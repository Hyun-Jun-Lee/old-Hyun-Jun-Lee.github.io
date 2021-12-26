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