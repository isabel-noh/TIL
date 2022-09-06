# Django Model
Model의 핵심 개념과 ORM을 통한 DB 조작 이해  
Django는 웹 어플리케이션의 데이터를 구조화하고 조작하기 위한 추상적인 계층(모델)을 제공함  

### Database
: 체계화된 데이터의 모임 
: 검색 및 구조화같은 작업을 보다 쉽게 하기 위하여 조직화된 데이터를 수집하는 저장 시스템  

#### Database 기본 구조
1.  **Schema 스키마**
뼈대(Structure)  
데이터베이스의 자료의 구조, 표현 방법, 관계 등을 정의한 구조  

2.  **Table 테이블**  
관계(Relation)
필드와 레코드를 사용하여 조직된 데이터 요소들의 집합  
    1) Field 필드  
    : 속성, 컬럼(Column)  
    : 각 필드에는 고유한 데이터 형식이 지정됨 ( INT, TEXT 등 ) 
    2) Record 레코드  
    : 튜플, 행(Row)  
    : 테이블의 데이터는 레코드에 저장됨  
  
3. PK(Primary Key)  
기본 키  
각 레코드의 고유한 값(식별자로 사용) (e.g. 주민등록번호)  
기술적으로 다른 항목과 절대로 중복될 수 없는 단일 값(unique)  
데이터베이스 관리 및 테이블 간 관계 설정시 주요하게 활용됨  

4. Query 쿼리  
데이터를 조회하기 위한 명령어  
조건에 맞는 데이터를 추출하거나 조작하는 명령어(주로 테이블형 자료구조에서)  
'Query를 날린다' == '데이터베이스를 조작한다'

## Model 
Django는 Model을 통해 데이터에 접근하고 조작  
사용하는 데이터들의 필수적인 필드들과 동작들을 포함  
저장된 데이터베이스의 구조(layout)  
일반적으로 각각 모델은 하나의 데이터베이스 테이블에 매핑(mapping)  
- `모델 클래스 1개 == 데이터 베이스 테이블 1개`  
> [참고]  
Mapping 매핑: 하나의 값을 다른 값으로 대응시키는 것  

### Model 작성하기
- 새 프로젝트(crud), 앱(articles) 작성 및 앱 등록  
`$ djang-admin startproject crud .`  
`$ python manage.py startapp articles`
```python
# setting.py
INSTALLED_APPS = [
    'articles',
    ...
]
```


## Migration


..
`python `


## ORM
Object-Relational-Mapping  
- 객체 지향 프로그래밍 언어를 사용하여 호환되지 않는 유형의 시스템 간(e.g. Django <-> DB)에 데이터를 변환하는 프로그래밍 기술
- 객체 지향 프로그래밍에서 데이터베이스를 연동할 때에, 데이터베이스와 객체 지향 프로그래밍 언어 간에 호환되지 않는 데이터를 변환하는 프로그래밍 기법
- Django - 내장 Django ORM 사용
- SQL 사용 없이 데이터베이스를 조작할 수 있게 함

## QuerySet API
[사전 준비]  



>[참고] Shell
> - 운영체제 상에서 다양한 기능과 서비스를 구현하는 인터페이스를 제공하는 프로그램 
> - 사용자와 운영체제의 내부 사이의 인터페이스를 감싸는 층이기 때문에 Shell이라는 이름이 붙음
> - 사용자 - 쉘 - 운영체제


### Database API
#### Object Manager

#### Query
- 데이터베이스에 특정한 데이터를 보여달라는 요청 
- 파이썬으로 작성한 코드가 ORM에 의하여 SQL로 변환되어 데이터베이스에 전달되며, 데이터베이스의 응답 데이터를 ORM이 QuerySet이라는 자료형태로 변환하여 우리에게 전달하게 됨

#### QuerySet
- DB에서 전달받은 객체 목록(데이터 모음)
    - 순회가 가능한 데이터로써 1개 이상의 데이터를 불러와 사용할 수 있음
- 

### CRUD
#### Create

#### Read
QuerySet API method를 사용하여 데이터를 다양하게 조회하기  
- Methods that "return new querysets" -> 데이터 목록 조회
- Methods that "do not return querysets" -> 데이터 개별 조회

#### Update

#### Delete