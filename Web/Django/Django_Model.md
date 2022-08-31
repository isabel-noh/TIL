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
