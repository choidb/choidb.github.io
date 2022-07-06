---
title: 'SQL Basics'
use_math: true
categories:
  - dr
---

**목차**  

[1. SQL 소개](#1-sql-소개)  
[2. 데이터베이스 설계](#2-데이터베이스-설계)  
[3. 스키마](#3-스키마)  
[4. SQL Basics](#4-sql-basics)  

---
* Contents
  1. SQL
  2. 데이터베이스 관계
  3. SQL 싱글 테이블 관련 문법 활용

[Lucidchart](https://www.lucidchart.com/pages/) : 스키마 작성하는 웹 기반 다이어그램 작성 애플리케이션  
스키마: 자료의 구조, 자료의 표현 방법, 자료 간의 관계를 형식 언어로 정의한 구조  
[DBeaver](https://dbeaver.io/) : SQL 클라이언트이자 데이터베이스 관리 도구  
[SQL 조인 시각 사이트](https://sql-joins.leopard.in.ua/)  
* SQL 연습 사이트  
[w3schools](https://www.w3schools.com/SQl/sql_exercises.asp)  
[sqlbolt](https://sqlbolt.com/)  
[sqlzoo](https://sqlzoo.net/wiki/SQL_Tutorial)  
[codeacademy](https://www.codecademy.com/learn/learn-sql)  
[techonthenet](https://www.techonthenet.com/sql/)  
* 데이터베이스 정규화
[Database Normalization Basics](https://www.lifewire.com/database-normalization-basics-1019735)


---
## 1. SQL 소개  
* 데이터베이스의 필요성
1. In-Memory
    프로그램 실행될 때만 데이터가 존재하므로 

2. File I/O
    파일을 읽어오는 방식으로 작동하는 형태
    예) 엑셀, csv 파일은 매번 읽어와야됨, 데이터량이 많을수록 다루기 어려워짐
    관계형 데이터베이스에서는 하나의 CSV 파일이나 엑셀 시트를 한 개의 테이블로 저장할 수 있으며 한번에 여러 개의 테이블을 가질 수 있기 때문에 SQL 을 활용해 데이터를 가져오기가 더 수월하다.

SQL(Structured Query Language)은 데이터베이스 언어의 기준으로 주로 관계형 데이터베이스에서 사용되며, 구조화된 쿼리 언어이다. MySQL, Oracle, SQLite, PostgreSQL 등이 있다. 
* 쿼리(query): '질의문', 저장되어 있는 정보를 필터하기 위한 질문. 예)  검색을 할 때 입력하는 검색어
* **SQL은 데이터베이스에 쿼리를 보내 원하는 데이터를 불러오게 한다.**
* SQL 종류
  * Data Definition Language (DDL)
    * 데이터를 정의할 때 사용되는 언어. 
      * CREATE: 테이블을 만들 때 사용
      * DROP: 테이블을 제거할 때 사용
  * Data Manipulation Language (DML)
    * 데이터베이스에 데이터를 저장할 때 사용되는 언어
      * INSERT: 새로운 레코드를 추가할 때 사용
      * DELETE: 데이터 삭제
      * UPDATE: 변경
  * Data Control Language (DCL)
    * 데이터베이스에 대한 접근 권한과 관련된 문법
      * GRANT: 권한 부여
      * REVOKE: 권한 회수
  * Data Query Language (DQL)
    * 정해진 스키마 내에서 쿼리를 할 수 있는 언어
      * SELECT
    * DQL 은 DML 의 일부분으로 말하기도 함
  * Transaction Control Language (TCL)
    * DML 을 거친 데이터 변경사항을 수정
      * COMMIT: DML이 작업한 내용을 데이터베이스에 커밋
      * ROLLBACK: 커밋했던 내용을 다시 롤백

## 2. 데이터베이스 설계
* 관계형 데이터베이스(Relational database)
  * 구조화된 데이터가 하나의 테이블로 표현
  * 관계형 데이터베이스 키워드
    * 데이터 : 각 항목에 저장되는 값
    * 테이블 (혹은 relation) : 사전에 정의된 행과 열로 구성되어 있는 체계화된 데이터
    * 필드 (혹은 column) : 테이블의 열
    * 레코드 (혹은 tuple) : 테이블의 한 행의 저장된 정보
    * 키 : 테이블의 각 레코드를 구분할 수 있는 값.  
각 레코드마다 고유값이어야 함.  
기본키 (primary key) 와 외래키 (foreign key) 등이 있을 수 있음.

### - 자기참조 관계 (Self Referencing Relationship) = 순환관계(Recursive Relationship)
정의
하나의 엔터티(Entity)가 다른 엔터티가 아닌 자기 자신과 관계를 맺는 타입  
동일 Entity 타입 내에서 자기가 자기의 인스턴스를 참조하는 구조, 대표적으로 조직을 표현할 때 자주 사용

### - 관계 종류
1. 1:1 관계  
    테이블의 레코드 하나당 다른 테이블의 한 레코드와 연결되어 있는 경우

2. 1:N 관계  
    테이블의 레코드 하나당 여러 개의 레코드와 연결되어 있는 경우

3. N:N 관계  
    여러 개의 레코드가 여러 개의 레코드를 가지는 관계  
    해당 관계의 경우에는 따로 '조인 테이블'을 만들어 관리


## 3. 스키마  
|Teachers|      
|---|     
|Name|
|Department|
|Classes|  

|Classes|
|---|
|Name|
|Room Number|
|Teacher|
|Students|

두 개의 표에서 Teachers와 Classes는 **Entity**(**엔티티**)에 해당  
엔티티 Teachers에서 Name, Department, Classes는 **Fields**(행렬에서 열(Column)에 해당)라고 한다.  
**레코드**(**Record**)는 테이블에 저장된 항목이다. 행렬에서 행(Row)라고 볼 수 있다. 예를 들어 Teachers 엔티티의 Fields 안에  
|Nmae|Department|Classes|
|---|---|---|
| Cynthia | Music| Music Theory, Brass Methods |

위와 같이 Cynthia, Music, Music Theory, Brass Methods의 내용이 저장된 항목(Record)이라 볼 수 있음. 

## 4. SQL Basics
* SQLite 샘플 데이터  
[sqlite tutorial](https://www.sqlitetutorial.net/sqlite-sample-database/)

* 기본 쿼리문  
  * Select
  * Where
  * And, Or, Not
  * Order By
  * Insert Into
  * Null Values
  * Update
  * Delete
  * Count
  * Like
  * Wildcards
  * Aliases
  * Joins
    * Inner Join
    * Left Join
    * Right Join
  * Group By
>
* 데이터베이스 관련
  * SQL Create DB
  * SQL Drop DB
  * SQL Create Table
  * SQL Drop Table
  * SQL Alter Table
  * SQL Not Null
  * SQL Unique
  * SQL Primary Key
  * SQL Foreign Key
  * SQL Default
  * SQL Auto Increment
  * SQL Dates
> 
* SQL 명령어 예시
  * SELECT
    * 데이터셋에 포함될 특성들을 특정
```SQL
SELECT 'hello world';   -- 일반 문자열
SELECT 2;               -- 숫자
SELECT 15 + 3;          -- 연산
```
  * FROM
    * 테이블과 관련이 있는 경우 필수로 명시해야 하는 명령어  \
    결과들을 도출해낼 데이터베이스 테이블을 명시
```SQL
-- 특정 특성을 테이블에서 사용
SELECT 특성_1
FROM 테이블_이름;
-- 예시
SELECT FirstName
FROM customers;

-- 특정 특성들을 테이블에서 사용
SELECT 특성_1, 특성_2
FROM 테이블_이름;
-- 예시
SELECT customers.FirstName, customers.LastName
FROM customers;

-- 테이블의 모든 특성을 선택
SELECT *
FROM 테이블_이름;
-- 예시
SELECT *
FROM customers;

* 는 와일드카드 (wildcard) 로 전부 선택할 때에 사용
```

  * WHERE
    * (선택적으로) 필터 역할을 하는 쿼리문
```SQL
-- 특정 값과 동일한 데이터 찾기
SELECT 특성_1, 특성_2
FROM 테이블_이름
WHERE 특성_1 = "특정 값";
-- 예시
SELECT customers.FirstName, customers.LastName
FROM customers
WHERE customers.FirstName = 'Helena';

-- 특정 값을 제외한 데이터 찾기
SELECT 특성_1, 특성_2
FROM 테이블_이름
WHERE 특성_2 <> "특정 값";
-- 예시
SELECT customers.FirstName, customers.LastName
FROM customers
WHERE customers.FirstName <> 'Helena';

-- 특정 값보다 크거나 작은 데이터를 필터할 때에는 '<', '>', 비교하는 값을 포함하는 '이상', '이하' 값은 '<=', '>=' 을 사용
SELECT 특성_1, 특성_2
FROM 테이블_이름
WHERE 특성_1 > "특정 값";

-- 문자열에서 특정 값과 비슷한 값들을 필터할 때에는 LIKE 와 '%' 혹은 '*' 를 사용
SELECT 특성_1, 특성_2
FROM 테이블_이름
WHERE 특성_2 LIKE "%특정 문자열%";
-- 예시
SELECT customers.FirstName, customers.LastName
FROM customers
WHERE customers.LastName LIKE '%han%';

-- 리스트의 값들과 일치하는 데이터를 필터할 때에는 IN 을 사용
SELECT 특성_1, 특성_2
FROM 테이블_이름
WHERE 특성_2 IN ("특정값_1", "특정값_2");
-- 예시
SELECT customers.FirstName, customers.LastName
FROM customers
WHERE customers.LastName IN ('Hansen', 'Johansson');

-- 값이 없는 NULL 과 같은 경우를 찾을 때에는 IS 를 사용
SELECT *
FROM 테이블_이름
WHERE 특성_1 IS NULL;
-- 예시
SELECT *
FROM employees
WHERE employees.ReportsTo is NULL;

-- 값이 없는 경우를 제외할 때에는 NOT 을 추가해 이용
SELECT *
FROM 테이블_이름
WHERE 특성_1 IS NOT NULL;
```

  * ORDER BY
    * 돌려받는 데이터 결과를 어떻게 정렬하지에 대한 선택적 항목
```SQL
-- 기본 정렬은 오름차순
SELECT *
FROM 테이블_이름
ORDER BY 특성_1;
-- 예시
SELECT *
FROM employees
ORDER BY employees.EmployeeId;

-- 내림차순으로도 정렬 가능
SELECT *
FROM 테이블_이름
ORDER BY 특성_1 DESC;
-- 예시
SELECT *
FROM employees
ORDER BY employees.EmployeeId DESC;
```
  * LIMIT
    * 돌려받는 데이터 결과 갯수를 정하기
    * 쿼리문에서 사용을 할 때에는 마지막에 추가
```SQL
-- 데이터 결과 갯수를 200개 한정
SELECT *
FROM 테이블_이름
LIMIT 200;

-- 예시
SELECT *
FROM customers
LIMIT 200;
```
  * DISTINCT
    * 유니크한 값들을 받고 싶을 때에는 SELECT 뒤에 붙여 사용
```SQL
-- 특성_1 기준으로 유니크한 값들만 선택
SELECT DISTINCT 특성_1
FROM 테이블_이름;
-- 예시
SELECT DISTINCT employees.Title
FROM employees;

-- 특성_1, 특성_2, 특성_3 의 유니크한 '조합' 값들을 선택
SELECT
  DISTINCT
    특성_1
    ,특성_2
    ,특성_3
FROM 테이블_이름;
```
 * INNER JOIN
   * 서로 공통된 부분으로만 연결
```SQL
-- INNER JOIN 이나 JOIN 으로 실행
SELECT *
FROM 테이블_1
JOIN 테이블_2 ON 테이블_1.특성_A = 테이블_2.특성_B;

-- 예시
SELECT 
  c.FirstName || ' ' || c.LastName AS 'Customer Name',
  e.Firstname || ' ' || e.LastName AS 'Employee Name'
FROM customers AS c
JOIN employees AS e ON c.SupportRepId = e.EmployeeId;
```
  * OUTER JOIN
    * Outer JOIN 은 다양한 선택지가 있음
      * 기본: 'left inclusive', 'right inclusive', 'full outer join'
```SQL
-- LEFT INCLUSIVE: LEFT OUTER JOIN 으로 진행
SELECT *
FROM 테이블_1
LEFT OUTER JOIN 테이블_2 ON 테이블_1.특성_A = 테이블_2.특성_B

-- RIGHT INCLUSIVE 도 비슷하게 RIGHT OUTER JOIN 으로 진행
SELECT *
FROM 테이블_1
RIGHT OUTER JOIN 테이블_2 ON 테이블_1.특성_A = 테이블_2.특성_B

-- sqlite 에서는 RIGHT OUTER JOIN / FULL OUTER JOIN 을 지원하지 않기 때문에 순서를 바꾸어 LEFT JOIN 을 이용하는 방법을 사용
```
```SQL
-- 명령어 여러개 조합 예시
SELECT c.CustomerId, c.FirstName, count(c.City) as 'City Count'
FROM customers AS c
JOIN employees AS e ON c.SupportRepId = e.EmployeeId
WHERE c.Country = 'Brazil'
GROUP BY c.City
ORDER BY 3 DESC, c.CustomerId ASC
LIMIT 3;
```
