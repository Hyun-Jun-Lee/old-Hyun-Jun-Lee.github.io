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

## Document 입력 (Create)

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

<br>

## Document 읽기 (Read)

- find()/findOne()

```sql
db.people.find() == SELECT * FROM people
db.people.find({}, {user_id:1, status:1, _id:0}) == SELECT user_id, status FROM people
db.people.find({ status : "A"}) == SELECT * FROM people WHERE status ="A"
db.people.find({status:"A", age:50}) == SELECT * FROM people WHERE status = "A" AND age=50
db.people.find({$or:[{status:"A"}, {age:50}]}) == SELECT * FROM people WHERE status = "A" OR age = 50
```

- 비교문법

```sql
$eq     =    Matches values that are equal to a specified value.
$gt     >    Matches values that are greater than a specified value.
$gte    >=   Matches values that are greater than or equal to a specified value.
$in          Matches any of the values specified in an array.
$lt     <    Matches values that are less than a specified value.
$lte    <=   Matches values that are less than or equal to a specified value.
$ne     !=   Matches all values that are not equal to a specified value.
$nin         Matches none of the values specified in an array.

-- Example

db.people.find({ age: { $gt: 25 } }) - SELECT * FROM people WHERE age > 25
db.people.find({ age: { $lt: 25 } }) - SELECT * FROM people WHERE age < 25
db.people.find({ age: { $gt: 25, $lte: 50 } }) - SELECT * FROM people WHERE age > 25 AND age <= 50
db.people.find( { age: { $nin: [ 5, 15 ] } } )) - SELECT * FROM people WHERE age = 5 or age = 15

- SELECT * FROM people WHERE user_id like "%bc%"
db.people.find( { user_id: /bc/ } )
db.people.find( { user_id: { $regex: /bc/ } } )

- SELECT * FROM people WHERE user_id like "bc%"
db.people.find( { user_id: /^bc/ } )
db.people.find( { user_id: { $regex: /^bc/ } } )

db.people.find( { status: "A" } ).sort( { user_id: 1 } ) - SELECT * FROM people WHERE status = "A" ORDER BY user_id ASC 
db.people.find( { status: "A" } ).sort( { user_id: -1 } ) - SELECT * FROM people WHERE status = "A" ORDER BY user_id DESC

db.people.count() - SELECT COUNT(*) FROM people

- SELECT COUNT(user_id) FROM people
db.people.count( { user_id: { $exists: true } } )
db.people.find( { user_id: { $exists: true } } ).count()

- SELECT COUNT(*) FROM people WHERE age > 30
db.people.count( { age: { $gt: 30 } } )
db.people.find( { age: { $gt: 30 } } ).count()

db.people.distinct( "status" ) - SELECT DISTINCT(status) FROM people
```

<br>

## Document 수정 (Update)

- updateOne(), updateMany()
  - `$set` : field 값 설정
  - `$inc` : field 값 증가or 감소 ($inc:{age:2} = age + 2)

```sql
db.people.updateMany( { age: { $gt: 25 } }, { $set: { status: "C" } } ) == UPDATE people SET status = "C" WHERE age > 25

db.people.updateMany( { status: "A" } , { $inc: { age: 3 } } ) == UPDATE people SET age = age + 3 WHERE status = "A"
```

<br>

## Document 삭제 (Delete)

- removeOne(), removeMany()

```sql
db.people.deleteMany( { status: "D" } ) == DELETE FROM people WHERE status = "D"

db.people.deleteMany({}) == DELETE FROM people
```