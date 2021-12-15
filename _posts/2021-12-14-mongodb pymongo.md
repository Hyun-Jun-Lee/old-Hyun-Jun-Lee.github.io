---
title:  "[MongoDB] pymongo"
excerpt: "pymongo"

categories:
- DB

toc: True
toc_sticky: True

date: 2021-12-14
last_modified_at: 2021-12-14
---

# [MongoDB] pymongo

## DB 연결하기

```python
import pymongo

# conn = pymongo.MongoClient(mongo_server, 27017)
conn = pymongo.MongoClient()
print(conn.list_database_names())

# Database 연결 or 생성
mydb=conn['mydb']

# collection 연결 or 생성
mycollection = mydb['mycollection']
```

<br>

## document INSERT

- `insert_one()` == `insertOne`

```python
post = {"author": "Mike", "text": "My first blog post!", "tags": ["mongodb", "python", "pymongo"] }

mycollection.insert_one(post)

# list 삽입가능
mycollection.insert_one({'title' : '암살', 'castings' : ['이정재', '전지현', '하정우']})

# primary key 확인
mycollection.inserted_id
```

- 없는 컬렉션에 문서 삽입 시, MongoDB가 컬렉션을 자동 생성

<br>

## document Read

- `find_one()` : 1개 데이터 찾기

```python
mycollection.find_one()

{'_id': ObjectId('5d329c5fc92b6508c3f5d300'),
 'author': 'Mike',
 'text': 'My first blog post!',
 'tags': ['mongodb', 'python', 'pymongo']}
 ```

 - `find({'키':'값'})` : 여러 데이터 찾기, 매개변수 없으면 mysql의 `SELECT *`와 같음

```python
# 0 인 경우 출력 X/ 1 인 경우 출력 O
mycollection.find({}, { "_id": 0, "mb_name": 1, "mb_level": 1 })
```

<br>

