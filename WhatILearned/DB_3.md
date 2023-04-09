# DB 3

## Grouping data

- Aggregate function
    - 집계 함수
    - 최대값, 최소값, 평균, 합계 및 개수를 계산
    - SELECT 문의 GROUP BY와 함께 종종 사용됨
    - AVG(), COUNT(), MAX(), MIN(), SUM()
    - AVG(), MAX(), MIN(), SUM()은 숫자를 기준으로 계산이 되어져야 하기 때문에 데이터 타입이 숫자(INTEGER)일 때만 사용가능하다.

```sql
-- users table 생성
CREATE TABLE users (
    first_name TEXT NOT NULL,
    last_name TEXT NOT NULL,
    age INTEGER NOT NULL,
    country TEXT NOT NULL,
    phone TEXT NOT NULL,
    balance INTEGER NOT NULL
);
```

```sql
SELECT COUNT(*) FROM users;
-- count를 사용하여 전체의 갯수를 찾는 법

SELECT AVG(balance) FROM users;
-- 계좌 잔고의 평균을 구하는 함수 AVG
SELECT DISTINCT country FROM users;
-- 중복 지역 제거
SELECT country, AVG(balance) FROM users WHERE country LIKE '전라북도';
-- 지역과 지역 잔고의 평균을 찾는방법
SELECT max(balance) FROM users;
-- 계좌 잔고의 최댓값
SELECT min(balance) FROM users;
-- 계좌 잔고의 최솟값
SELECT sum(balance) FROM users;
-- 계좌 잔고의 합계
SELECT COUNT(*), MAX(balance), MIN(age) FROM users;
-- 다양한 방식으로 데이터를 찾을 수 있다.

SELECT country, avg(balance) FROM users GROUP BY country ORDER BY avg(balance) DESC;
-- 지역별로 잔고 평균과 묶어서 찾는 방법(GROUP BY) 내림차순으로 정렬
SELECT AVG(age) FROM users WHERE age >= 25;
-- 25살 이상 사람들의 평균 나이
SELECT last_name, COUNT() FROM users GROUP BY last_name;
-- 성씨별로 각각 몇명인지 찾기
SELECT last_name, COUNT(*) AS number_of_name FROM users GROUP BY last_name;
-- AS 로 조사하는 컬럼명을 임시로 변경해서 조회하는 방법
-- 실제 컬럼을 변경하는 것은 아니다!

SELECT
    country AS '지역',
    COUNT(*) AS '총인구',
    AVG(balance) AS '평균잔고',
    MAX(balance) AS '최고',
    MIN(balance) AS '최저'
FROM users
WHERE country='경기도';
-- 정리해서 표현할 수 있다.
```

## Changing data

```sql
CREATE TABLE classmates (
    name TEXT NOT NULL,
    age INTEGER NOT NULL,
    address TEXT NOT NULL
);
```

```sql
-- 데이터 정보 넣기
INSERT INTO classmates (name, age, address)
VALUES ('홍길동', 25, '서울');

INSERT INTO classmates
VALUES
    ('김철수', 30, '경기'),
    ('이영미', 20, '강원'),
    ('박진수', 25, '전라'),
    ('최지수', 31, '충청'),
    ('성요한', 28, '경상');

-- 특정 번호 정보 수정하기
UPDATE classmates
SET name='김철수한무두루미',
    age = '21',
    address='제주도'
WHERE rowid=2;

UPDATE classmates
SET name='오징어',
    age = '27',
    address='독도'
WHERE rowid=3;

DELETE FROM classmates WHERE rowid=5;
-- 몇번 데이터 삭제하기
SELECT rowid, * FROM classmates;
-- 삭제된것 확인하기
DELETE FROM classmates WHERE name LIKE '%한';
-- 이름에 특정 글자가 들어가면 삭제하기
DELETE FROM classmates;
-- 테이블을 지우는 것이 아니라 테이블 안의 내용 전체를 날리는 방법
```

## 데이터베이스 정규형(Datebase Normalization)

- 데이터베이스를 구조화 하는 방법론
- 데이터의 중복을 최소화하고 일관성과 무경성을 보장하기 위함
- 데이터의 구조를 더 좋은 구조로 바꾸는 것
- [Database normalization - Wikipedia](https://en.wikipedia.org/wiki/Database_normalization)
- 관계형 데이터베이스의 경우 6개의 정규형이 있다.

- 제 1 정규형
    - 하나의 속성에는 값이 하나만 들어가야한다.
- 제 2 정규형
    - 테이블의 기본키에 종속되지 않는 컬럼은 테이블이 분리되어야 한다.
    - 테이블과 관련 없는 정보는 분리한다.
- 제 3 정규형
    - 다른 속성에 의존하는 속성은 따로 분리할 것
    

### JOIN

- 테이블이 여러 개로 나누어 진다.
- SELECT  * FROM articles, users;
- CROSS JOIN
    - 요즘 데이터가 너무 많아서 보통 쓰지는 않는다.
- SELECT  * FROM articles, users WHERE articles.userid=users.rowid;

- Join : 두 개 이상의 테이블에서 데이터를 가져와 결합하는 것
    - CROSS JOIN : 모든 조합 출력
    - INNER JOIN  : 두 테이블에서 일치하는 데이터만 결과 출력
    - LEFT JOIN : 왼쪽 테이블의 데이터를 기준으로 오른쪽 데이터 결합, 없으면 NULL
    - RIGHT JOIN : 오른쪽 테이블의 데이터를 기준으로 왼쪽 데이터 결합, 없으면 NULL
    - FULL OUTER JOIN

```sql
CREATE TABLE articles (
    title TEXT,
    content TEXT,
    user_id INTEGER
);

CREATE TABLE users (
    name TEXT,
    role_id INTEGER
);

CREATE TABLE roles (
    role TEXT
);
```

```sql
SELECT * FROM articles;
SELECT * FROM users;
SELECT * FROM roles;

SELECT * FROM articles, users;
SELECT articles.rowid, title, content, name
FROM articles, users
WHERE articles.user_id = users.rowid;

SELECT articles.rowid, title, content, name
FROM
  articles INNER JOIN users
  ON articles.users_id = users.rowid

WHERE users.name LIKE '%e%';

SELECT *
FROM 
  users INNER JOIN roles
  ON users.role_id = roles.rowid
WHERE roles.role = 'student';

-- articles 중 users가 role이 student인 레코드만 반환하는 SELECT

SELECT title, content, name, role
FROM
  articles INNER JOIN (
  SELECT 
  
    users.rowid as user_id,
    users.name,
    roles.role
  FROM
    users INNER JOIN roles
    ON users.role_id = roles.rowid
  
  WHERE roles.role = 'student') table_b
  ON articles.user_id = table_b.user_id
```

```sql
INSERT INTO articles VALUES
    ('제목1','내용1',1),
    ('제목2','내용2',2),
    ('제목3','내용3',3);

INSERT INTO users VALUES
    ('aiden',1),
    ('ken',3),
    ('lynda',3);

INSERT INTO roles VALUES
    ('admin'),
    ('staff'),
    ('student');
```

```sql
INSERT INTO articles
VALUES
    ('제목4', '내용4', 4),
    ('제목5', '내용5', 5),
    ('제목6', '내용6', 6),
    ('제목7', '내용7', 7),
    ('제목8', '내용8', 8),
    ('제목9', '내용9', 9),
    ('제목10', '내용10', 10);

INSERT INTO users
VALUES
    ('sophia', 2),
    ('beemo', 1),
    ('feel', 3),
    ('coco', 2);

DELETE FROM articles WHERE title IN (
    '제목4',
    '제목6',
    '제목7',
    '제목8'
);

-----------------------------------------
SELECT * FROM articles;
-----------------------------------------

SELECT *
FROM
    articles INNER JOIN users
    ON articles.user_id = users.rowid;

SELECT *
FROM
    articles LEFT OUTER JOIN users
    ON articles.user_id = users.rowid;

SELECT *
FROM 
    users LEFT JOIN articles
    ON user.rowid = articles.user_id;
```