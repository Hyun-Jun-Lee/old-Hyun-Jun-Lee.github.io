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

# connection = pymongo.MongoClient(mongo_server, 27017)
conn = pymongo.MongoClient()
print(conn.list_database_names())
```