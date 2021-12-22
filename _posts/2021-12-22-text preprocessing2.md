---
title:  "어간 추출(Stemming)/표제어 추출(Lemmatization)"
excerpt: "Text Preprocessing"

categories:
- AIB2 Study

toc: True
toc_sticky: True

date: 2021-12-22
last_modified_at: 2021-12-22
---

# 어간 추출(Stemming)/표제어 추출(Lemmatization)

## 표제어 추출(Lemmatization)

표제어 추출은 단어들이 다른 형태를 가지더라도, 그 뿌리 단어를 찾아가서 단어의 개수를 줄일 수 있는지 판단합니다. 예를 들어서 am, are, is는 서로 다른 스펠링이지만 그 뿌리 단어는 be라고 볼 수 있습니다. 이때, 이 단어들의 표제어는 be라고 합니다.

- 어간(stem) : 단어의 의미를 담고 있는 핵심적인 부분
- 접사(affix) : 단어에 추가적인 의미를 주느 부분

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

words = ['policy', 'doing', 'organization', 'have', 'going', 'love', 'lives', 'fly', 'dies', 'watched', 'has', 'starting']

print('표제어 추출 전 :',words)
print('표제어 추출 후 :',[lemmatizer.lemmatize(word) for word in words])

>>> 표제어 추출 전 : ['policy', 'doing', 'organization', 'have', 'going', 'love', 'lives', 'fly', 'dies', 'watched', 'has', 'starting']
>>> 표제어 추출 후 : ['policy', 'doing', 'organization', 'have', 'going', 'love', 'life', 'fly', 'dy', 'watched', 'ha', 'starting']
```

표제어 추출은 단어의 형태가 적절히 보존되는 양상을 보이는 특징, 본래 단어의 품사 정보를 알아야 보다 정확한 결과를 얻을 수 있음

```python
lemmatizer.lemmatize('dies', 'v')
>>> 'die'

lemmatizer.lemmatize('watched', 'v')
>>> 'watch'

lemmatizer.lemmatize('has', 'v')
>>> 'have'
```

<br>

## 어간 추출(Stemming)

어간 추출은 형태학적 분석을 단순화한 버전이라고 볼 수도 있고, 정해진 규칙만 보고 단어의 어미를 자르는 어림짐작의 작업이라고 볼 수도 있다. 이 작업은 섬세한 작업이 아니기 때문에 어간 추출 후에 나오는 결과 단어는 사전에 존재하지 않는 단어일 수도 있다.

```python
from nltk.stem import PorterStemmer
from nltk.stem import LancasterStemmer

porter_stemmer = PorterStemmer()
lancaster_stemmer = LancasterStemmer()

words = ['policy', 'doing', 'organization', 'have', 'going', 'love', 'lives', 'fly', 'dies', 'watched', 'has', 'starting']
print('어간 추출 전 :', words)
print('포터 스테머의 어간 추출 후:',[porter_stemmer.stem(w) for w in words])
print('랭커스터 스테머의 어간 추출 후:',[lancaster_stemmer.stem(w) for w in words])

>>> 어간 추출 전 : ['policy', 'doing', 'organization', 'have', 'going', 'love', 'lives', 'fly', 'dies', 'watched', 'has', 'starting']
>>> 포터 스테머의 어간 추출 후: ['polici', 'do', 'organ', 'have', 'go', 'love', 'live', 'fli', 'die', 'watch', 'ha', 'start']
>>> 랭커스터 스테머의 어간 추출 후: ['policy', 'doing', 'org', 'hav', 'going', 'lov', 'liv', 'fly', 'die', 'watch', 'has', 'start']
```

<br>

## Stemming vs Lemmatization

- Stemming

```
am → am
the going → the go
having → hav
```

- Lemmatization

```
am → be
the going → the going
having → have
```