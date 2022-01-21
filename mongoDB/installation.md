## NoSQL이란?

NoSQL(not only SQL)은 2000년대 말 스토리지 비용이 급격히 하락하면서 등장한 새로운 형태의 데이터베이스이다.
데이터를 사용하는 애플리케이션이 급격히 증가함에 따라 정형 데이터 뿐만 아니라 비정형 데이터도 증가하였고, 스키마를 미리 정의하는 것이 불가능하게 되어 각 데이터에 따라 스키마 변경이 가능한 유연한 형태의 NoSQL이 탄생하게 되었다.복잡한 쿼리가 가능하며 문서 내부 다른 문서를 삽입할 수 있다.

## NoSQL 데이터베이스 유형

### 문서(Document)데이터베이스

JSON(JavaScript Object Notation) 객체와 비슷한 문서에 데이터를 저장한다. 스키마는 실제 데이터 객체에 맞게 유연하게 변경되며 복잡한 쿼리가 가능하다. MongoDB가 대표적이다.

구조: Database-Collection-Document-Field

### 키-값 데이터베이스

키-값이 포함되어 있는 간단한 유형의 데이터 베이스이며, 키를 참조하는 방식으로만 값에 접근할 수 있다. 주로 캐싱에 사용되며 Redis가 대표적이다.


## 설치

1. https://www.mongodb.com/try/download/enterprise
2. 시스템 환경변수 path 설정

## 윈도우에서 MongoDB 서버 on/off

CMD 관리자 모드 실행

\> net start MongoDB

\> net stop MongoDB

## 윈도우에서 MongoDB 접속

CMD

\> mongo

## 기본

\> show dbs // 데이터베이스 전체 목록 보기

\> use {db} // 데이터베이스 생성 및 조회

\> show collections //컬렉션 조회

\> db.stats() //데이터베이스, 컬렉션의 하위 계층 정보

\> db.{collection}.count()

## CRUD

\> db.dropDatabase() //데이터베이스 제거

\> db.{collection}.insertOne({}) //도큐먼트 생성

\> db.{collection}.insertMany([{}]) //다수의 도큐먼트 생성

\> db.{collection}.find() ////컬렉션 전체 목록 조회

\> db.{collection}.find({})

\> db.{collection}.find({query criteria}, {projection: 0|1}).limit(%d)

\> db.{collection}.drop() //컬렉션 제거

\> db.{collection}.updateOne()/updateMany()/replaceOne()

\> db.{collection}.updateMany({update filter}, {$set:{update action}})

\> db.{collection}.deleteOne()/deleteMany()

\> db.{collection}.find({}).explain("executionStats") //쿼리 경로에 대한 정보 제공

\> db.{collection}.createIndex({}) //인덱스 생성

\> db.{collection}.getIndexes //인덱스 조회

## 예제

\> db.collection.find({$or:[{status: 'A'}, {qty: { $lt: 30}}]})

\> db.collection.find({status:{$nin:['A']}})

\> db.collection.find({status: "A", $or: [{qty:{$lt: 30}}, {item: /^p/}]})

\> db.collection.find({qty: {$mod:[50,0]}})

## 참고

쿼리 연산자(query operator): https://docs.mongodb.com/manual/reference/operator/query/#std-label-query-selectors
