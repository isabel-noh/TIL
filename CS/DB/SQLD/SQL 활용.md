# 표준 조인

## Standard SQL

### 1. 일반 집합 연산자

UNION → UNION

INTERSECTION → INTERSECT

DIFFERENCE → EXCEPT(MINUS)

PRODUCT → CROSS JOIN(CARTESIAN PRODUCT)

### 2. 순수 관계 연산자

SELECT → WHERE

PROJECT → SELECT

(NATURAL)JOIN → 다양한 JOIN

DIVIDE → X

## FROM절 JOIN 형태

INNER JOIN → NATURAL JOIN → USING → ON → CROSS JOIN → OUTER JOIN

## INNER JOIN

JOIN 조건에서 동일한 값이 있는 행만 반환 (양 테이블에 모두 있는 키 값이 출력됨)

CROSS JOIN, OUTER JOIN과 같이 사용X

**USING 조건절 혹은 ON 조건절 필수**

같은 내용의 컬럼 2개 있음

## NATURAL JOIN

두 테이블 간의 동일한 이름을 갖는 컬럼에 대해 EQUI(`=`) JOIN

USING, ON, WHERE 절에서 JOIN 불가

JOIN에 사용된 컬럼은 같은 데이터 타입이어야 함

ALIAS, 테이블명과 같은 접두사 X

같은 내용의 컬럼은 1개만 (중복 삭제)

## USING (조건절)

같은 이름을 갖는 컬럼들 중에서 원하는 컬럼에 대해서만 선택적으로 EQUI JOIN

SQL server X

ALIAS, 테이블명 등 접두사 X

## ON 조건절

컬럼명이 다르더라도 JOIN 조건을 사용할 수 있음

WHERE 검색 조건은 충돌 없이 사용할 수 있음 \*\*\*\*(WHERE 절과 혼용 가능)

**ALIAS나 테이블명같은 접두사 필수**

## CROSS JOIN

CARTESIAN PRODUCT

JOIN 조건이 없는 경우 생길 수 있는 모든 데이터의 조합

m\*n

## OUTER JOIN

JOIN 조건에서 동일한 값이 없는 행도 NULL값도 출력됨

**USING 조건이나 ON 조건 필수 사용**

- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN → union처럼 중복을 허용하지 않음

# 집합연산자

두 개 이상의 테이블에서 **조인을 사용하지 않고** 연관된 데이터를 조회하는 방법 중 하나

집합연산자는 2개 이상의 질의 결과를 **하나의 결과로** 만들어줌

SELECT 절의 **컬럼 수가 동일**하고, 동일 위치에 존재하는 컬럼의 **데이터 타입이 상호 호환** 가능해야 함

| 집합 연산자 | 설명                                                                       |
| ----------- | -------------------------------------------------------------------------- |
| UNION       | 여러 결과에 대한 합집합으로 결과에서 모든 중복된 행은 하나의 행으로(중복X) |
| UNION ALL   | 여러 결과에 대한 합집합으로 중복된 행도 그대로 결과로 표시됨 (중복O)       |

여러 질의 결과가 상호 배타적일 때 많이 사용
결과가 서로 중복되지 않을 경우, UNION과 결과가 동일함 |
| INTERSECT | 결과들에 대한 교집합
(중복X) |
| EXCEPT(MINUS) | 앞의 SQL 문의 결과에서 뒤의 SQL문의 결과에 대한 차집합 (앞 - 뒤)
(중복 X) |

# 계층형 질의

## 계층형 질의

테이블에 계층형 데이터가 존재하는 경우, 데이터를 조회하기 위해 계층형 질의 Hierarchcal Query를 사용

엔터티를 **순환관계** 데이터 모델로 설계할 경우, 계층형 데이터가 발생함 (조직, 사원, 메뉴 등)

### 1. Oracle 계층형 질의

```sql
SELECT ... FROM TABLE_NAME
WHERE CONDITION AND CONDITION ...
START WITH CONDITION
CONNECT BY [NOCYCLE] CONDITION AND CONDITION ...
[ORDER SIBLINGS BY COL1, COL2, ...]
```

- START WITH 조건이 레벨 1 (루트 데이터가 됨)

- ORDER SIBLINGS BY → 동일 레벨 노드 간의 정렬 규칙 (형제 노드 간)

- CONNECT BY PRIOR C1 = C2 : 이전 레벨의 노드의 C1이 현재 행의 C2와 값이 같은 행이 다음 레벨로 옴

- CONNECT BY PRIOR 자식 = 부모 : 순방향전개 (부모 → 자식)

| 가상 컬럼                            | 설명                                                                       |
| ------------------------------------ | -------------------------------------------------------------------------- |
| LEVEL                                | 루트 데이터이면 1, 하위 데이터이면 2.                                      |
| 리프 데이터까지 1씩 증가             |
| CONNECT_BY_ISLEAF                    | 전개 과정에서 해당 데이터가 리프 데이터이면 1, 아니면 0                    |
| CONNECT_BY_ISCYCLE                   | 전개 과정에서 자식을 갖는데, 해당 데이터가 조상으로서 존재하면 1, 아니면 0 |
| CYCLE 옵션을 사용했을 때만 사용 가능 |

### 2. SQL server 계층형 질의

Common Table Expression **CTE를 재귀 호출**

1. 앵커 멤버가 시작점이자 outer 집합이 되어 Inner 집합인 재귀 멤버와 조인을 시작함
2. 앞서 조인한 결과가 다시 Outer 집합이 되어 재귀 멤버와 조인을 반복하다가 조인 결과가 비어있으면 (더 조인할 수 없으면) 지금까지 만들어진 결과 집합을 모두 합하여 리턴함

## 셀프 조인

동일 테이블 사이의 조인

**한 테이블 내에서 두 컬럼이 연관 관계가 있을 때 사용** → FROM 절이 동일 테이블에서 2번 나타남

**반드시 ALIAS를 사용하여야 함**

# 서브쿼리

## 서브쿼리

하나의 SQL 문 안에 있는 또 다른 SQL 문

서브쿼리는 메인쿼리의 컬럼을 모두 사용할 수 있지만, 메인 쿼리는 서브쿼리의 컬럼을 이용할 수 없음

서브쿼리를 괄호로 감싸서 활용

단일행 혹은 복수행 비교연산자와 함께 사용 가능

**ORDER BY 사용 X**

## 서브쿼리 종류

| Sub-query                                       | description                                      |
| ----------------------------------------------- | ------------------------------------------------ |
| Un-correlated 비연관 서비쿼리                   | 서브쿼리가 메인쿼리 컬럼을 가지고 있지 않은 경우 |
| 메인쿼리에 결과값을 제공하기 위한 목적으로 사용 |
| Correlated 연관 서브쿼리                        | 서브쿼리가 메인쿼리의 컬럼을 가지고 있는 경우    |

메인쿼리가 먼저 수행되어 읽혀진 데이터를 서브쿼리에서 조건에 맞는지를 확인하는 용도로 사용  
EXISTS |

| Sub-Query                                                                                                           | description                                     |
| ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| Single row sub-query                                                                                                | 서브쿼리의 실행 결과가 항상 1건 이하인 서브쿼리 |
| 단일행 비교 연산자와 함께 사용 <, <=, =, >, >=, <>                                                                  |
| Multi row sub-query                                                                                                 | 서브쿼리의 실행 결과가 여러 건인 서브쿼리       |
| 다중 행 비교 연산자와 함께 사용 IN, ALL, ANY, EXISTS, SOME                                                          |
| Multi column sub-query                                                                                              | 서브쿼리의 실행결과로 여러 칼럼을 반환          |
| 메인쿼리의 조건절에서 여러 컬럼을 동시에 비교할 수 있음( 서브쿼리와 메인쿼리의 컬럼 개수와 컬럼위치가 동일해야 함 ) |

| Multi row operator   | description                                                                          |
| -------------------- | ------------------------------------------------------------------------------------ |
| IN (sub-query)       | 서브쿼리의 결과에 존재하는 임의의 값과 동일한 조건 (Multiple OR 조건)                |
| 비교연산자 ALL (s-q) | 서브쿼리의 결과에 존제하는 모든 값을 만족하는 조건                                   |
| 비교연산자 ANY (s-q) | 서브쿼리의 결과에 존재하는 어느 하나의 값이라도 만족하는 조건 (= SOME)               |
| EXISTS(sub-query)    | 서브쿼리의 결과를 만족하는 값이 존재하는지 확인하는 조건. 1건만 찾으면 더 이상 검색X |

## 그 외 서브쿼리

### SELECT 절에서 서브쿼리 사용하기 → `스칼라 서브쿼리` (한 행, 한 컬럼만을 반환하는 서브쿼리)

```sql
SELECT PLAYER_NAME 선수명, HEIGHT 키,
		(SELECT AVG(HEIGHT)
		FROM PLAYER X
		WHERE X.TEAM_ID = P.TEAM_ID)
FROM PLAYER P
```

### FROM절에서 서브쿼리 사용하기 → `인라인 뷰 Inline View`, `동적 뷰 Dynamic View`

- **인라인 뷰에서는 ORDER BY를 사용할 수 없음.**
- 인라인 뷰에서 먼저 정렬하고, 정렬된 결과 중에서 일부를 추출하는 것을 `TOP-N 쿼리`라고 함
- Oracle - ROWNUM이라는 연산자를 통해 일부 데이터만 추출 가능

**HAVING 절에서 서브쿼리 사용하기**

**UPDATE - SET 절에서 서브쿼리 사용하기**

**INSERT - VALUES 절에서 서브쿼리 사용하기**

## **뷰**

테이블은 실제로 데이터를 가지고 있지만, 뷰는 실제 데이터를 가지고 있지 않음

| Advantage of View                                                        | description                                                                                                |
| ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------- |
| 독립성                                                                   | 테이블 구조가 변경되어도 뷰를 사용하는 응용프로그램은 변경하지 않아도 됨                                   |
| 편리성                                                                   | 복잡한 질의를 뷰로 생성함으로써 관련 질의를 단순하게 작성할 수 있음                                        |
| 해당 형태의 SQL문을 자주 사용할 때 뷰를 이용하면 편리하게 사용할 수 있음 |
| 보안성                                                                   | 숨기고 싶은 정보가 존재한다면, 뷰를 생성할 때 해당 컬럼을 빼고 생성함으로써 사용자에게 정보를 감출 수 있음 |

# 그룹 함수

### 데이터 분석 개요

ANSI/ISO SQL 표준 - 데이터 분석을 위한 함수

- **AGGREGATE FUNCTION**
- **GROUP FUNCTION**
- **WINDOW FUNTION**

## ROLLUP 함수

ROLLUP에 지정된 Grouping Columns의 List는 **Subtotal**을 생성하기 위해 사용됨

Grouping Columns의 수를 N이라고 할 때, **N+1 Level의 Subtotal**이 생성됨

계층구조로, 인수 순서가 바뀌면 수행 결과도 바뀜. 가능한 Subtotal만 생성

GROUP BY의 확장 형태

- SQL
  ```sql
  # 부서명과 업무명을 기준으로 사원수와 급여 합을 집계한 일반적인 GROUP BY SQL문을 수행
  SELECT DNAME, JOB, COUNT(*) "TOTAL EMPL", SUM(SAL) "TOTAL SAL"
  FROM ENP, DEPT
  WHERE DEPT.DEPTNO = EMP.DEPTNO
  GROUP BY DNAME, JOB;
  ```
  ```sql
  SELECT DNAME, JOB, COUNT(*) "TOTAL EMPL", SUM(SAL) "TOTAL SAL"
  FROM ENP, DEPT
  WHERE DEPT.DEPTNO = EMP.DEPTNO
  GROUP BY ROLLUP (DNAME, JOB);
  # LEVEL 집계가 생성됨
  # L1 - GROUP BY 수행시 생성되는 표준 집계
  # L2 - DNAME 별 모든 JOB의 SUBTOTAL
  # L3 - GRAND TOTAL (마지막 행, 1건)
  ```

## CUBE 함수

결합 가능한 모든 값에 대하여 다차원 집계를 생성

Grouping Columns이 가질 수 있는 모든 경우의 수에 대하여 Subtotal을 생성하므로 Grouping Columns의 수가 N이라고 할 때, 2^N Level의 Subtotal을 생성함

- SQL
  ```sql
  # ROLLLUP -> CUBE
  SELECT
  CASE GROUPING(DNAME) WHEN 1 THEN 'ALL DEPARTMENTS' ELSE DNAME END AS DNAME,
  CASE GROUPING(JOB) WHEN 1 THEN 'ALL JOBS' ELSE JOB END AS JOB,
  COUNT(*) "TOTAL EMPL", SUM(SAL) "TOTAL SAL" FROM EMP, DEPT
  WHERE DEPT.DEPTNO = EMP.DEPTNO
  GROUP BY CUBE(DNAME, JOB);
  ```

## GROUPING SETS 함수

원하는 부분의 소계만 쉽게 추출할 수 있음

인수의 순서는 바뀌어도 결과는 같음

| expression           |               |
| -------------------- | ------------- |
| ROLLUP(expr1, expr2) | expr1 + expr2 |

expr1
전체 |
| GROUP BYexpr1, ROLLUP (expr2, expr3) | expr1 + (expr2 + expr3)
expr1 + (expr2)
expr1 |
| GROUP BY ROLLUP(expr1), expr2 | expr2 + expr1
expr2 |
| CUBE(expr1, expr2) | expr1 + expr2
expr1
expr2
전체 |
| GROUP BY expr1 CUBE(expr2, expr3) | expr1 + (expr2 + expr3)
expr1 + (expr2)
expr1 + (expr3)
expr1 |

# 윈도우 함수

분석함수(ANALYTIC FUNCTION), 순위함수(RANK FUNCTION)

`OVER` 키워드 필수!

윈도우 함수는 중첩X, 서브쿼리 안에서는 사용 가능

```sql
SELECT WINDOW_FUNCTION (ARGUMENT)
OVER ([PARTITION BY COL][ORDER BY ~][WINDOWING ~])FROM TABLE_NAME;
```

- `PARTITION BY` : 전체 집합을 기준에 의해 소그룹으로 나눌 수 있음
- `WINDOWING 절` : 함수의 대상이 되는 **행 기준의 범위**를 강력하게 지정
  (SQL serverX)
  - ROWS : 물리적인 결과 행의 수
  - RANGE : 논리적 값에 의한 범위

## 그룹내 순위 함수 RANK FUNTION

### RANK

```sql
SELECT JOB, ENAME, SAL, RANK() OVER (PARTITION BY JOB ORDER BY SAL DESC) JOB_RANK
FROM EMP;
```

### DENSE_RANK

동일한 순위를 하나의 건수로 취급 → 1등 공동 2등 공동 2등 3등
(RANK의 경우, 1등 공동 2등 공동 2등 4등)

### ROW_NUMBER

동일한 값이라도 고유한 순위를 부여함

1등 2등 3등 4등 (2등과 3등 비교값 동일해도)

(RANK의 경우, 1등 공동 2등 공동 2등 4등)

- SQL
  ```sql
  SELECT JOB, ENAME, SAL,
  RANK() OVER(ORDER BY SAL DESC) ALL_RANK,
  RANK() OVER (PARTITION BY JOB ORDER BY SAL DESC) JOB_RANK
  FROM EMP;
  ```

## 일반 집계 함수

SUM, MAX, MIN, AVG, COUNT

## 그룹 내 행 순서 함수

SQL server 미지원

### FIRST_VALUE

파티션 별 윈도우에서 가장 먼저 나온 값

공동 등수 인정 X

### LAST_VALUE

파티션 별 윈도우에서 가장 나중에 나온 값

공동 등수 인정 X

### LAG

현재 읽혀진 데이터의 이전 값을 알아내는 함수

- SQL
  ```sql
  # 입사가 빠른 날짜 순으로 정렬, 본인보다 입사가 한 명 앞선 사원의 급여를 본인의 급여와 함께 출력
  SELECT ENAME, HIREDATE, SAL, LAG(SAL) OVER (ORDER BY HIREDATE)
  FROM EMP
  WHERE JOB="SALESMAN";
  # 본인보다 입사가 빠른 2명의 급여를 함께 가져옴
  # 3번째 인자는 가져올 데이터가 없어 NULL 값이 들어오면 다른 값으로 바꿔줄 것을 지정하는 인자
  SELECT ENAME, HIREDATE, SAL, LAG(SAL, 2, 0) OVER (ORDER BY HIREDATE)
  FROM EMP
  WHERE JOB="SALESMAN";
  ```

### LEAD

이후 값을 알아내는 함수

- SQL
  ```sql
  # 직원들을 입사일자가 빠른 순으로 정렬하고, 해당 직원 다음에 입사한 사람의 입사일자를 같이 출력
  SELECT ENAME, HIREDATE, SAL,
  LEAD(HIREDATE, 1) OVER (ORDER BY HIREDATE) as "NEXTHIRED"
  FROM EMP;
  ```

## 그룹 내 비율 함수

### RATIO_TO_REPORT

전체 **SUM**컬럼 값에 대한 행 별 **컬럼 값의 백분율을** 소수점으로 구함 → 개별 RATIO의 합을 구하면 1이 됨

- SQL
  ```sql
  SELECT ENAME, SAL, ROUND(RATIO_TO_REPORT(SAL) OVER (), 2) AS R_R
  FROM EMP
  WHERE JOB="SALESMAN";
  ```

### PERCENT_RANK

파티션 별 윈도우에서 제일 먼저 나오는 것을 0으로, 제일 마지막에 나오는 것을 1로하여 값이 아닌 행의 **순서별 백분율**

- SQL
  ```sql
  SELECT ENAME, SAL,
  PERCENT_RANK() OVER (PARTITION BY DEPTNO ORDER BY SAL DESC) AS P_R
  FROM EMP;
  ```

### CUME_DIST

파티션 별 윈도우의 전체 건수에서 현재 행보다 작거나 같은 건수에 대한 **누적 백분율**

- SQL
  ```sql
  SELECT ENAME, SAL,
  CUME_DIST() OVER (PARTITION BY DEPTNO ORDER BY SAL DESC) AS C_D
  FROM EMP;
  ```

### NTILE

파티셔 별 전체 건수를 ARGUMENT 값으로 N등분한 결과

- SQL
  ```sql
  SELECT ENAME, SAL,
  NTILE(4) OVER (ORDER BY SAL DESC) AS QUAR_TILE
  FROM EMP;
  ```

# DCL(Data Control Language)

유저를 생성하고 권한을 제어하는 명령어

| User                                | Role                                                |
| ----------------------------------- | --------------------------------------------------- |
| SCOTT                               | Oracle 테스트용 샘플 유저                           |
| Default password : TIGER            |
| SYS                                 | DBA ROLE을 부여받은 유저                            |
| SYSTEM                              | 데이터베이스의 모든 시스템 권한을 부여받은 DBA 유저 |
| Oracle 설치 완료 시에 패스워드 설정 |

### 유저와 권한

- 유저 생성과 시스템 권한 부여 : ROLE을 이용하여 간편하고 쉽게 권한 부여
- OBJECT에 대한 권한 부여 : 오브젝트 권한은 특정 오브젝트인 테이블, 뷰 등에 대한 SELECT, INSERT, DELETE, UPDATE 작업 명령어를 의미

<aside>
💡 **Oracle과 SQL server의 Difference in User Architecture 
- Oracle : 유저**를 통해 DB에 접속하는 형태 
ID와 PW 방식으로 인스턴스에 접속하고 해당하는 스키마에 오브젝트 생성 등 권한을 부여받음
- **SQL server :** 인스턴스에 접속하기 위해 로그인이라는 것을 생성하게 되며, 인스턴스 내에 존재하는 다수의 DB에 연결하여 작업하기 위해 유저를 생성한 뒤, **로그인과 유저를 매핑**해 주어야 함 
Windows 인증방식과 혼합모드 방식

</aside>

### 시스템 권한

사용자가 SQL 문을 실행하기 위해서 필요한 권한

- GRANT: 권한 부여
- REVOKE: 권한 취소

```sql
GRANT CREATE USER TO SCOTT;
CONN SCOTT/TIGE
CREATE USER NHJ IDENTIFIED BY KOREA7;
GRANT CREATE SESSION TO NHJ;
GRANT CREATE TABLE TO NHJ;
REVOKE CREATE TABLE FROM NHJ;
```

모든 유저는 각각 자신이 생성한 테이블 외에 다른 유저의 테이블에 접근하기 위해서는 해당 테이블에 대한 Object 권한을 소유자로부터 부여받아야 한다.

## ROLE을 이용한 권한 부여

유저에게 알맞은 권한들을 한 번에 부여하기 위해 사용

- 많은 데이터베이스에서 유저들과 권한들 사이에서 중개 역할을 하는 ROLE을 제공
- 데이터베이스 관리자는 ROLE을 생성하고, ROLE에 각종 권한들을 부여한 후, ROLE을 다른 ROLE이나 유저에게 부여할 수 있음
- ROLE에 포함되어있는 권한들이 필요한 유저에게는 해당 ROLE만을 부여함으로써 빠르고 정확하게 필요한 권한을 부여

```sql
CREATE ROLE LOGIN_TABLE;
GRANT CREATE TABLE TO LOGIN_TABLE;
DROP USER NHJ CASCADE; # CASCADE : 하위 오브젝트까지 이어서 삭제
```

| DBA 수준 역할명                                                       | desc                                                                                                        |
| --------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| db_accessadmin                                                        | windows login, windows group, and SQL server login의 데이터베이스에 대한 액세스를 추가하거나 제거할 수 있음 |
| db_backupoperator                                                     | 데이터베이스를 백업할 수 있음                                                                               |
| db_datareader                                                         | 모든 사용자 테이블의 모든 데이터를 읽을 수 있음                                                             |
| db_datawriter                                                         | 모든 사용자 테이블에서 데이터를 추가, 삭제, 수정할 수 있음                                                  |
| db_ddladmin                                                           | 데이터베이스에서 모든 DDL 명령을 수행할 수 있음                                                             |
| db_denydatareater                                                     | 데이터베이스 내에 있는 사용자 테이블의 데이터를 읽을 수 없음                                                |
| db_denydatawriter                                                     | 데이터베이스 내의 모든 사용자 테이블에 있는 데이터를 추가, 삭제, 변경할 수 없음                             |
| db_owner                                                              | 데이터베이스 내에 있는 모든 구성 및 유지 관리 작업을 수행할 수 있고, 데이터베이스를 삭제할 수도 있음        |
| db_securityadmin                                                      | 역할 멤버 자격을 수정하고 사용권한 관리를 할 수 있음                                                        |
| 이 역할에 보안 주체를 추가하면 원하지 않는 권한 상승이 설정될 수 있음 |

# 절차형 SQL

## 절차형 SQL

SQL에도 절차 지향적인 프로그래밍이 가능하도록 DBMS 벤더별로
PL(Procedural Language)/SQL(Oracle), SQL/PL(DB2), T-SQL(SQL server) 등의 절차형 SQL을 제공함

절차형 SQL을 사용하면 SQL문의 **연속적인 실행이나 조건에 따른 분기처리**를 이용하여 특정 기능을 수행하는 **저장 모듈**을 생성할 수 있음

Procedure, User Defined Function, Trigger 등

<aside>
💡 **저장모듈 :** PL/SQL 문장을 DB 서버에 저장하여 사용자와 앱 사이에서 공유할 수 있도록 만든 일종의 SQL
독립적으로 실행되거나 다른 프로그램으로부터 실행될 수 있는 완전한 실행 프로그램

</aside>

## PL/SQL 개요

### PL/SQL 특징

- Oracle
- Block 구조로 되어있고(모듈화 가능) Block 내에는 DML 문장과 QUERY 문장, 그리고 절차형 언어(IF, LOOP)등을 사용할 수 있으며, 절차적 프로그래밍을 가능하게 하는 트랜잭션 언어
- 변수, 상수 등을 선언하여 SQL 문장 간 값을 교환
- DBMS 정의 에러나 사용자 정의 에러를 정의하여 사용할 수 있음

### PL/SQL 구조

- DECLARE : BEGIN ~ END
- 절에서 사용될 변수와 인수에 대한 정의 및 데이터 타입을 선언하는 선언부
- BEGIN ~ END : 개발자가 처리하고자 하는 SQL문과 여러 가지 비교문, 제어문을 이용하여 필요한 로직을 처리하는 실행부
- EXCEPTION : SQL문이 실행될 때 에러가 발생하면 그 에러를 어떻게 처리할 것인지를 정의하는 예외 처리부

```sql
CREATE [OR REPLACE] Procedure [Procedure_name] (args1, [mode] datatype1, ...)
IS [AS] ... .. BEGIN ... EXCEPTION ... END;

DROP Procedure [Procedure_name];
```

- 프로시저는 개발자가 자주 실행해야 하는 로직을 절차적인 언어를 이용하여 작성한 프로그램 모듈
- OR REPLACE : DB내에 같은 이름의 프로시저가 있는 경우, 기존의 프로시저를 무시하고 새로운 내용으로 덮어씀

PL/SQL로 작성된 Procedure, User Defined Function 은 작성자의 기준으로 트랜잭션을 분할할 수 있음

동적 SQL 또는 DDL문장을 실행할 때 `EXECUTE IMMEDIATE`를 사용하여야 함

## T-SQL

### T-SQL 특징

- T-SQL은 SQL server을 제어하기 위한 언어로, MS사에서 ANSI/ISO 표준의 SQL에 약간의 기능을 추가하여 보완적으로 만든 것

```sql
CREATE Procedure [schema_name.]Procedure_name @parameter1 datatype1 [mode], ...
BEGIN ... EXCEPTION .. END;

DROP Procedure [schema_name.]Procedure_name;
```

**절차형 SQL 모듈**

- 저장형 프로시저는 SQL을 로직과 함께 DB 내에 저장해 놓은 명령문은 집합
- 저장형 함수(사용자 정의 함수)는 단독적으로 실행되기 보다는 다른 SQL문을 통해서 호출되고 그 결과를 리턴하는 SQL 보조 역할
- 트리거는 특정한 테이블에 INSERT, UPDATE, DELETE… DML문이 수행되었을 때 DB에서 자동으로 동작하도록 작성된 프로그램
  데이터의 무결성과 일관성을 위해서 사용자 정의 함수를 사용 → Trigger
- Trigger는 TCL을 사용할 수 없음

| Procedure                 | Trigger             |
| ------------------------- | ------------------- |
| CREATE Procedure 문법     | CREATE TRIGGER 문법 |
| EXECUTE 명령어            | 생성 후 자동 실행   |
| COMMIT, ROLLBACK 실행가능 | TCL 실행 X          |
