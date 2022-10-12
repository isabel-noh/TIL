# A many-to-one relationship
관계형 데이터베이스에서의 외래 키 속성을 사용하여 모델간 N:1 관계 설정  
> RDB(관계형 데이터베이스): 데이터를 테이블, 행, 열 등으로 나누어 구조화하는 방식  
RDB의 모든 테이블에서는 행에서 고유하게 식별할 수 있는 기본 키(primary key, pk)라는 속성이 있으며, 외래 키(foreign key, fk)를 사용하여 각 행에서 서로 다른 테이블 사이의 관계를 만드는 데 사용할 수 있음   
- N:1 관계 : 한 테이블의 0개 이상의 레코드가 다른 테이블의 1개의 레코드와 관련된 경우 

#### Foreign Key 외래 키/외부 키
- 관계형 데이터베이스에서 다른 테이블의 행을 식별할 수 있는 키  
- `참조되는 테이블의 기본 키 primary key,PK`를 가리킴  
- 참조하는 테이블의 행 1개의 값은, 참조되는 테이블의 행 값에 대응됨  
    - 참조하는 테이블의 행에는 참조되는 테이블에 나타나지 않는 값을 포함할 수 없음  
- 참조하는 테이블 행 여러 개가 참조되는 테이블의 동일한 행을 참조할 수 있음
---
- 키를 사용하여 부모 테이블의 유일한 값을 참조(참조 무결성)
- 외래 키의 값이 반드시 부모 테이블의 기본 키, pk일 필요는 없지만 `유일한 값`이어야 함

> [참조 무결성]  
데이터베이스 관계 모델에서 관련된 2개의 테이블 간의 일관성을 의미함  
외래 키가 선언된 테이블의 외래 키 속성의 값은 그 테이블의 부모가 되는 테이블의 기본 키 값으로 존재해야 함(없는 값을 외래키로 사용할 수 없음)

# N:1(Comment-Article)
Comment 모델과 Article 모델 간 관계 설정  
## Django Relationship fields
1. OneToOneField() : 1대1
2. **ForeignKey()** : N대1
3. ManyToManyField() : N대N
### Comment 모델 정의
```python
class Comment(models.Model):
    article = models.ForeignKey(Article, on_delete=models.CASCADE) # table에서 article_id로 저장됨 
    content = models.CharField(max_length=200)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```
- 외래키 필드는 ForeignKey 클래스를 작성하는 위치와 관계없이 필드의 마지막에 작성됨(작성위치와 관계없이 마지막 컬럼에 작성됨) 
- ForeignKey() 클래스의 인스턴스 이름은 참조하는 모델 클래스 이름의 단수형(소문자)으로 작성하는 것을 권장 >> `모델클래스이름_id`로 저장됨

#### ForeignKey(to, on_delete, **options)
1대N relationship을 담당하는 Django의 모델 필드 클래스  
Django 모델에서 관계형 데이터베이스의 외래 키 속성 담당  

필수 인자 : 
1. 참조하는 `model_class` 
2. `on_delete` 옵선

#### ForeignKey arguments - on_delete
- 외래키가 참조하는 객체가 사라졌을 때, 외래 키를 가진 객체를 어떻게 처리할지를 정의  
- on_delete 옵션값 
    - `CASCADE` : 부모 객체(참조된 객체)가 삭제되었을 때 이를 참조하는 객체도 삭제   
        - 게시글을 삭제하면 그 아래 댓글들도 모두 삭제함
    - PROTECT, SET_NULL, SET_DEFAULT... 등

> [참고] 데이터 무결성(Data Integrity)  
> 데이터의 정확성과 일관성을 유지하고 보증하는 것  
> 데이터베이스와 RDBMS의 중요한 기능  
> 1. 개체 무결성(Entity Integrity)
> 2. 참조 무결성(Referential Integrity)
> 3. 범위 무결성(Domain Integrity)

```terminal
<!-- database를 sql문으로 바꿔서 보여줌 -->
$ python manage.py sqlmigrate migrations_file_name
```
#### 댓글 생성
```python
$ python manage.py shell_plus

# <!-- Comment Class의 Instance 'comment' 생성 -->
comment = Comment()

# <!-- 인스턴스 변수 저장 -->
comment.content = 'first_comment'

# <!-- DB에 댓글 저장 -->
comment.save()

# <!-- 에러 발생 -->
IntegrityError: NOT NULL constraint failed: articles_comment.article_id
# articles.comment 테이블의 ForeignKey field, article_id 값이 저장시에 누락되었기 때문

# 게시글 생성
article = Article.objects.create(title='title', content='content')
# 외래 키 데이터 입력 / article 객체 자체를 넣음
comment.article = article
# comment 저장
comment.save()
```

## 관계 모델 참조
```python
article.comment_set.method()
```
- Article모델이 Comment모델을 참조(역참조)할 때 사용하는 매니저
- article.comment로는 참조할 수 없음  
    - 실제로 Article 클래스에서는 Comment 클래스에 대한 어떠한 관계도 작성되어 있지 않음  
- `article.comment_set`으로 댓글 객체를 참조할 수 있음
- N:1 관계에서 생성되는 related manager의 이름은 참조하는 `모델명_set`이름 규칙으로 만들어짐  
#### Related Manager
- Related Manager는 N:1 / N:M 관계에서 사용 가능한 문맥(context)  
- Django에서 모델 간 N:1 / N:M 관계가 설정되면 `역참조`할 때에 사용할 수 있는 manager을 생성함  
    - related manager을 사용하여 queryset api를 사용할 수 있게 됨 
#### 역참조
- 나를 참조하는 테이블을 참조하는 것
- 본인을 외래키로 참조하는 다른 테이블에 접근하는 것  
- N:1관계에서 1이 N을 참조 (외래키를 가지지 않은 1이 외래키를 가진 N을 참조)
- Article이 Comment를 참조


#### ForeignKey arguments - related_name
Foreign Key 선택 옵션  
역참조 시 사용하는 매니저 이름 변경 (작성 후 makemigrations, migrate해야함)  
```python
# articles/models.py
class Comment(models.Model):
    article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name='comments')
    ...
```

#### admin site 등록
- 새로 작성한 Comment 모델을 admin site에 등록
```python
from django.contrib import admin
from .models import Article, Comment

# Register your models here.
admin.site.register(Article)
admin.site.register(Comment)
```


# N:1(Article-User)

# N:1(Comment-User)