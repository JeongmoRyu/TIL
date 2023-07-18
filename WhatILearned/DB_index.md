# DB index

- 추가적인 쓰기 작업과 저장 공간을 활용하여 DB 테이블의 검색 속도를 향상시키기 위한 자료 구조
- 테이블에 있는 데이터를 빠르게 검색하기 위해 생성되는 객체

## 장점

- 성능의 향상
- 시스템 부하 감소

![imgae](https://th.bing.com/th/id/OIP.cplaYYaSVcK4QgnsFpgSAQAAAA?pid=ImgDet&rs=1)

## 사용시 주의점

- index 관리를 위한 추가 작업
    - insert
    - delete
    - update
- 추가 저장 공간 필요
- 잘 못 사용했을 경우 성능 저하 가능성 존재

## 활용

- 규모가 작지 않은 테이블
- insert, delete, update 가 자주 발생하지 않는 칼럼
- join, where, order by 자주 사용하는 칼럼
- 데이터의 중복도가 낮은 칼럼

단일 인덱스 vs 다중 컬럼 인덱스 vs query문

### 설계하는 방법

```dart
- 한 테이블 당 3-5개가 적당
- 자주 사용하는 컬럼
- 고유한 값 위주
- 카디널리티가 높을 수록 좋다. (한 컬럼이 갖고 있는 중복의 정도가 낮을 수록 좋다.)
- Index 키의 크기는 되도록 작게 설계
- PK, Join의 연결고리가 되는 칼럼
- 단일 인덱스 여러 개 보다 다중 컬럼 Index 생성 고려
- update가 빈번하지 않은 컬럼
- join시 자주 사용되는 컬럼
- index를 생성할 떄 가장 효율적인 자료형은 정수형 자료(가변적 자료는 비효율적)
```

## Index 생성 방법

- **이미 인덱스가 존재하는 컬럼/옵션의 경우 오류(ORA-01408)가 발생할 수 있습니다.**

```dart
*ORA-01408: 열 목록에 인덱스 작성되어 있음*
```

- Basic

```dart
- 생성
CREATE TABLE t1 ( c1 INT, c2 INT, c3 INT NOT NULL )
```

- **B-TREE, NON UNIQUE**

```dart
create index INDEX
on TableName(Column);
```

- **B-TREE, NON UNIQUE, COMPISITE**
    - CREATE INDEX 문을 통해 여러 개의 인덱스를 생성할 수 있다.

```dart
create index INDEX
on TableName(ColumnA, ColumnB);
```

****

****

- **UNIQUE**
    - 고유 값 지정

```dart
create unique index INDEX
on TableName(Column);
```

- **DESCENDING**
    - 내림차순

```dart
create index INDEX
on TableName(Column desc);
```

****

- **Functin Based**

```dart
create index INDEX
on TableName(expression);
```

- **BITMAP**
    - 각 구분에 대해 비트맵(0,1)을 사용하여 인덱스를 생성합니다.
    - discrete, binomial, category, categorical variable → Column

```dart
create bitmap index INDEX
on TableName(Column)
```