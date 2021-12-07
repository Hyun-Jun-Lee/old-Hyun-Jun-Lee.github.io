---
title:  "[MongoDB] CURD vs RDBMS 1"
excerpt: "RDBMS와 비교하며 CURD 익히기"

categories:
- DB

toc: True
toc_sticky: True

date: 2021-12-07
last_modified_at: 2021-12-07
---

# MongoDB CURD

## 데이터 입력 (Create)

- vs SQL INSERT

```sql
-- mysql
INSERT INTO people(user_id, age, status)
VALUES ("bcd001", 45, "A")

-- mongoDB
db.people.insertOne(
    {user_id:"bcd001", age: 45, status: "A"}
)
```

- insertMany

```sql
db.articles.insertMany(
   [
     { subject: "coffee", author: "xyz", views: 50 },
     { subject: "Coffee Shopping", author: "efg", views: 5 },
     { subject: "Baking a cake", author: "abc", views: 90  },
     { subject: "baking", author: "xyz", views: 100 },
     { subject: "Café Con Leche", author: "abc", views: 200 }
   ]
)
```

> Example

- employees Collection 생성 {capped:true, size:100000} Capped Collection, size는 100000 으로 생성
- 다음 Document 데이터 넣기
  - user_id 가 bcd001, age 가 45, status 가 A 인 Document
  - user_id 가 bcd002, age 가 25, status 가 B 인 Document

```sql
-- collection 생성/ 'capped:true' = 최조 제한된 크기로 생성된 공간에서만 데이터 저장하는 설정
db.createCollection("employees", {capped:true, size:10000})

-- 데이터 입력
db.employees.insertMany(
    [
        {user_id:"bcd001", age:45, status:"A"},
        {user_id:"bcd002", age:25, status:"B"}
    ]
)
```