# DB 2

## SQL

structured Query Language

- 데이터베이스 관리 + CRUD 하는 언어

관계형 데이터베이스에서 데이터를 관리하기 위해 사용하는 언어

### SQL Commands

- DDL(Data Definition Language)
    - 데이터 정의 언어
    - 관계형 데이터베이스 구조(테이블, 스키마)를 정의(생성, 수정 및 삭제)하기 위한 명령어
    - create, crop, alter
- DML(Data Manipulation Language)
    - 데이터 조작 언어
    - 데이터를 조작(추가, 조회, 변경, 삭제)하기 위한 명령어
    - insert, select, update, delete
- DCL(Data Control Language)
    - 데이터 제어 언어
    - 데이터의 보안, 수행제어, 사용자 권한 부여 등을 정의하기 위한 명령어
    - grant, revoke, commit, rollback

### SQL Syntax

```jsx
ex)
SELECT column_name FROM table_name;
```

- 모든 SQL 문은 SELECT, INSERT, UPDATE 등과 같은 키워드로 시작하고 하나의 statement는 세미콜론으로 끝난다.
- 대소문자 구분 X - but, 대문자 작성 권장

```sql
CREATE TABLE contacts (
  name TEXT NOT NULL,
  age INTEGER NOT NULL,
  email TEXT NOT NULL UNIQUE
);

ALTER TABLE contacts RENAME TO new_contacts;
```

```sql
sqlite explorer
	- ddl.sqlite3
		- new_contacts
			- name : text
			- age : integer
			- email : text
```

### SQLite Data Types

- 종류
    1. NULL
        1. NULL value
        2. 정보가 없거나 알 수 없음을 의미
    2. INTEGER
        1. 정수
        2. 크기에 따라 0, 1, 2, 3, 4, 6, 8바이트와 같은 가변 크기를 가진다.
    3. REAL
        1. 실수
        2. 8바이트 부동 소수점을 사용하는 10진수 값이 있는 실수
    4. TEXT
        1. 문자 데이터
    5. BLOB
        1. 입력된 그대로 저장된 데이터 덩어리(대용 타입 없음)
        2. 바이너리 등 멀티미디어 파일
- Type Affinity
    - 타입 선호도
        - 다른 데이터베이스 엔진 간의 호환성을 최대화한다.
        - 정적이고 엄격한 타입을 사용하는 데이터베이스의 SQL문을 SQLite에서도 작동하도록 하기 위함
    - INTEGER, TEXT, BLOB, REAL, NUMERIC 이 아닌 데이터 타입이라면 지정된 선호도에 따라 5가지 선호도로 인식된다.
    

### Contraints

- 제약조건
- 입력하는 자료에 대해 제약을 정한다.
- 제약에 맞지 않는다면 입력이 거부된다.
- 사용자가 원하는 조건의 데이터만 유지하기 위한 제약
- 종류
    - NOT NULL
        - 칼럼이 NULL 값을 허용하지 않도록 지정
        - 기본적으로 테이블의 모든 컬럼은 NOT NULL 제약 조건을 명시적으로 사용하는 경우를 제외하고는 NULL 값을 허용한다.
    - UNIQUE
        - 칼럼의 모든 값이 서로 구별되거나 고유한 값이 되도록한다.
    - PRIMARY KEY
        - 테이블에서 행의 고유성을 식별하는 데 사용되는 컬럼
        - 각 테이블에는 하나의 기본 키만 있다.
    - AUTOINCREMENT
        - 사용되지 않는 값이나 이전에 삭제된 행의 값을 재사용하는 것을 방지한다.
        - INTEGER PRIMARY KEY 다음에 작성되면 해당 rowid를 다시 재사용 못하게 한다.
            - rowid
                - 테이블을 생성할 때 마다 암시적으로 자동 증가 컬럼이 생성된다.
                - 64비트 부호 있는 정수 값
                - 정수 값을 자동으로 할당
                    - 1부터 시작
    - 기타 Contraints
    

### ALTER TABLE

- Modify the structure of an existing tabel
- 기존 테이블의 구조를 수정 및 변경
    1. Rename a table
    2. Rename a column
    3. Add a new column to a table
    4. Delete a column

```sql
ALTER TABLE table_name RENAME TO new_table_name;
ALTER TABLE table_name RENAME COLUMN column_name TO new_column_name;
ALTER TABLE table_name ADD COLUMN column_definition;
ALTER TABLE table_name ADD COLUMN column_definition TEXT NOT NULL DEFAULT'no address';
ALTER TABLE table_name DROP COLUMN column_name;
```

### DROP TABLE

- Remove a table from the database
- 데이터베이스에서 테이블 제거
- 한번에 하나의 테이블만 삭제할 수 있다.
- 여러 테이블을 제거하려면 여러 DROP TABLE 문을 실행해야 한다.
- 실행 취소하거나 복구할 수 없다.

```sql
$ sqlite3 db.sqlite3
SQLite version 3.41.2 2023-03-22 11:56:21
Enter ".help" for usage hints.
sqlite> .mode csv
sqlite> .import users.csv users
```

```sql
CREATE TABLE users (
    first_name TEXT NOT NULL,
    last_name TEXT NOT NULL,
    age INTEGER NOT NUll,
    country TEXT NOT NULL,
    phone TEXT NOT NULL,
    balance INTEGER NOT NULL
);
```

## DML

- CRUD
- INSERT SELECT UPDATE DELETE

- sql query statement 만들기

```sql
SELECT * FROM users;
-- 전체
SELECT first_name, last_name FROM users;
-- 필요한 요소들을 뽑아내는 것

SELECT * FROM users ORDER BY last_name;
-- 순서를 주는 것
SELECT last_name, first_name, balance, age FROM users ORDER BY age, balance DESC;
-- 오름차순, 내림차순을 줄 수도 있고 특정 요소들로만 구성할 수 있다.
SELECT DISTINCT country FROM users;
-- 중복제거
SELECT DISTINCT country, first_name FROM users ORDER BY country;
-- 컴럼들에서 중복들을 다 제거할 때 

SELECT * FROM users WHERE balance > 777777;
-- 조건을 추가해서 특정 요소들을 보여줄 떄
SELECT * FROM users WHERE balance > 777777 ORDER BY balance;
-- 조건을 추가해서 특정 요소들을 보여줄 떄 보기 이쁘게 정렬
-- balance 대신 first_name, last_name 등을 통한 이름 순으로 정렬할 수 도 있다.
SELECT * FROM users WHERE balance < 800000 AND balance > 700000;
-- AND 를 통해 여러 조건을 붙여줄 수 있다.
SELECT * FROM users WHERE balance < 10000 OR balance > 900000;
-- OR도 물론 가능하다.
SELECT * FROM users WHERE balance > 900000;
SELECT * FROM users WHERE last_name = '류';
-- 글자로도 조건들을 찾을 수 있다.
SELECT * FROM users WHERE first_name LIKE '정_';
-- 이름을 찾을 때 wildcard(_)를 통해 특정 단어가 포함된 단어를 조건에 등록해 찾을 수 있다.
SELECT * FROM users WHERE phone LIKE '010-_________';
SELECT * FROM users WHERE phone LIKE '010-%';
SELECT * FROM users WHERE phone LIKE '%77%';
-- %를 사용하여 앞 혹은 뒤에 어떠한 것이 온다면 조건에 충족되게 하는 방법

SELECT * FROM users WHERE age >= 20 AND age < 30 ORDER BY age;
SELECT * FROM users where age LIKE '2_' ORDER BY age;
-- 20대라는 조건을 찾는 경우
SELECT * FROM users where age NOT LIKE '2_' ORDER BY age;
SELECT * FROM users WHERE NOT age >= 20 ORDER BY age;
-- 조건을 제외하고 찾는 경우 NOT의 위치를 생각하면서 사용해보자

SELECT first_name, country FROM users WHERE country in ('경상남도', '경상북도');
-- IN 을 사용하면서 조건을 걸 수 있다.

SELECT * FROM users LIMIT 10;
-- 한번에 다 나오는건 문제가 발생할 수 있기 떄문에 LIMIT를 걸 수 있다.age
SELECT * FROM users ORDER BY age LIMIT 50;
SELECT * FROM users ORDER BY age LIMIT 50 OFFSET 50;
-- 처음 몇개 이후에 리미트 몇개 LIMIT -- OFFSET --
SELECT rowid, last_name, first_name FROM users LIMIT 50 OFFSET 50;
```