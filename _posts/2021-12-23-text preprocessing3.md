---
title:  "Integer Encoding/Padding"
excerpt: "Text Preprocessing"

categories:
- AIB2 Study

toc: True
toc_sticky: True

date: 2021-12-23
last_modified_at: 2021-12-23
---

# Integer Encoding/Padding

## Integer Encoding

### Integer Encoding 하기 전 전처리

```python
from nltk.tokenize import sent_tokenize
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords

raw_text = "A barber is a person. a barber is good person. a barber is huge person. he Knew A Secret! The Secret He Kept is huge secret. Huge secret. His barber kept his word. a barber kept his word. His barber kept his secret. But keeping and keeping such a huge secret to himself was driving the barber crazy. the barber went up a huge mountain."

# 문장 토큰화
sentences = sent_tokenize(raw_text)
print(sentences)
>>> ['A barber is a person.', 'a barber is good person.', 'a barber is huge person.', 'he Knew A Secret!', 'The Secret He Kept is huge secret.', 'Huge secret.', 'His barber kept his word.', 'a barber kept his word.', 'His barber kept his secret.', 'But keeping and keeping such a huge secret to himself was driving the barber crazy.', 'the barber went up a huge mountain.']
```

정수인코딩은 텍스트를 수치화하는 단계이고 본격적으로 자연어 처리 작업에 들어간다는 의미이므로, 단어가 텍스트일 때만 할 수 있는 최대한의 전처리를 끝내놓아야 함<br>

- ex)
  - 모든 단어를 소문자로 만들어 단어 수를 줄이기
  - stopdword
  - 낮은 빈도수 단어 제거


```python
# 단어 count 위한 dict
vocab = {}
preprocessed_sentences = []
stop_words = set(stopwords.words('english'))

for sentence in sentences:
    # 단어 토큰화
    tokenized_sentence = word_tokenize(sentence)
    result = []

    for word in tokenized_sentence: 
        word = word.lower() # 모든 단어를 소문자화하여 단어의 개수를 줄인다.
        if word not in stop_words: # 단어 토큰화 된 결과에 대해서 불용어를 제거한다.
            if len(word) > 2: # 단어 길이가 2이하인 경우에 대하여 추가로 단어를 제거한다.
                result.append(word)
                if word not in vocab:
                    vocab[word] = 0 
                vocab[word] += 1
    preprocessed_sentences.append(result) 
print(preprocessed_sentences)

>>> [['barber', 'person'], ['barber', 'good', 'person'], ['barber', 'huge', 'person'], ['knew', 'secret'], ['secret', 'kept', 'huge', 'secret'], ['huge', 'secret'], ['barber', 'kept', 'word'], ['barber', 'kept', 'word'], ['barber', 'kept', 'secret'], ['keeping', 'keeping', 'huge', 'secret', 'driving', 'barber', 'crazy'], ['barber', 'went', 'huge', 'mountain']]
```

<br>

### keras

- `fit_on_texts()` : 입력한 텍스트로부터 단어 빈도수가 높은 순으로 낮은 정수 인덱스를 부여
  - `word_index` : 각 단어에 부여된 인덱스 확인
  - `word_counts` : 각 단어 count 수


```python
from tensorflow.keras.preprocessing.text import Tokenizer

tokenizer = Tokenizer()

# fit_on_texts()안에 코퍼스를 입력으로 하면 빈도수를 기준으로 단어 집합을 생성.
tokenizer.fit_on_texts(preprocessed_sentences) 

print(tokenizer.word_index)
>>> {'barber': 1, 'secret': 2, 'huge': 3, 'kept': 4, 'person': 5, 'word': 6, 'keeping': 7, 'good': 8, 'knew': 9, 'driving': 10, 'crazy': 11, 'went': 12, 'mountain': 13}

print(tokenizer.word_counts)
>>> OrderedDict([('barber', 8), ('person', 3), ('good', 1), ('huge', 5), ('knew', 1), ('secret', 6), ('kept', 4), ('word', 2), ('keeping', 2), ('driving', 1), ('crazy', 1), ('went', 1), ('mountain', 1)])
```

- `texts_to_sequences()` : 각 단어를 이미 정해진 인덱스로 변환
- `tokenizer = Tokenizer(num_words=숫자)` : 빈도수가 높은 상위 몇 개의 단어만 사용하겠다고 지정

```python 
print(tokenizer.texts_to_sequences(preprocessed_sentences))
>>> [[1, 5], [1, 8, 5], [1, 3, 5], [9, 2], [2, 4, 3, 2], [3, 2], [1, 4, 6], [1, 4, 6], [1, 4, 2], [7, 7, 3, 2, 10, 1, 11], [1, 12, 3, 13]]

vocab_size = 5
# 상위 5개 단어만 사용/ +1을 하는 이유는 num_words는 0부터 카운트하기 때문에
tokenizer = Tokenizer(num_words = vocab_size + 1) 
tokenizer.fit_on_texts(preprocessed_sentences)

# 실제 적용은 text_to_sequences 사용할 때 적용됨(word_index,word_counts에는 적용 X)
print(tokenizer.texts_to_sequences(preprocessed_sentences))
>>> [[1, 5], [1, 5], [1, 3, 5], [2], [2, 4, 3, 2], [3, 2], [1, 4], [1, 4], [1, 4, 2], [3, 2, 1], [1, 3]]
```

> IF) `word_index`, `word_counts에도` 지정된 num_words 만큼만 남기고 싶다면?

```python
tokenizer = Tokenizer()
tokenizer.fit_on_texts(preprocessed_sentences)

vocab_size = 5
# index가 num_words 이상인 'word만' 저장
words_frequency = [word for word, index in tokenizer.word_index.items() if index >= vocab_size + 1] 

# 인덱스가 5 초과인 단어 제거
for word in words_frequency:
    del tokenizer.word_index[word] # 해당 단어에 대한 인덱스 정보를 삭제
    del tokenizer.word_counts[word] # 해당 단어에 대한 카운트 정보를 삭제

print(tokenizer.word_index)
>>> {'barber': 1, 'secret': 2, 'huge': 3, 'kept': 4, 'person': 5}

print(tokenizer.word_counts)
>>> OrderedDict([('barber', 8), ('person', 3), ('huge', 5), ('secret', 6), ('kept', 4)])
```