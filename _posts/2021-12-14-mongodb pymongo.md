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