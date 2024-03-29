# DataBase
- 데이터 베이스에 데이터를 어떻게 입력하고, 어떻게 출력하는가   
### Database의 정의 
체계화된 데이터의 모임  
- 여러 사람이 공유하고 사용할 목적으로 통합 관리되는 정보의 집합  
- 검색, 구조화 같은 작업을 보다 쉽게 하기 위해 조직화된 데이터를 수집하는 저장 시스템 
    - 내용을 고도로 구조화함으로써 검색과 갱신의 효율화를 꾀함
    - 자료 파일을 조직적으로 통합하여 자료 항목의 중복을 없애고 구조화하여 기억시켜 놓은 자료의 집합체
- Database를 조작하는 프로그램 = DBMS(Database Management System)
    - Oracle, MySQL, SQLite... 
    - DBMS에서 Database를 조작하기 위해 사용하는 언어 : SQL  
- 웹 개발에서 대부분의 데이터베이스는 '관계형 데이터베이스 관리 시스템(RDBMS)'를 사용하여 SQL로 데이터와 프로그래밍을 구성

### RDB
- Relational Database(관계형 데이터베이스)
- 데이터를 테이블, 행,, 열 등으로 나누어 구조화하는 방식
- 자료를 여러 테이블로 나누어 관리, 테이블 간의 관계를 설정하여 여러 데이터를 쉽게 조작할 수 있음 
- SQL을 사용하여 데이터를 조회하고 조작  
![테이블간 관계 설정 예시](./relation%20settiing.png)

#### RDB 기본 구조
1. 스키마
    - 테이블의 구조(structure)
    - 데이터 베이스에서 자료의 구조, 표현 방법, 관계 등 전반적인 `명세`를 기술한 것
2. 테이블 
    - 필드와 레코드르 사용하여 조직된 데이터 요소들의 집합
    - 관계(relation)
    1. 필드(field)
        - 속성, 컬럼(Column)
    2. 레코드(record) : 테이블의 데이터는 레코드에 저장됨
        - 튜플, 행(Row)
    3. 기본 키(Primary Key, PK)
        - 각 레코드의 고유한 값
        - 각각의 데이터를 구분할 수 있는 고윳값
        - 다른 항목과 절대 중복될 수 없는 `단일 값`(unique)

### RDBMS(Relational Database Management System, 관계형 데이터 베이스 관리 시스템)
관계형 데이터 베이스를 만들고 업데이트하고 관리하는 데에 사용하는 프로그램  
- SQLite, MySQL, PostgreSQL, Microsoft SQL Server, Oracle Database ... 

# SQL
#### SQL이란
Structured Query Language  
- 데이터베이스와 상호작용하는 방법
- RDBMS의 `데이터를 관리`하기 위해 설계된 `특수` 목적의 프로그래밍 언어
- RDBMS에서 데이터베이스 스키마를 생성 및 수정할 수 있으며, 테이블에서의 자료를 검색 및 관리할 수 있음 
- 데이터베이스 객체에 대한 처리를 관리하거나 접근권한을 설정하여 허가된 사용자만 RDBMS를 관리할 수 있도록 할 수 있음 
- 많은 데이터베이스 관련 프로그램들이 SQL을 표준으로 함

#### SQL COMMANDS
- DDL Data Definition Language 데이터 정의 언어
    - 관계형 데이터베이스 구조(테이블, 스키마)를 정의하기 위한 언어
    - CREATE, DROP, ALTER
- DML Data Manipulation Language 데이터 조작 언어 
    - 데이터를 조작하기 위한 명령어
    - INSERT, SELECT, UPDATE, DELETE
- DCL Data Control Language 데이터 제어 언어
    - 데이터의 보안, 수행제어, 사용자 권한 부여 등을 정의하기 위한 언어
    - GRANT, REVOKE, COMMIT, ROLLBACK
    - SQLite는 파일로 관리되는 DB이기 때문에 SQL을 이용한 접근제한을 지원하지 않고  운영체제의 파일 접근 권한으로만 제어가능(GRANT, REVOKE 지원 X)

#### SQL SYNTAX
```sql
-- SQL Syntax 예시
SELECT column_name FROM table_name;
```
모든 SQL문(statement)은 SELECT, UPDATE, INSERT 같은 키워드로 시작하고, 하나의 statement는 세미콜론`;`으로 끝남  
SQL 키워드는 대소문자를 구분하지 않으나 `대문자`로 작성하는 것을 권장  
주석을 `--` 하이픈 2개로 시작함  

> [SELECT statement]  
>
> `SELECT column_name FROM table_name` 
> - 위 SELECT문은 2개의 Clause로 구분됨 
>   - SELECT column_name / FROM table_name
> - Statement(문)
>   - 독립적으로 실행할 수 있는 완전한 코드 조각
>   - statement는 clause로 구성됨  
> - Clause(절)
>   - statement의 하위단위

# DDL Data Definition Language 데이터 정의 언어
##### 사전 준비
1. 데이터베이스 mydb.sqlite3 파일 생성
2. DDL.sql 파일 생성
3. vscode 실행후 DDL.sql파일 화면에서 마우스 우측 클릭 후 Use Database 선택

---
- SQL 데이터 정의 언어를 사용하여 테이블 데이터 베이스 개체를 만드는 방법을 학습
- CREATE(생성), ALTER(수정), DROP(삭제)
## CREATE TABLE
Create a new table in database  
```sql
CREATE TABLE table_name(
    -- 컬럼 정의
    column1 data_type constraints,
    column2 data_type constraints,
    column3 data_type constraints,
);
```
```sql
-- 예시
CREATE TABLE contacts (
  name TEXT NOT NULL,
  age INTEGER NOT NULL,
  email TEXT NOT NULL UNIQUE
);
```
- Query 실행하기   
실행하고자하는 Query문에 커서를 두고 마우스 우측 버튼 클릭 - `Run Selected Query` 선택
- id column은 사용자가 직접 기본 키 역할의 컬럼을 정의하지 않으면 자동으로 `rowid`라는 컬럼이 생성됨  

### SQLite Data Types 
1. **NULL**
Null value  
정보가 없거나 알 수 없음(missing information or unknown)
2. **INTEGER**
정수  
크기에 따라 0, 1, 2, 4, 6, 8바이트와 같은 가변의 크기를 가짐
3. **REAL**
실수  
8바이트 부동소수점을 사용하는 10진수 값이 있는 실수
4. **TEXT**
문자 데이터 
5. **BLOB** Binary Large Object  
입력된 그대로 저장된 데이터 덩어리  
바이너리 등 멀티미디어 파일(이미지 등)

>[참고]  
> SQLite에는 별도로 Boolean타입이 없음  
> 대신 0(False) or 1(True)로 저장됨

##### Binary Data
데이터 저장과 처리를 목적으로 0과 1의 이진 형식으로 인코딩된 파일  
기본적으로 컴퓨터의 모든 파일은 binary data이지만 필요에 따라서 text type 등으로 변형하여 사용하는 것

#### 데이터 타입 결정 
- 값에 둘러싸는 따옴표와 소수점 혹은 지수가 없으면 **INTEGER**
- 값이 작은 따옴표나 큰따옴표로 묶이면 **TEXT**
- 값에 따옴표나 소수점, 지수가 없으면 **REAL**
- 값이 따옴표없이 NULL이면 **NULL**

#### SQLite Data types의 특징 
- SQLite는 다른 모든 SQL 데이터베이스 엔진의 정적이고 엄격한 타입(static, rigid typing)이 아닌 `동적 타입 시스템(dynamic type system)`을 사용 
- 컬럼에 선언된 데이터 타입에 의하지 않고 `컬럼에 저장된 값에 따라 데이터 타입이 결정`됨
- 테이블 생성할 때에 컬럼에 대해 특정 데이터 타입을 선언하지 않아도 됨 
- SQLite의 동적 타입 시스템을 사용하면 기존의 엄격하게 타입이 지정된 데이터베이스에서는 불가능한 작업을 유연하게 할 수 있음 
- 정적 타입 시스템이 지정된 데이터베이스에서 작동하는 SQL문이 SQLite에서는 동일한 방식으로 작동함 
- but, 다른 데이터베이스와의 `호환성 문제`가 있으므로 테이블 생성시 `데이터 타입을 지정하는 것을 권장`
- 데이터 타입을 지정하면 SQLite는 입력된 데이터의 타입을 지정된 데이터 타입으로 변환  
![허용가능한 타입변환](./types%20allowed.png)  

#### Type Affinity 타입 선호도 
특정 컬럼에 저장된 데이터에 권장되는 타입  
데이터 타입 작성 시 SQLite의 5가지 데이터 타입이 아닌 다른 데이터 타입을 선언한다면 내부적으로 각 타입의 지정된 선호도에 따라 5가지 선호도로 인식됨  
1. INTEGER
2. TEXT
3. BLOB
4. REAL
5. NUMERIC

- 타입 선호도 존재 이유  
: 다른 데이터베이스 엔진 간의 호환성을 최대화  
: 정적이고 엄격한 타입을 사용하는 데이터베이스의 SQL문을 SQLite에서도 작동하게 하기 위함 

## Constraints
입력하는 자료에 대해 제약을 정함  
제약에 맞지 않다면 입력이 거부됨 
사용자가 원하는 조건의 데이터만 유지하기 위한, 데이터의 무결성을 유지하기 위한 보편적인 방법으로 데이터의 특정 컬럼에 설정하는 제약 

> [무결성]  
> 데이터 베이스 내의 데이터에 대한 정확성, 일관성을 보장하기 위해 데이터 변경 혹은 수정 시 여러 제한을 두어 데이터의 정확성을 보증하는 것  
> 데이터베이스에 저장된 데이터의 무결성을 보장하고 데이터베이스의 상태를 일관되게 유지하는 것이 목적임  

### Constraints 종류
1. NOT NULL  
컬럼이 NULL값을 허용하지 않도록 지정  
기본적으로 테이블의 모든 컬럼은 NOT NULL 제약 조건을 명시로 거는 경우를 제외하고는 NULL값을 허용함  
2. UNIQUE  
컬럼의 모든 값이 서로 구별되거나 고유한 값이 되도록 함  
3. PRIMARY KEY  
테이블에서 행의 고유성을 식별하는 데에 사용되는 컬럼  
각 테이블에는 하나의 기본키만 있음  
암시적으로 NOT NULL 제약 조건이 포함되어 있음  
**INTEGER 타입에만 사용가능**(INT, BIGINT 사용 불가)
```sql
CREATE TABLE table_name(
    id INTEGER PRIMARY KEY,
)
```
4. AUTOINCREMENT  
사용되지 않은 값이나 이전에 삭제된 행의 값을 재사용하는 것을 방지  
INTEGER PRIMARY KEY 다음에 AUTOINCREMENT를 작성하면 해당 rowid를 재사용하지 못하도록 함  
```sql
CREATE TABLE table_name(
    id INTEGER PRIMARY KEY AUTOINCREMENT
)
```
> Django가 테이블 생성시 id컬럼에 기본적으로 사용하는 제약조건  

#### rowid의 특징
- 테이블 생성할 때마다 rowid라는 암시적 자동 증가 컬럼이 자동으로 생성됨 
- 테이블의 행을 고유하게 식별하는 64비트 부호있는 정수 값
- 테이블에 새 행을 삽입할 때마다 자동으로 정수값을 할당 
    - 값은 1부터 시작
    - 데이터 삽입시에 rowid 혹은 INTEGER PRIMARY KEY 컬럼에 명시적으로 값이 지정되지 않은 경우, SQLite에서는 테이블에서 가장 큰 rowid보다 하나 큰 다음 순차 정수를 할당함  
    (AUTOINCREMENT와 무관)
- INTEGER PRIMARY KEY키워드를 가진 컬럼을 직접 만들면 이 컬럼은 rowid컬럼의 별칭(alias)가 됨  
    - 새로운 컬럼 이름으로도, rowid로도 접근이 가능함
- 데이터가 최대값에 도달하고 새 행을 삽입하려고 하면 SQLite는 사용되지 않은 정수를 찾아서 사용함 (Limits in SQLite)
- 만일 SQLite가 사용되지 않은 정수를 찾을 수 없으면 SQLITE_FULL에러가 발생 
    - 또한 일부 행을 삭제하고 새 행을 삽입하면 SQLite는 삭제된 행에서 rowid값을 재사용하려고 시도 (AUTOINCREMENT 제약조건이 없다면)

## ALTER TABLE
Modify the structure of an existing table  
기존 테이블의 구조를 수정(변경)  
```sql
-- 1. Rename a table(테이블 이름 변경)
ALTER TABLE table_name RENAME TO new_table_name;
-- 2. Rename a column(컬럼 이름 변경)
ALTER TABLE table_name RENAME COLUMN column_name TO new_column_name;
-- 3. Add a new column to a table(테이블에 컬럼 추가)
ALTER TABLE table_name ADD COLUMN column_definition;
-- 4. Delete a column (컬럼 삭제)
ALTER TABLE table_name DROP COLUMN column_name;
```
#### ALTER TABLE ADD COLUMN  
Add a new column to a table 
```sql
ALTER TABLE table_name 
ADD COLUMN column_name TEXT(/INTEGER/...) NOT NULL(constraints);
```

- 만약 기존 데이터가 있을 경우, 에러 발생  
`Cannot add NOT NULL column with default value NULL`
- 이전에 이미 저장된 데이터들은 새롭게 추가되는 컬럼에 값이 없기 때문에 NULL이 작성됨  
- 새로 추가되는 컬럼에 NOT NULL 제약조건이 있기 때문에 기본 값 없이는 추가될 수 없다는 에러가 발생하게 됨
- **DEFAULT 제약조건을 사용하여 해결**
    - column_name 컬럼이 추가되면서 기존에 있던 데이터들의 column_name 컬럼 값은 'no column_name'이 됨
```sql
ALTER TABLE table_name 
ADD COLUMN column_name TEXT NOT NULL DEFAULT 'no column_name';
-- e.g.) ALTER TABLE new_contacts  ADD COLUMN address TEXT NOT NULL DEFAULT 'no address';
```
> [참고] DEFAULT 제약조건
> - column 제약조건 중 하나
> - 데이터를 추가할 때 값을 생략할 시에 기본 값을 설정할 수 있음

#### ALTER TABLE DROP COLUMN 
Delete a column
```sql
ALTER TABLE table_name DROP COLUMN column_name;
```
- 삭제하지 못하는 경우  
    - 컬럼이 다른 부분에서 참조되는 경우 : `FOREIGN KEY(외래 키)제약조건`에서 사용되는 경우
    - `PRIMARY KEY`인 경우
    - `UNIQUE 제약조건`이 있는 경우
        - Cannot drop UNIQUE column: "email"


## DROP TABLE
Remove a table from the database  
```sql
DROP TABLE table_name;
```
존재하지 않는 테이블을 제거하면 SQLite에서 오류 발생 `no such table: table_name`
- 한 번에 하나의 테이블만 삭제할 수 있음
- 여러 테이블을 제거하려면 여러 DROP TABLE문을 실행하여야 함
- [**주의**] DROP TABLE문은 실행취소 혹은 복구할 수 없음  

# DML
DML을 통해 데이터 조작하기(CRUD)
- INSERT, SELECT, UPDATE, DELETE
##### sqlite3 사용하기
```terminal
<!-- 1. 시작하기 -->
$ sqlite3
<!-- 2. 데이터베이스 파일 열기 -->
.open mydb.sqlite3 
<!-- 1-1. sqlite3 종료하기 -->
.exit
<!-- 3. 모드mode를 csv로 설정 -->
.mode csv
<!-- 4. cvs 데이터를 테이블로 불러오기 -->
.import users.cvs users
```

## SELECT
특정 테이블에서 데이터를 조회하기 위해 사용   
Query data from table
```sql
SELECT column1, column2 FROM table_name;
```
1. SELECT 절에서 컬럼 또는 쉼표로 구분된 컬럼 목록을 지정
2. FROM 절(clause)에서 데이터를 가져올 테이블을 지정  
---
- 이름과 나이 조회하기
```sql
SELECT first_name, age FROM users;
```
- 전체 데이터 조회하기 
```sql
SELECT * FROM users;
```
- rowid는 전체 데이터 조회 시 조회되지 않으므로 별도로 명시해주어야 한다.  
```sql
SELECT rowid, first_name FROM users;
```

### Sorting rows 레코드 정렬
#### `ORDER BY` clause  
Sort a result set of a query  
SELECT 문제 추가하여 결과를 정렬  
ORDER BY 절은 FROM 절 뒤에 위치함   
하나 이상의 컬럼을 기준으로 결과를 오름차순 혹은 내림차순으로 정렬할 수 있음   
- ASC : 오름차순(기본값)
- DESC : 내림차순
```sql
SELECT select_list FROM table_name 
ORDER BY column1 ASC, column2 DESC;
```
---
- 이름과 나이를 나이가 어린 순으로 조회하기
```sql
SELECT first_name, age FROM users ORDER BY age ASC;
SELECT first_name, age FROM users ORDER BY age;
```
- 이름, 나이, 계좌 잔고를 나이가 어린 순으로, 만약 같은 나이라면 계좌 잔고가 많은 순서대로 정렬하기 
```sql
SELECT first_name, age, balance FROM users 
ORDER BY age ASC, balance DESC;
```

> [참고]**Sorting NULLs**
> - NULL의 정렬방식
> - 정렬과 관련하여 SQLite는 NULL을 다른 값보다 작은 값으로 간주함  
> - ASC를 사용하는 경우, 결과의 시작에 NULL이 표시되고, DESC를 사용하는 경우, 결과의 끝에 NULL이 표시됨

### Filtering data
#### SELECT DISTINCT clause
Remove duplicate rows in the result  
조회된 결과에서 중복 제거  
DISTINCT절은 SELECT에서 선택적으로 사용할 수 있는 절  
```sql
SELECT DISTINCT select_list FROM table_name;
```
- DISTINCT 절은 SELECT 키워드 바로 뒤에 나타나야 함  
- DISTINCT 키워드 뒤에 컬럼 또는 컬럼 목록을 작성 

--- 
- 모든 지역 조회하기
```sql
SELECT country FROM users;
```
- 중복 없이 모든 지역 조회하기
```sql
SELECT DISTINCT country FROM users;
```
- 지역순으로 오름차순 정렬하여 중복 없이 모든 지역 조회하기
```sql
SELECT DISTINCT country FROM users ORDER BY country;
```
- 이름과 지역을 중복없이 모든 이름과 지역 조회하기
    - 각 컬럼의 중복을 따로 계산하는 것이 아니라, 두 컬럼을 하나의 집합으로 보고 중복을 제거함
```sql
SELECT DISTINCT first_name, country FROM users;
```
- 이름과 지역을 중복없이 지역순으로 내림차순 정렬하여 조회하기
```sql
SELECT DISTINCT first_name, country FROM users 
ORDER BY country DESC;
```
> [참고] NULL with DISTINCT
> - SQLite는 NULL 값을 중복으로 간주
> - NULL 값이 있는 컬럼에 DISTINCT 절을 사용하면 SQLite는 NULL 값의 한 행을 유지

#### WHERE clause
Specify the search condition for rows returned by the query  
조회시 특정 검색 조건을 지정  
WHERE 절은 SELECT에서 선택적으로 사용할 수 있는 절  
FROM 절 뒤에 작성  
> SELECT 문 외에도 UPDATE 혹은 DELETE문에서도 사용할 수 있음

- WHERE 검색조건 작성 형식
```sql
left_expression COMPARISON_OPERATOR right_expression
```
```sql
-- 작성 예시
WHERE column_1 = 10  -- 10인 경우
WHERE column_2 LIKE 'Ko%'  -- Ko로 시작한느 데이터 조회
WHERE column_3 IN (1, 2)   -- 1 아니면 2
WHERE column_4 BETWEEN 10 AND 20 -- 10에서 20사이
```
- SQLite comparison operators(비교 연산자)
    - = 
    - <> or !=
    - <
    - \>
    - <=
    - =>

- SQLite logical operators(논리 연산자)
    - 일부 표현식의 truth 를 테스트할 수 있음
    - 1, 0 또는 NULL 값을 반환 
    - SQLite는 Boolean 타입을 제공하지 않으므로 0 혹은 1로 나타냄 (0 == False, 1 == True)
    - ALL, OR, ANY, AND, BETWEEN, IN, LIKE, NOT 등

---
- 나이가 30살 이상인 사람들의 이름, 나이, 계좌 잔고 조회하기
```sql
SELECT last_name, age, balance FROM users 
WHERE age >= 30;
```
- 나이가 30살 이상이고, 계좌 잔고가 50만원 초과인 사람들의 이름, 나이, 계좌 잔고 조회하기
```sql
SELECT last_name, age, balance FROM users 
WHERE age >= 30 AND balance > 500000;
```


#### LIKE operator
Query data based on pattern matching  
패턴 일치를 기반으로 데이터를 조회  
- SELECT, DELETE, UPDATE 문의 `WHERE 절에서 사용`
- 기본적으로 대소문자를 구분하지 않음  
    - `'A' LIKE 'a' --> True`

- SQLite는 패턴 구성을 위한 두 개의 wild cards를 제공  
1. `%` (percent)
    - 0개 이상의 문자가 올 수 있음
        - '영%'패턴은 영으로 시작하는 모든 문자열과 일치(영, 영미리, 영화...)
        - '%도'패턴은 도로 끝나는 모든 문자열과 일치(도, 수도, 경기도...)
        - '%강원%'패턴은 문자열에 강원이 포함되는 모든 문자열과 일치(강원도, 강원, 강원도에 살아요 등)
2. `_` (underscore)
    - 단일(1개) 문자가 있음
        - '영_'패턴은 영으로 시작하고 총 2자리인 문자열과 일치(영미, 영주, 영도 등)
        - '_도'패턴은 도로 끝나고 총 2자리인 문자열과 일치(수도, 과도 등)

- _2% : 첫번째 자리에 아무 값이 하나 있고 그 다음은 2로 시작하는 패턴(최소 2자리)
- 1_ _ _ : 1로 시작하는 4자리 패턴(반드시 4자리)
- 2 _ % _ % or 2_ _ % : 2로 시작하고 최소 3자리인 패턴(3자리 이상)

> [참고] 'wildcards' character 
> - 파일을 지정할 때, 구체적인 이름 대신 여러 파일을 동시에 지정할 목적으로 사용하는 특수기호
> - *, ? 등
> - 주로 특정한 패턴이 있는 문자열 혹은 파일을 찾거나, 긴 이름을 생략할 때 쓰임
> - 텍스트 값에서 알 수 없는 문자를 사용할 수 있는 특수 문자로, 유사하지만 동일한 데이터가 아닌 여러 항목을 찾기에 매우 편리한 문자
> - 지정된 패턴 일치를 기반으로 데이터를 수집하는 데도 도움이 될 수 있음 

---
- 이름에 '호'가 포함된 사람들의 이름과 성 조회하기
```sql
SELECT last_name, first_name FROM users 
WHERE first_name LIKE '%호%';
```
- 이름이 '준'으로 끝나는 사람들의 이름 조회하기
```sql
SELECT first_name FROM users WHERE first_name LIKE '%준';
```
- 서울 지역 전화번호를 가진 사람들의 이름과 전화번호 조회하기 
```sql
SELECT first_name, phone  FROM users WHERE phone LIKE '02-%';
```
- 나이가 20대인 사람들의 이름과 나이 조회하기
```sql
SELECT first_name, age FROM users WHERE age LIKE '2_';
```
- 전화번호의 중간 4자리가 51로 시작하는 사람들의 이름과 전화번호 조회하기
```sql
SELECT first_name, phone FROM users WHERE phone LIKE '%-51__-% ';
```

#### IN operator
Determine whether a value matches any value in a list of values  
값이 값 목록 결과에 있는 값과 일치하는지 확인  
표현식이 값 목록의 값과 일치하는지 여부에 따라 true or false를 반환  
IN 연산자의 결과를 부정하려면 `NOT IN` 연산자를 사용  

---
- 경기도 혹은 강원도에 사는 사람들의 이름과 주소 조회하기
```sql
SELECT first_name, country FROM users 
WHERE country IN ('강원도, 경기도');

SELECT first_name, country FROM users 
WHERE country = '경기도' OR country = '강원도';
```
- 경기도 혹은 강원도에 살지 않는 사람들의 이름과 주소 조회하기
```sql
SELECT first_name, country FROM users
WHERE country NOT IN ('강원도', '경기도');
```
#### BETWEEN operator
Test whether a value is in a range of values  
값이 값 범위에 있는지 테스트  
값이 지정된 범위 안에 있으면 true 리턴  
SELECT, DELETE, UPDATE 문의 WHERE 절에서 사용할 수 있음   
BETWEEN 연산자의 결과를 부정하려면 `NOT BETWEEN` 연산자를 사용  

---
- 나이가 20살 이상 30살 이하인 사람들의 나이와 이름 조회하기
```sql
SELECT first_name, age FROM users 
WHERE age BETWEEN 20 and 30;

SELECT first_name, age FROM users 
WHERE age >= 20 AND age <= 30;
```
- 나이가 20살 이상 30살 이하가 아닌 사람들의 나이와 이름 조회하기
```sql
SELECT first_name, age FROM users 
WHERE age NOT BETWEEN 20 and 30;

SELECT first_name, age FROM users 
WHERE age < 20 OR age > 30;
```
#### LIMIT clause
Constraint the number of rows returned by a query  
쿼리에서 반환되는 행의 수를 제한  
값이 지정된 범위 안에 있으면 true 리턴    
SELECT문에서 선택적으로 사용할 수 있음     
row_count는 반환되는 행의 수를 의미함  
```sql
SELECT column_list FROM table_name LIMIT row_count;
```

---
- 첫번째부터 열번째 데이터까지 rowid와 이름 조회하기
```sql
SELECT rowid, first_name FROM users LIMIT 10;
```
- 계좌잔고가 제일 많은 순으로 상위 10명의 이름과 계좌잔고 조회하기
```sql
SELECT first_name, balance FROM users 
ORDER BY balance DESC LIMIT 10;
```
- 나이가 가장 어린 순으로 5명의 이름과 나이 조회하기
```sql
SELECT first_name, age FROM users ORDER BY age LIMIT 5;
```

#### OFFSET keyword
- LIMIT절을 사용하면 첫번째 데이터부터 지정한 수만큼의 데이터를 받아올 수 있지만, OFFSET과 함께 사용하면 특정 지정된 위치에서부터 데이터를 조회할 수 있음 
```sql
-- 11번쨰 부터 20번쨰까지 (10개의) 데이터의 rowid와 이름 조회하기
SELECT rowid, first_name FROM users LIMIT 10 OFFSET 10;
```

#### GROUP BY clause
Make a set of summary rows from a set of rows  
특정 그룹으로 묶인 결과를 생성  
선택된 컬럼 값을 기준으로 데이터(행)들의 공통 값을 묶어서 결과로 리턴  
SELECT 문에서 선택적으로 사용 가능  
SELECT 문에서 FROM절 뒤에 작성(WHERE이 있는 경우 WHERE 뒤에)
```sql
SELECT column_1, aggregate_function(column_2)
FROM table_name
GROUP BY column_1, column_2;
```
#### Aggregate function
"집계 함수"  
값 집합의 최대값, 최소값, 평균, 합계 및 개수를 계산  
값 집합에 대한 계산을 수행하고 단일 값을 반환 (여러 행으로부터 하나의 결과값을 반환)  
SELECT문의 GROUP BY 절과 함께 사용됨  
- AVG(), COUNT(), MAX(), MIN(), SUM()
- AVG(), MAX(), MIN(), SUM()는 숫자를 기준으로만 계산이 되어지기 때문에 반드시 컬럼의 데이터 타입이 숫자`INTEGER`일 떄만 사용가능함  

---
- users 테이블의 전체 행 수 조회하기
```sql
SELECT COUNT(*) FROM users;
```
- 지역별로 몇명씩 살고 있는지 지역과 인원 조회하기
```sql
SELECT country, COUNT(*) FROM users GROUP BY country;
```
- 나이가 30살 이상인 사람들의 평균 나이 조회하기
```sql
SELECT AVG(age) FROM users WHERE age >= 30;
```

> [참고] COUNT의 참고사항 
> - 이전 쿼리에서 COUNT(), COUNT(age), COUNT(last_name) 등 어떤 컬럼을 넣어도 결과는 같음 
> - 현재 쿼리에서는 그룹화된 country를 기준으로 카운트하는 것이기 때문에 어떤 컬럼을 카운트해도 전체 개수는 동일하기 때문
> - *AS* 키워드를 통해 컬럼명을 임시로 변경하여 조회할 수 있음 
> ```sql
> SELECT last_name, COUNT(*) AS number_of_name 
> FROM users GROUP BY last_name;
> ```


## Changing Data
### INSERT Statement
Insert new rows into a table  
새 행을 테이블에 삽입  
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```
1. 먼저 INSERT INTO 키워드 뒤에 데이터를 삽입합 테이블 이름을 지정 
2. 테이블 이름 뒤에 쉼표로 구분된 컬럼 목록을 추가 (컬럼 목록을 포함하는 것이 권장)
3. VALUES 키워드 뒤에 쉼표로 구분된 값 목록을 추가 
    - 컬럼 목록을 생략하는 경우, 값 목록의 모든 컬럼에 대한 값을 지정해야 함
    - 값 목록의 개수는 컬럼 목록의 개수와 같아야 함

---
- 단일 행 삽입하기
```sql
INSERT INTO classmates (name, age, address) 
VALUES ('홍길동', 20, '강남구');

INSERT INTO classmates VALUES ('홍길동', 20, '강남구');
```
- 여러 행 삽입하기
```sql
INSERT INTO classmates 
VALUES 
    ('홍길동', 20, '강남구'),
    ('홍영민', 24, '관악구'),
    ('홍상수', 33, '송파구'),
    ('홍지원', 22, '광진구');
```

### UPDATE Statement
Update existing rows in a table.  
테이블에 있는 기존 행의 데이터를 업데이트  
```sql
UPDATE table_name
SET column_1 = new_value_1,
    column_2 = new_value_2
WHERE
    search_condition;
```
1. UPDATE 절 이후 업데이트할 테이블 지정 
2. SET 절에서 테이블의 각 컬럼에 대해 새 값 설정
3. WHERE 절의 조건을 사용하여 업데이트할 행을 지정  
    - WHERE절은 선택 사항이며, `생략`하면 UPDATE 문은 테이블의 `모든 행에 있는 데이터를 수정함`
4. 선택적으로 ORDER BY 및 LIMIT 절을 사용하여 업데이트할 행의 수를 지정할 수 있음  

---
- 2번 데이터의 이름을 '김철수한무두루미', 주소를 '제주도'로 수정하기
```sql
UPDATE users 
SET first_name='김철수한무두루미', 
    address='제주도' 
WHERE rowid=2;
```

### DELETE statement
Delete rows from a table  
테이블에서 행 제거  
테이블의 한 행, 여러 행, 모든 행을 삭제할 수 있음
```sql
DELETE FROM table_name
WHERE search_condition;
```
1. DELETE FROM 키워드 뒤에 행을 제거하려는 테이블의 이름을 지정 
2. WHERE 절에 검색조건을 추가하여 제거할 행을 식별
    - WHERE 절은 선택사항이며, `생략`하면 DELETE문은 `테이블의 모든 행을 삭제`
3. 선택적으로 ORDER BY 및 LIMIT 절을 사용하여 삭제할 행의 수를 지정할 수 있음  

---
- 5번 데이터 삭제하기
```sql
DELETE FROM users WHERE rowid=5;
```
- 삭제된 것 확인하기
```sql
SELECT rowid, * FROM users;
```
- 이름에 '영'이 포함되는 데이터 삭제하기 
```sql
DELETE FROM users WHERE first_name LIKE '%영%' OR last_name LIKE '%영%';
```
- 테이블의 모든 데이터 삭제하기
```sql
DELETE FROM users;
```