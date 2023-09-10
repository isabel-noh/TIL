# 관계형 데이터베이스 개요

**DBMS(Database Management System)**

## **RDBMS(Relational Database Management System)**

- **정규화**를 통한 합리적인 테이블 모델링을 통해 **이상 현상을 제거**하고 **데이터 중복을 피할** 수 있으며, **동시성 관리, 병행 제어**를 통해 많은 사용자들이 동시에 데이터를 공유 및 조작할 수 있는 기능을 제공하였다.

- 메타 데이터를 총괄 관리할 수 있기 때문에, 데이터의 성격, 속성 등을 체계화할 수 있고, **데이터 표준화**를 통한 데이터 품질을 확보할 수 있다.

- 보안을 통해 데이터 무결성을 보장할 수 있다.

## **SQL(Structured Query Language)**

: 관계형 데이터베이스에서 ㄷ데이터 정의 , 데이터 조작, 데이터 제어를 하기 위해 사용하는 언어

ANSI/ISO 표준을 따름

| 명령어 종류        | 명령어  | 설명                                                                  |
| ------------------ | ------- | --------------------------------------------------------------------- |
| 데이터 조작어(DML) | SELECT  | 데이터베이스에 들어있는 데이터를 조회하거나 검색하는 명령어, RETRIEVE |
|                    | INSERT, |

UPDATE,
DELETE | 데이터베이스의 테이블에 들어있는 데이터에 변형을 가하는 명령어 |
| 데이터 정의어(DDL) | CREATE,
ALTER,
DROP,
TRUNCATE | 테이블과 같은 데이터 구조를 정의하는 명령어 |
| 데이터 제어어(DCL) | GRANT,
REVOKE | 데이터베이스에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 명령어 |
| 트랜잭션 제어어(TCL) | COMMIT,
ROLLBACK | 논리적인 작업의 단위를 묶어서 DML에 의해 조작된 결과를 작업단위(트랜잭션)별로 제어하는 명령어 |

## **TABLE**

- 데이터는 관계형 데이터베이스의 기본단위인 테이블형태로 저장된다

- 테이블은 반드시 하나 이상의 컬럼을 가진다

| 용어                  | 설명                                                                  |
| --------------------- | --------------------------------------------------------------------- |
| 테이블                | 행과 컬럼 2차원 구조로 된 데이터의 저장 장소                          |
| 컬럼/열               | 테이블에서 세로 방향으로 이루어진 하나 하나의 특정 속성 - 하나의 속성 |
| 로우/행/튜플/인스턴스 | 테이블에서 가로 방향으로 이루어진 연결된 데이터                       |
| 필드                  | 칼럼과 행이 겹치는 하나의 공간                                        |

**정규형**

- 테이블을 분할하여 데이터의 불필요한 중복을 줄이는 것

- 데이터의 정합성 확보와 데이터 입력/수정/삭제 시 발생할 수 있는 이상현상을 방지하기 위해

**Primary Key 기본 키**

- 각 행을 한가지 의미로 특정할 수 있는 한 개 이상의 컬럼

**Foreign Key 외래 키**

- 다른 테이블의 기본 키로 사용되면서 테이블과의 관계를 연결하는 역할을 하는 컬럼

## **ERD(Entity Relationship Diagram)**

구성요소 : **엔터티, 관계, 속성**

# DDL

Data Definition Language

## **데이터의 유형**

특정 칼럼을 정의할 때 선언한 데이터의 유형은 그 컬럼이 받아들일 수 있는 자료의 유형을 규정

| 데이터 유형  | 설명                                  |
| ------------ | ------------------------------------- |
| CHARACTER(s) | - 고정 길이 문자열 정보 (CHAR로 표현) |

- s는 기본 1바이트, 최대 길이 Oracle 2000바이트, SQL 8000바이트
- s만큼 최대 길이를 가지고 고정길이를 가지고 있으므로, 할당된변수 값의 길이가 s보다 작을 경우에는 그 차이만큼 공간으로 채워진다.
- ‘AA’ == ‘AA ‘ |
  | VARCHAR(s) | - CHARACTER VARYING
- 가변길이 문자열 정보, Oracle - VARCHAR2, SQL - VARCHAR
- s는 최소 길이 1바이트, 최대 길이 Oracle 4000바이트, SQL 8000바이트
- s만큼의 최대 길이를 갖지만 길이 조정이 가능하기 때문에 할당된 변수값의 바이트만 적용된다. (Limit 개념)
- ‘AA’ != ‘AA ‘ |
  | NUMERIC | - 정수, 실수 등 숫자 정보를(Oracle- NUMBER, SQL은 10가지 이상)
- Oracle은 처음에 전체 자리 수를 지정하고, 다음 소수 부분의 자리 수를 지정한다. |
  | DATETIME(DATE) | - 날짜와 시각 정보 (Oracle - DATE, SQL - DATETIME)
- Oracle - 1초 단위, SQL은 3.33ms 단위 관리 |

### CHAR vs VARCHAR

- CHAR은 문자열을 비교할 때 공백을 채워서 비교하는 방법을 시행
  → 끝의 공백만 다른 문자열은 같다고 판단
- VARCHAR은 맨 처음부터 한 문자씩 비교하고 공백도 하나의 문자로 취급하므로 끝의 공백이 다르면 다른 문자로 판단

## CREATE TABLE

테이블 생성을 위해서는 해당 테이블에 입력될 데이터를 정의하고, 정의한 데이터를 어떠한 데이터 유형으로 선언할 것인지를 결정해야

### 테이블과 컬럼의 정의

테이블 간의 관계는 기본키와 외부키를 활용하여 설정한다.

### CREATE TABLE

```sql
CREATE TABLE 테이블_이름 (컬럼이름 DATATYPE [DEFAULT 형식], ...);
```

**테이블 생성 시 주의 규칙**

- 테이블명은 객체를 의미할 수 있는 적절한 이름을 사용한다
- 가능한 단수형
- 테이블 명은 다른 테이블의 이름과 중복되지 않아야 한다
- 한 테이블 내에서는 컬럼명이 중복 X
- 테이블명을 지정하고 각 컬럼들은 괄호`()`로 묶어 지정
- 각 컬럼은 콤마 `,` 로 구분되고, 테이블의 생성문은 항상 세미콜론 `;` 으로 끝남
- 컬럼에 대해서는 다른 테이블 까지 고려하여 DB 내에서는 일관성 있게 사용하는 것이 좋음
- 컬럼 뒤에 데이터 유형은 필수
- 테이블명과 컬럼명은 반드시 문자로 시작해야하고, 벤더 별로 길이에 대한 한계 있음
- 예약어는 쓸 수 없음
- A-Z, a-z, 0-9, \_, $, # 만 허용
- 대/소문자는 구분하지 않음(기본적으로 테이블이나 컬럼명은 대문자)
- DATETIME은 크기 지정X
- 문자 데이터 유형은 반드시 최대 길이를 표시해야
- 마지막 컬럼은 콤마X
- 컬럼에 대한 제약 조건이 있으면 `CONSTRAINT` 를 이용하여 추가할 수 있음
- ```sql
  CREATE TABLE PLAYER
  	(PLAYER_ID CHAR(7) NOT NULL, PLAYER_NAME VARCHAR(20) NOT NULL,
  	TEAM_ID CHAR(3)[NOT NULL],
  	E_PLAYER_NAME VARCHAR(40), NICKNAME VARCHAR(30), JOIN_YYYY CHAR(4),
  	POSITION VARCHAR(10), BACK_NO TINYINT, NATION VARCHAR(20), BIRTH_DATE DATE,
  	SOLAR CHAR(1), HEIGHT SMALLINT, WEIGHT SMALLINT,
  	CONSTRAINT PLAYER_PK PRIMARY KEY (PLAYER_ID),
  	CONSTRAINT PLAYER_FK FOREIGN KEY (TEAM_ID) REFERENCES TEAM(TEAM_ID)
  );
  ```

### 제약조건(CONSTRAINT)

데이터의 무결성을 유지하기 위해 테이블의 특정 칼럼에 설정하는 제약

**제약 조건의 종류**

| 구분        | 설명                                                               |
| ----------- | ------------------------------------------------------------------ |
| PRIMARY KEY | - 테이블에 저장된 행 데이터를 고유하게 식별하기 위한 기본키를 정의 |

- 기본키 제약을 정의하면 DBMS는 자동으로 UNIQUE 인덱스를 생성하며, 기본키 컬럼에는 NULL을 입력할 수 없다
- 기본키 제약 = 고유키 제약 && NOT NULL 제약 |
  | UNIQUE KEY | - 테이블에 저장된 행 데이터를 고유하게 식별하기 위한 고유키를 정의
- NULL은 고유키 제약의 대상이 아니므로, NULL이 있어도 됨 |
  | NOT NULL | - NULL 값 입력 금지
- DEFAULT에서는 NULL을 허가하고 있지만, 이 제약을 함으로써 값 입력이 필수가 된다 |
  | CHECK | - 입력할 수 있는 값의 범위를 제한
- TRUE or FALSE로 평가할 수 있는 논리식을 지정 |
  | FOREIGN KEY | - RDBMS에서 테이블 간의 관계를 정의하기 위해 기본키를 다른 테이블의 외래키로 복사하는 경우 외래키가 생성됨
- 외래키 지정시 참조 무결성 제약 옵션을 선택할 수 있음 |

**DEFAULT의 이미**

데이터 입력시 명시된 값을 지정하지 않은 경우에 NULL이 입력되고, **DEFAULT**를 정의했다면 해당 컬럼에 NULL이 입력되지 않고 정의된 기본 값이 자동으로 입력된다

- ```sql
  CREATE TABLE TEAM(
      TEAM_ID CHAR(3) NOT NULL,
      REGION_NAME VARCHAR(8) NOT NULL,
      TEAM_NAME VARCHAR(40), NOT NULL
      E_TEAM_NAME VARCHAR(50),
      ORIG_YYY CHAR(4),
      STADIUM_ID CHAR(4) NOT NULL,
      CONSTRAINT TEAM_PK PRIMARY KEY (TEAM_ID),
      CONSTRAINT TEAM_FK FOREIGN KEY (STADIUM_ID) REFERENCES STADIUM (STADIUM_ID)
  );
  ```

### 생성된 테이블 구조 확인

아래 명령어로 테이블에 대한 정보를 확인할 수 있음

Oracle : `DESCRIBE 테이블이름;` `DESC 테이블이름;`

SQL : `sp_help 'dbo.테이블이름'`

<aside>
💡 **SELECT 문장을 통한 테이블 생성**

CTAS : Create Table ~ As Select ~ / Select ~ Into ~

주의사항 : 제약 조건만 NOT NULL만 새로운 복제 테이블에 적용되고, 기본키, 외래키, 고유키, CHECK 등의 조건은 사라진다.
제약 조건을 추가하기 위해서는 ALTER TABLE을 활용하여야 한다.

</aside>

## ALTER TABLE

변경 - 컬럼을 추가/삭제하거나 제약조건을 추가/삭제 하는 작업

### ADD COLUMN

```sql
ALTER TABLE 테이블명 ADD 추가할컬럼명 DATATYPE;
```

새롭게 추가된 컬럼은 마지막에 추가되며 컬럼 위치를 정할 수 없다.

### DROP COLUMN

테이블에서 필요없는 컬럼을 삭제(데이터가 있든지 없든지)

한 번에 하나의 컬럼만 삭제 가능

삭제 후 최소 하나 이상의 컬럼이 테이블에 존재하여야 함

삭제된 컬럼은 복구 불가능❗️

```sql
ALTER TABLE 테이블명 DROP COLUMN 삭제할컬럼명;
```

### MODIFY(ALTER) COLUMN

컬럼에 대한 정의를 변경하는 명령

테이블에 존재하는 컬럼에 대해서 ALTER TABLE 명령을 이용하여 컬럼의 데이터 유형, DEFAULT 값, NOT NULL 제약 조건에 대한 변경을 포함할 수 있음

```sql
ALTER TABLE 테이블명 MODIFY (컬렴명1 DATATYPE [DEFAULT 식 NOT NULL], 컬럼명2 DATATYPE [DEFAULT 식 NOT NULL], ... );
ALTER TABLE 테이블명 ALTER (컬렴명1 DATATYPE [DEFAULT 식 NOT NULL], 컬럼명2 DATATYPE [DEFAULT 식 NOT NULL], ... );
```

**컬럼 수정시 고려사항**

- 해당 컬럼의 크기를 늘릴 수는 있지만 줄일 수는 없음
- 해당 컬럼이 NULL 값만 가지고 있거나 테이블에 아무 행도 없으면 컬럼의 폭을 줄일 수 있음
- 해당 컬럼이 NULL 값만 있으면 데이터 유형을 변경할 수있음
- 해당 컬럼의 DEFAULT 값을 바꾸면 변경 작업 이후 발생하는 행 삽입에 대해서만 영향을 미침
- 해당 컬럼에 NULL이 없을 경우에만 NOT NULL 조건을 추가할 수 있음
- ```sql
  #Oracle
  ALTER TABLE TEAM MODIFY (ORIG_YYYY VARCHAR2(8) DEFAULT '20020129' NOT NULL);

  #SQL
  ALTER TABLE TEAM ALTER COLUMN ORIG_YYYY VARCHAR(8) NOT NULL;
  ALTER TABLE TEAM ALTER ADD CONSTRAINT DF_ORIG_YYYY DEFAULT '20020129' FOR ORIG_YYYY;
  ```

\***\*\*\*\*\*\*\***\*\*\***\*\*\*\*\*\*\***RENAME COLUMN\***\*\*\*\*\*\*\***\*\*\***\*\*\*\*\*\*\***

컬럼명 변경

```sql
ALTER TABLE 테이블이름 RENAME COLUMN 컬럼명 TO 새로운컬럼이름;
sp_rename 컬럼명, 새로운컬럼명, 'COLUMN';
```

### DROP CONSTRAINT

컬럼의 제약조건을 삭제

```sql
ALTER TABLE 테이블명 DROP CONSTRAINT 제약조건명;

# PLAYER 테이블의 외래키 제약조건을 삭제한다.
ALTER TABLE PLAYER DROP CONSTRAINT PLAYER_FK;
```

### ADD CONSTRAINT

특정 컬럼에 제약 조건을 추가

```sql
ALTER TABLE 테이블명 ADD CONSTRAINT 제약조건명 제약조건 (컬럼명);

# PLAYER 테이블에 TEAM 테이블과의 외래키 제약조건을 추가한다. 제약조건명은 PLAYER_FK로 하고, PLAYER 테이블의 TEAM_ID 칼럼이 TEAM 테이블의 TEAM_ID를 참조하는 조건이다.
ALTER TABLE PLAYER ADD CONSTRAINT PLAYER_FK FOREIGN KEY (TEAM_ID) REFERENCES TEAM(TEAM_ID);
```

FOREIGN KEY로 참조되는 테이블이 있는데 해당 테이블을 삭제하려고 하면, 에러 발생

마찬가지로 참조되는 테이블의 데이터를 삭제하려고 하여도 에러 발생

## RENAME TABLE

```sql
RENAME TABLE 테이블명 TO 새로운테이블명;
sp_rename 테이블명, 새로운테이블명;
```

## DROP TABLE

테이블을 삭제하는 명령어

```sql
DROP TABLE 테이블명 [CASCADE CONSTRAINT];
```

**`CASCADE CONSTRAINT`** : 해당 테이블과 관계가 있었던 참조되는 제약조건에 대해서도 삭제 (연결고리도 삭제하는 거)

※ SQL에서는 CASCADE 옵션이 없으므로 테이블을 삭제하기 전에 참조하는 FOREIGN KEY 제약 조건 또는 참조하는 테이블을 먼저 삭제하여야 한다.

## TRUNCATE TABLE

해당 테이블에 있던 모든 행들이 제거되고 저장 공간을 재사용 가능하도록 해제한다. (테이블 내 데이터 전체를 날리는 것) 테이블 구조를 완전히 삭제하기 위해서는 DROP TABLE을 사용하여야 함

DML의 DELETE TABLE을 사용하여도 되지만, TRUNCATE TABLE이 시스템 부하가 적음, 하지만 TRUNCATE의 경우 정상적인 데이터 복구가 불가능함

```sql
TRUNCATE TABLE 테이블명;
```

# DML

Data Manipulation Language

테이블에 관리하기를 원하는 데이터를 입력, 수정, 삭제, 조회하는 방법

<aside>
💡 DDL의 경우, 실행시 AUTO COMMIT 
DML의 경우, COMMIT을 입력하여야 함

</aside>

## INSERT

한 번에 한 건만 입력됨

```sql
INSERT INTO 테이블명 (COLUMN_LIST) VALUES (컬럼리스트에 넣을 VALUE 리스트);
INSERT INTO 테이블명 VALUES (전체 컬럼에 넣을 VALUE 리스트);
```

해당 컬럼명과 입력되어야 하는 값을 1:1로 매핑하여 입력

해당 컬럼의 데이터 유형이 CHAR이거나 VARCHAR2 등 문자유형일 경우 `‘’` single quotation으로 입력할 값을 입력

숫자일 경우, 따옴표 X

첫 번쨰 예시의 경우, 컬럼 리스트가 테이블의 컬럼 리스트 순서와 일치할 필요는 없음

두 번쨰 예시의 경우, 컬럼의 순서대로 빠짐없이 데이터가 입력되어야 함

정의하지 않은 컬럼은 Default로 NULL 값이 입력됨(단, PK나 NOT NULL로 지정된 컬럼은 NULL이 허용되지 않음) 혹은 `''` 이나 `NULL` 로 명시할 수 있음

## UPDATE

입력한 정보 중에서 정보를 수정

```sql
UPDATE 테이블명 SET 수정되어야할컬럼명 = 수정되기를 원하는 값;
```

- ```sql
  UPDATE PLAYER SET BACK_NO = 99;
  UPDATE PLAYER SET POSITION = "MF";
  ```

## DELETE

```sql
DELETE [FROM] 삭제를원하는테이블명;
```

`FROM`은 생략 가능

`WHERE` 절을 사용하지 않는다면 테이블의 전체 데이터가 삭제됨

## SELECT

데이터 조회

```sql
SELECT 컬럼명1, 컬럼명2, ... FROM 테이블명;
```

**`ALL`** : default 옵션
**`DISTINCT`** : 중복된 데이터가 있는 경우 1건으로 처리하여 출력 (중복X)

**WILDCARD `*`**

해당 테이블의 모든 컬럼의 정보를 조회하고 싶은 경우, 와일드카드로 애스터리스크(`*`)를 사용하여 조회할 수 있음

```sql
SELECT * FROM PLAYER;
```

**ALIAS**

조회된 결과에 별명을 부여하여 컬럼 레이블을 변경

- 컬럼명 바로 뒤에 작성
- 컬럼명 AS 별명 or 컬럼명 별명
- 이중인용부호 `""` 는 ALIAS가 공백, 특수문자를 포함할 경우와 대소문자 구분이 필요한 경우 사용
- 컬럼 별명을 적용할 때에 별명 중간에 공백이 들어가는 경우 `" "`를 사용하여야 함
  - SQL Server - `" "`, `' '`, `[ ]`

## 산술 연산자와 합성 연산자

### 산술 연산자

NUMBER, DATE 자료형에 대해 적용됨

- 산술 연산을 사용하거나 특정 함수를 적용하게 되면 컬럼의 레이블이 길어지므로 별명을 새로 부여하는 것이 좋음

산술 연산자의 우선순위대로 나열함

| 산술연산자 | 설명                               |
| ---------- | ---------------------------------- |
| ( )        | 연산자 우선순위 변경하기 위한 괄호 |
| \*         |                                    |
| /          |                                    |
| +          |                                    |
| -          |                                    |

### 합성 연산자

문자와 문자를 연결하는 합성(CONCATENATION) 연산자

- 문자와 문자를 연결하는 경우
  - Oracle - 2개의 수직바 `||`
  - SQL - `+`
- CONCAT(str1, str2)
- 컬럼과 문자 혹은 컬럼과 컬럼을 연결
- 문자 표현식의 결과에 의해 새로운 컬럼을 생성

# TCL

트랜잭션은 데이터베이스의 논리적 연산단위이다. 논리적인 작업 단위를 구성하는 세부적인 연산들의 집합

**트랜잭션의 특징**

| 특성                | 설명                                                                                                                             |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| 원자성(atomicity)   | 트랜잭션에서 정의된 연산들은 모두 성공적으로 실행되던지 전혀 실행되지 않던지                                                     |
| (all or nothing)    |
| 일관성(consistency) | 트랜잭션 실행되기 전의 데이터베이스의 내용이 잘못 되어있지 않았다면, 실행된 이후에도 데이터베이스의 내용에 잘못이 있으면 안된다. |
| 고립성(isolation)   | 트랜잭션이 실행되는 도중에 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어서는 안됨                                             |
| 지속성(durability)  | 트랜잭션이 성공적으로 수행되면 그 트랜잭션이 갱신한 DB의 내용은 영구적으로 저장됨                                                |

**LOCKING(잠금)**

: 트랜잭션이 수행되는 동안 특정 데이터에 대하여 다른 트랜잭션이 동시에 접근하지 못하도록 제한하는 기법

## COMMIT과 ROLLBACK

<aside>
💡 **COMMIT이나 ROLLBACK 이전의 데이터 상태**
- 데이터 변경 이전 상태로 복구 가능
- 현재 사용자는 SELECT 문장으로 결과를 확인 가능
- 다른 사용자는 현재 사용자가 수행한 명령의 결과를 볼 수 없음 
- 변경된 행은 LOCKING되어 다른 사용자가 변경할 수 없음

</aside>

### COMMIT

commit을 하면 → - 데이터에 대한 변경 사항이 데이터베이스에 반영됨

- 이전 데이터는 영원히 잃어버리게 됨
- 모든 사용자는 결과를 볼 수 있음
- LOCKING이 풀리고, 다른 사용자들이 행을 조작할 수 있음

### ROLLBACK

데이터 변경사항이 취소되어 데이터의 이전 상태로 복구됨

### SAVEPOINT

현시점에서 SAVEPOINT까지 트랜잭션의 일부만 롤백할 수 있음

복수의 저장점을 정의할 수 있고, 동일 이름으로 저장점을 정의했을 경우, 나중에 정의한 저장점이 유효

```sql
SAVEPOINT SVPT1;

ROLLBACK TO SVPT1;

SAVEPOINT TRANSACTION SVPT1;

ROLLBACK TRANSACTION SVPT1;

```

# WHERE 절

```sql
SELECT [DISTINCT / ALL] 컬럼명 [별명] FROM 테이블명 WHERE 조건식;
```

WHERE 조건절

→ 컬럼명 - 비교 연산자 - 문자, 숫자, 표현식 - 비교 컬럼명(JOIN 사용시)

## 연산자의 종류

| 구분             | 연산자              | 의미                                       | 우선순위 |
| ---------------- | ------------------- | ------------------------------------------ | -------- |
|                  | ( )                 | 괄호                                       | 1        |
| 비교 연산자      | =                   |                                            | 3        |
|                  | <, ≤                |                                            | 3        |
|                  | >, ≥                |                                            | 3        |
| SQL 연산자       | BETWEEN a AND b     | a와 b를 포함하여 그 사이의 값 중에 있다    | 3        |
|                  | IN (list)           | 리스트에 있는 값 중에서 어느 하나라도 일치 | 3        |
|                  | LIKE ‘비교문자열’   | 비교문자열과 형태 일치 (%, \_ )            | 3        |
|                  | IS NULL             | NULL 값인 경우                             | 3        |
| 논리 연산자      | AND                 | 앞과 뒤의 조건 모두 동시 만족              | 4        |
|                  | OR                  | 앞 뒤 조건 주에서 하나라도 참인 경우       | 5        |
|                  | NOT                 | 뒤에 오는 조건과 반대 결과                 | 2        |
| 부정 비교 연산자 | ! =                 |                                            | 3        |
|                  | ^=                  | 같지 않다.                                 | 3        |
|                  | <>                  | 같지 않다. (ISO 표준)                      | 3        |
|                  | NOT 컬럼명 =        | ~와 같지 않다                              | 2        |
|                  | NOT 컬럼명 >        | ~보다 크지 않다                            | 2        |
| 부정 SQL 연산자  | NOT BETWEEN a AND b | a,b 사이에 있지 않다(a, b를 포함X)         | 2        |
|                  | NOT IN (list)       | list의 값과 일치하지 않는다                | 2        |
|                  | IS NOT NULL         | NULL이 아니다                              | 2        |

Oracle - VARCHAR2 빈 문자열을 NULL로 판단

### 비교 연산자

```sql
=, <, <=, >, >=
```

### SQL 연산자

```sql
BETWEEN a AND b, IN LIST, LIKE "비교문자열", IS NULL
```

```sql
SELECT ~~~ FROM TABLE_NAME WHERE (DATA_A, DATA_B) IN ((DATA1, DATA2), (DATA1, DATA2))
```

**\*\*\*\***LIKE 연산자**\*\*\*\***

| 와일드 카드 | 설명              |
| ----------- | ----------------- |
| %           | 0개 이상의 문자들 |
| \_          | 1개의 문자        |

**\*\***\*\***\*\***IS NULL**\*\***\*\***\*\***

- NULL 값과의 수치 연산은 NULL을 리턴함
- NULL 값과의 비교 연산은 FALSE를 리턴함
- 어떤 값과도 비교할 수 없으며, 특정 값보다 크다 작다를 표현할 수 없음

### 논리 연산자

```sql
AND, OR, NOT
```

### 부정 연산자

```sql
!=, ^=, <>, NOT 컬렴명 = , NOT 컬럼명 >, NOT BETWEEN a AND b, NOT IN list, IS NOT NULL
```

## ROWNUM, TOP

<aside>
💡 ORDER BY를 사용하지 않으면 ROWNUM, TOP은 같은 기능을 수행 - 원하는 행의 개수만 return

</aside>

### ROWNUM

SQL 처리 결과 집합의 각 행에 대해 임시로 부여되는 일련 번호

테이블이나 집합에서 원하는 만큼의 행만 가져오고 싶을 때 **WHERE 절에서 행의 개수를 제한하는 역할**

```sql
# 1건의 행만 가져오는 경우
SELECT COLNAME FROM TABLENAME WHERE ROWNUM = 1;
SELECT COLNAME FROM TABLENAME WHERE ROWNUM <= 1;
SELECT COLNAME FROM TABLENAME WHERE ROWNUM < 2;

# n건의 행을 가져오고 싶은 경우
# SELECT COLNAME FROM TABLENAME WHERE ROWNUM = n; 처럼 사용할 수 없음
SELECT COLNAME FROM TABLENAME WHERE ROWNUM <= n;
SELECT COLNAME FROM TABLENAME WHERE ROWNUM < n + 1;
```

테이블 내의 고유한 키나 인덱스 값을 생성

```sql
UPDATE TABLE_NAME SET COL_NAME = ROWNUM;
```

### TOP

결과 집합으로 출력되는 행의 수를 제한

```sql
TOP (Expression) [PERCENT] [WITH TIES];
```

Expression : 반환할 행의 수를 지정하는 숫자

PERCENT : 쿼리 결과 집합에서 처음의 Expression%의 행만 반환

WITH TIES : ORDER BY 절이 지정된 경우에만 사용 가능, TOP N(PERCENT)의 마지막 행과 같은 값이 있는 경우, 추가 행이 출력되도록 지정

```sql
SELECT TOP(1) COL_NAME FROM TABLE_NAME;
SELECT TOP(n) COL_NAME FROM TABLE_NAME;
```

# FUNCTION

```sql
함수멷 (컬럼이나 표현식 [, Arg1, Arg2, ...])
```

**단일행 함수의 종류**

| 종류                                  | 내용                                        | 함수의 예                                                                                       |
| ------------------------------------- | ------------------------------------------- | ----------------------------------------------------------------------------------------------- | ---- | ------------- | --------- |
| 문자형 함수                           | 문자를 입력하면 문자나 숫자 값을 반환       | LOWER, UPPER, SUBSTR/SUBSTRING,                                                                 |
| LENGTH/LEN, LTRIM, RTRIM, TRIM, ASCII |
| 숫자형 함수                           | 숫자를 입력하면 숫자 값을 반환              | ABS, MOD, ROUND, TRUNC, SIGN, CHR/CHAR, CEIL/CEILING, FLOOR, EXP, LOG, LN, POWER, SIN, COS, TAN |
| 날짜형 함수                           | DATE 타입의 값을 연산                       | SYSDATE/GETDATE, EXTRACT/DATEPART, TO_NUMBER(TO_CHAR(d, ‘YYYY’                                  | ’MM’ | ’DD’)) / YEAR | MONTH}DAY |
| 변환형 함수                           | 문자, 숫자, 날짜 형 값의 데이터 타입을 변환 | TO_NUMBER, TO_CHAR, TO_DATE/CAST, CONVERT                                                       |
| NULL 관련 함수                        | NULL을 처리하기 위한 함수                   | NVL/ISNULL, NULLIF, COALESCE                                                                    |

**단일행 함수의 특징**

- SELECT, WHERE, ORDER BY 사용 가능
- 각 행들에 대해서 개별적으로 작용, 각 각 행에 대한 조작 결과를 리턴
- 여러 인자를 입력하여도 단 하나의 결과만 리턴
- 여러 개의 인수를 가질 수 있음
- 함수 중첩 가능

## 문자형 함수

| 문자형 함수                        | 설명                                                                                          | 결과 값 및 설명                       |
| ---------------------------------- | --------------------------------------------------------------------------------------------- | ------------------------------------- | --------------------------------------------------- |
| LOWER                              | 소문자로                                                                                      |                                       |
| UPPER                              | 대문자로                                                                                      |                                       |
| ASCII                              | 문자나 숫자를 ASCII 코드로                                                                    |                                       |
| CHR/CHAR                           | ASCII 코드를 문자나 숫자로                                                                    |                                       |
| CONCAT                             | Oracle, MySQL - 문자열1과 문자열2를 연결                                                      |
|                                    | (Oracle)과 + (SQL server)과 동일                                                              | CONCAT (’RDBMS’, ‘SQL’) ⇒ ‘RDBMS SQL’ |
| SUBSTR/SUBSTRING (문자열, m[, n])  | 문자열 중에서 m위치에서 n개의 문자 길이에 해당하는 문자를 리턴 (n이 생략되면 마지막 문자까지) | SUBSTR(’SQL Expert’, 5, 3) ⇒ ‘Exp’    |
| LENGTH/LEN                         | 문자열 길이                                                                                   |                                       |
| LTRIM(문자열 [, 지정문자])         | 문자열에서 해당 문자 제거 ( 왼쪽에서→ 오른쪽으로)                                             |
| 문자 지정하지 않으면 공백을 제거함 | LTRIM(’xxYYZZxYZ’, ‘x’) ⇒ ‘YYZZxYZ’                                                           |
| RTRIM(문자열 [, 지정문자])         | 문자열에서 해당 문자 제거 ( 오른쪽에서 ← 왼쪽으로)                                            |
| 문자 지정하지 않으면 공백을 제거함 | RTRIM(’XXYYzzXYzz’, ‘z’) ⇒ ‘XXYYzzXY’                                                         |
| TRIM([leading                      | trailing                                                                                      | both] 지정문자 FROM 문자열)           | 문자열에서 해당 문자 제거 (처음, 마지막, 혹은 양쪽) |

leading or trailiing이 생략되면 both가 default
문자 지정하지 않으면 공백을 제거함 | TRIM(’x’ FROM ‘xxYYZZxYZxx’) ⇒ ‘YYZZxYZ’ |

## 숫자형 함수

| 숫자형 함수 | 설명                    | 결과 값 및 설명 |
| ----------- | ----------------------- | --------------- |
| ABS         | 절대값                  |                 |
| SIGN        | 음수, 양수, 0 인지 구별 | SIGN(-20) ⇒ -1  |

SIGN(0) ⇒ 0
SIGN(21) ⇒ 1 |
| MOD(NUM1, NUM2) | NUM1을 NUM2로 나눈 나머지 값
% 대체 가능 | MOD(7,3) ⇒ 1 |
| CEIL/CEILING | 올림 | CEIL(3.2) ⇒ 4 |
| FLOOR | 내림 | FLOOR(2.6) ⇒ 2 |
| ROUND(NUM [, m]) | 반올림 (소수점 m자리에서 반올림) | ROUND(2.543, 2) ⇒ 2.5 |
| TRUNC(NUM [, m]) | 숫자를 소수점 m자리에서 잘라서 버림(m이 없으면 0)
SQL server에는 본 기능 X | TRUNC(28.5223, 3) ⇒ 28.522 |
| SIN, COS, TAN | 삼각함수 값 | |
| EXP(), POWER(), SQRT(), LOG(), LN() | 지수, 거듭 제곱, 제곱근, 로그, 자연 로그 값 | |

## 날짜형 함수

| 날짜형 함수                                                                                                      | 설명                                 |
| ---------------------------------------------------------------------------------------------------------------- | ------------------------------------ | ------------------------------- | ------- | --------- | ------------------------------------ |
| SYSDATE / GETDATE()                                                                                              | 현재 날짜와 시각 출력                |
| EXTRACT(’YEAR’                                                                                                   | ’MONTH’                              | ’DAY’ from d) / DATEPART(’YEAR’ | ’MONTH’ | ’DAY’, d) | 날짜 데이터에서 년/월/일 데이터 출력 |
| 시간/분/초도 가능                                                                                                |
| TO_NUMBER(TO_CHAR(d, ‘YYYY’))/YEAR(d), TO_NUMBER(TO_CHAR(d, ‘MM’))/MONTH(d), TO_NUMBER(TO_CHAR(d, ‘DD’))/DAY(d), | 날짜 데이터에서 년/월/일 데이터 출력 |
| TO_NUMBER 함수 제외 시 문자형으로 출력                                                                           |

1 = 하루, 1/24 = 1시간, 1/24/60 = 1분

## 변환형 함수

- 명시적 데이터 유형 변환 : 데이터 변환형 함수로 데이터 유형을 변환하도록 명시
- 암시적 데이터 유형 변환 : 데이터베이스가 자동으로 데이터 유형을 변환하여 계산하는 경우
  - 성능 저하가 발생할 수 있음
  - 에러 발생할 수 있음

### Oracle

| 변환형 함수             | 설명                                          |
| ----------------------- | --------------------------------------------- | ------------------------------------------------------- |
| TO_NUMBER(STR)          | alphanumeric 문자열을 숫자로 변환             |
| TO_CHAR(NUM             | DATE [, FORMAT])                              | 숫자나 날짜를 주어진 포맷의 형태로 문자열 타입으로 변환 |
| TO_DATE(STR [, FORMAT]) | 문자열을 주어진 포맷형태로 날짜 타입으로 변환 |

### SQL server

| 변환형 함수                                          | 설명                                 |
| ---------------------------------------------------- | ------------------------------------ |
| CAST (expression AS data_type [(length)])            | expression 목표 데이터 유형으로 변환 |
| CONVERT (data_type [(length)], expression [, style]) | expression 목표 데이터 유형으로 변환 |

- ```sql
  SELECT TO_CHAR(SYSDATE, 'YYYY/MM/DD') 날짜, TO_CHAR(SYSDATE, 'YYYY. MON, DAY') 문자형 FROM DUAL;
  SELECT CONVERT(VARCHAR(10), GETDATE(), 111) AS CURRENTDATE CURRENTDATE
  날짜 문자형
  ---------
  2023/09/03
  2023. 9월, 일요일
  ```
  ```sql
  SELECT TO_CHAR(123456789/1200, '$999,999,999,99') 환율반영달러, TO_CHAR(123456789, 'L999,999,999') 원화 FROM DUAL;
  ```
  ```sql
  SELECT TEAM_ID, TO_NUMBER(ZIP_CODE1, '999') + TO_NUMBER(ZIP_CODE2, '999') 우편번호합 FROM TEAM;
  SELECT TEAM_ID, CAST(ZIP_CODE1 AS INT) + CAST(ZIP_CODE2 AS INT) 우편번호합 FROM TEAM;
  ```

## CASE 표현

IF-THEN-ELSE 논리와 유사한 방식으로 표현식을 작성

| CASE 표현 | 설명 |
| --------- | ---- |

| CASE
SIMPLE_CASE_EXPRESSION 조건
ELSE EXPRESSION
END | SIMPLE_CASE_EXPRESSION CONDITION이 옳으면 해당 조건 내 THEN 절을 수행하고, 아니면 ELSE 절을 수행 |
| CASE
SEARCHED_CASE_EXPRESSION 조건
ELSE EXPRESSION
END | SEARCHED_CASE_EXPRESSION CONDITION이 맞으면 해당 조건 내 THEN 절을 수행하고, 조건이 맞지 않으면 ELSE 문을 수행 |
| DECODE (EXPRESSION, TARGET1, VAL1
[, TARGET2, VAL2, …, DEFAULT ] | (ONLY FOR ORACLE) 표현식 값이 TARGET1이면 VAL1을 출력하고, TARGET2이면 VAL2를 출력
기준값이 없으면 DEFAULT값을 출력 |

## NULL 관련 함수

### NVL/ISNULL 함수

<aside>
💡 NULL
- 아직 정의되지 않은 값으로 0/공백과는 다름
- 테이블을 생성할 때 NOT NULL 또는 PK로 정의되지 않은 모든 데이터 유형은 NULL 값을 포함할 수 있음
- NULL을 포함하는 연산은 결과 값도 NULL
- 결과값을 NULL이 아닌 다른 값을 얻고자 할 때 NVL/ISNULL 함수를 사용

</aside>

| 일반형 함수 | 설명 |
| ----------- | ---- |

| NVL(표현식1, 표현식2) /
ISNULL(표현식1, 표현식2) | 표현식1의 결과값이 NULL이면 표현식2의 값을 출력
단, 표현식1과 표현식2의 결과 Data_type이 동일해야 함
공집합을 바꿔주지는 않음 |
| NULLIF(표현식1, 표현식2) | 표현식1이 표현식2와 같으면 NULL을, 같지 않으면 표현식1을 리턴 |
| COALESCE(표현식1, 표현식2,…) | 임의의 개수 표현식에서 NULL이 아닌 최초의 표현식을 나타냄
모든 표현식이 NULL이면 NULL을 리턴 |

- 다중행 함수는 입력 값으로 전체 건수가 NULL값인 경우에만 함수의 결과가 NULL이 나옴

전체 건수 중에서 일부만 NULL인 경우에는 다중행함수의 대상에서 제외됨

→ NVL함수를 다중행함수의 인자로 사용할 필요없음

- ```sql
  COALESCE (NULL, NULL, 'abc'); => 'abc'
  ```

### NULL과 공집합

조건에 맞는 데이터가 한 건도 없는 경우 → `공집합`

→ 공집합에 NVL/ISNULL함수를 사용하여도 공집합이 출력됨

### NULLIF

**`NULLIF**(표현식1, 표현식2)`

NULLIF함수는 표현식1과 표현식2가 같으면 NULL을, 같지 않으면 표현식1을 리턴

특정 값을 NULL로 대체하는 경우 사용

### COALSECE

NULL이 아닌 최초의 표현식을 리턴

모든 표현식이 NULL이라면 NULL을 리턴

# GROUP BY, HAVING 절

집계 함수 : 다중행 함수 중에서 여러 행들의 그룹이 모여서 그룹 당 하나의 결과를 return

- GROUP BY : 행들을 소그룹화
- SELECT, HAVING, ORDER BY절에 사용 가능

| 집계 함수        | 설명                                        |
| ---------------- | ------------------------------------------- | ----------------------------------------- |
| COUNT(\*)        | NULL 값을 포함한 행의 수                    |
| COUNT(표현식)    | 표현식의 값이 NULL 값인 것을 제외한 행의 수 |
| SUM([DISTINCT    | ALL] 표현식)                                | 표현식의 NULL 값을 제외한 합계            |
| AVG([DISTINCT    | ALL] 표현식)                                | 표현식의 NULL 값을 제외한 평균            |
| MAX([DISTINCT    | ALL] 표현식)                                | 표현식의 최대값(문자, 날짜 데이터도 가능) |
| MIN([DISTINCT    | ALL] 표현식)                                | 표현식의 최소값(문자, 날짜 데이터도 가능) |
| STDDEV([DISTINCT | ALL] 표현식)                                | 표현식의 표준 편차                        |
| VARIAN([DISTINCT | ALL] 표현식)                                | 표현식의 분산                             |
| 기타             | 벤더별로 다양한 통계식 제공                 |

## GROUP BY

```sql
SELECT [DISTINCT] 컬럼명 [별명] FROM 테이블명 [WHERE 조건식] [GROUP BY 컬럼이나 표현식] [HAVING 그룹조건식];
```

1. GROUP BY절을 통해 소그룹별 기준을 정한 다음, SELECT 절에 집계 함수를 사용함
2. 집계 함수의 통계 정보는 NULL값을 제외하고 수행
3. GROUP BY 에서는 ALIAS 별명 사용 불가
4. 집계함수는 WHERE 절에 올 수 없음
5. HAVING 절에는 집계함수를 이용하여 조건을 표시
6. HAVING 절은 일반적으로 GROUP BY 뒤에 위치

```sql
SELECT POSITION COUNT(*) 인원수, COUNT(HEIGHT) 키대상, MAX(HEIGHT) 최대키, MIN(HEIGHT) 최소키, ROUND(AVG(HEIGHT),2) 평균키 FROM PLAYER GROUP BY POSITION;
```

WHERE 에서는 집계 함수를 사용할 수 없으므로 대신 HAVING을 사용 → GROUP BY를 통해서 통계 정보가 만들어지고, 이후 적용된 결과 값에 대한 HAVING 절의 제한 조건에 맞는 데이터를 출력하는 것

## HAVING

<aside>
💡 1. WHERE절 조건 적용 및 데이터 추출 → GROUP BY
2. GROUP BY → HAVING 절로 필요한 데이터만 필터링

</aside>

`집계 함수(CASE ( )) ~ GROUP BY` 기능은 모델링의 제1 정규화로 인해 반복되는 컬럼의 경우, 구분 컬럼

을 두고 여러 개의 레코드로 만들어진 집합을 정해진 컬럼의 수만큼 확장하여 집계 보고서를 만드는 기법

- 자세히
  ```sql
  예) 부서별로 월별 입사자의 평균 급여를 알고 싶다는 고객의 요구사항 -> 입사 후 1년마다 급여 인상이나 보너스 지급과 같은 일정이 정기적으로 잡힌다면?
  ```
  step1. 개별 입사정보에서 월별 데이터를 추출
  ```sql
  SELECT ENAME, DEPTNO, EXTRACT(MONTH FROM HIREDATE) 입사월, SAL FROM EMP;
  ```
  step2. 월별 데이터 구분
  ```sql
  SELECT ENAME,DEPTNO, CASE MONTH WHEN 1 THEN SAL END M01,
  										CASE MONTH WHEN 2 THEN SAL END M02.
  										CASE MONTH WHEN 3 THEN SAL END M03, ...
  										CASE MONTH WHEN 12 THEN SAL END M12
  FROM( SELECT ENAME, DEPTNO, EXTRACT(MONTH FROM HIREDATE) MONTH, SAL FROM EMP);
  ```
  step3. 부서별 데이터 집계
  ```sql
  SELECT DEPTNO, AVG(CASE MONTH WHEN 1 THEN SAL END) M01,
  							 AVG(CASE MONTH WHEN 2 THEN SAL END) M02, ...
  							 AVG(CASE MONTH WHEN 12 THEN SAL END) M12
  FROM (SELECT ENAME, DEPTNO, EXTRACT(MONTH FROM HIREDATE) MONTH, SAL FROM EMP)
  GROUP BY DEPTNO;
  ```
  or **DECODE 사용**
  `DECODE (컬럼, 조건1, 결과1, 조건2, 결과2, … , else결과)`
  else 결과를 지정하지 않으면 NULL\***\*\*\*\*\***\*\*\***\*\*\*\*\***\*\*\***\*\*\*\*\***\*\*\***\*\*\*\*\***이 디폴트 값이 됨\***\*\*\*\*\***\*\*\***\*\*\*\*\***\*\*\***\*\*\*\*\***\*\*\***\*\*\*\*\***
  ```sql
  SELECT DEPTNO, AVG(DECODE(MONTH, 1, SAL)) M01, AVG(DECODE(MONTH, 2, SAL)) M02,
  AVG(DECODE(MONTH, 3, SAL)) M03 ,... AVG(DECODE(MONTH, 12, SAL)) M12
  FROM (SELECT ENAME, DEPTNO, EXTRACT(MONTH FROM HIREDATE) MONTH, SAL FROM EMP)
  GROUP BY DEPTNO;
  ```

### 집계함수와 NULL

다중행함수에서는 전체 건수가 NULL인 경우에만 함수의 결과가 NULL이 나오고, 전체 건수 중에서 일부만 NULL인 경우는 NULL인 행을 다중행함수의 대상에서 제외시킴

- NULL이 아닌 0을 표시하고 싶은 경우, `NVL(SUM(COL1, 0))`이나 `ISNULL(SUM(SAL), 0)`처럼 전체 SUM의 결과가 NULL인 경우에만 한 번 NVL/ISNULL을 사용하면 됨

# ORDER BY 절

## ORDER BY

ORDER BY절 - 조회된 데이터들을 다양한 목적에 맞게 특정 컬럼을 기준으로 **정렬** 출력

- 컬럼명 대신 ALIAS 명이나 컬럼 순서를 나타내는 정수도 사용 가능

```sql
SELECT COL_NAME FROM TABLE_NAME [WEHRE CONDITION][GROUP BY EXP][HAVING CONDITION]
[ORDER BY 표현식 ASC/DESC]
```

- ```sql
  SELECT PLAYER_NAME, POSITION, BACK_NO FROM PLAYER WHERE BACK_NO IS NOT NULL
  ORDER BY PLAYER_NAME DESC;
  ```

**\*\*\*\***\*\***\*\*\*\***\*\***\*\*\*\***\*\***\*\*\*\***ORDER BY 절 특징**\*\*\*\***\*\***\*\*\*\***\*\***\*\*\*\***\*\***\*\*\*\***

- 기본 정렬 순서 오름차순 ASC
- Oracle에서는 NULL을 가장 큰 값으로 간주
- SQL server에서는 NULL을 가장 작은 값으로 간주

## **SELECT 문장 실행 순서**

1. SELECT 컬럼명 [ALIAS명]

1. FROM 테이블명

1. WHERE 조건식
1. GROUP BY
1. HAVING

1. ORDER BY

1. 발췌 대상 테이블을 참조한다 `FROM`
1. 발췌 대상 데이터가 아닌 것은 제거 `WHERE`
1. 행들을 소그룹화 `GROUP BY`
1. 그룹들의 값의 조건에 맞는것만 출력 `HAVING`
1. 데이터 값을 출력/계산 `SELECT`
1. 데이터 정렬 `ORDER BY`

## Top N 쿼리

### ROWNUM

인라인 뷰를 사용하여 추출하고자 하는 집합을 정렬한 후 ROWNUM을 적용시켜 결과에 참여한느 순서와 추출되는 로우 순서를 일치시킴

먼저 테이블을 정렬 → 4개를 뽑아 냄

```sql
SELECT ENAME, SAL FROM (SELECT ENAME, SAL FROM EMP ORDER BY SAL DESC) WHERE ROWNUM < 4;
```

### TOP()

-SQL server

```sql
TOP (expression) [PERCENT] [WITH TIES]
```

`WITH TIES` : ORDER BY의 기준으로 TOP n의 마지막 행으로 표시되는 추가 행의 데이터가 같을 경우 n+ 동일한 정렬 순서 데이터를 추가 반환하도록 함 → 동일 수치의 데이터를 추가로 더 추출함 (공동 n등)

- ```sql
  SELECT TOP(2) ENAME, SAL FROM EMP ORDER BY SAL DESC;
  SELECT TOP(2) WITH TIES ENAME, SAL FROM EMP ORDER BY SAL DESC;
  ```

# 조인

두 개 이상의 테이블들을 연결 혹은 결합하여 데이터를 추출하는 것

## EQUI JOIN

두 개의 테이블 간에 컬럼 값들이 서로 정확하게 일치하는 경우 사용

- 대부분 PK-FK 관계를 기반으로 함 (반드시 그렇지는 않음)
- JOIN의 조건은 WHERE 절에 기술 `=`

```sql
SELECT 테이블1.칼럼명, 테이블2.칼럼명 ... FROM 테이블1, 테이블2 WHERE 테이블1.컬럼명1 = 테이블2.컬럼명;
SELECT 테이블1.칼럼명, 테이블2.칼럼명 ... FROM 테이블1 INNER JOIN 테이블2 ON 테이블1.컬럼명1 = 테이블2.컬럼명;
```

## Non EQUI JOIN

두 개의 테이블 간에 컬럼 값들이 서로 정확하게 일치하지 않는 경우 사용

- Non EQUI JOIN의 경우 `=` 연산자가 아닌 다른 (`Between, >, ≥, <, ≤ 등`) 연산자들을 이용하여 JOIN을 수행

```sql
SELECT 테이블1.칼럼명, 테이블2.칼럼명 ... FROM 테이블1, 테이블2 WHERE 테이블1.컬럼명1 BETWEEN 테이블2.컬럼명1 AND 테이블2.컬럼명2;;
SELECT 테이블1.칼럼명, 테이블2.칼럼명 ... FROM 테이블1 INNER JOIN 테이블2 ON 테이블1.컬럼명1 BETWEEN 테이블2.컬럼명1 AND 테이블2.컬럼명2;
```
