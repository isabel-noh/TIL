
ModelSerializer
- 단일모델에 대한 serialize
```shell
python manage.py shell_plus
>>> from articles.serializers import ArticleListSerializer
>>> serializer = ArticleListSerializer()
>>> serializer
ArticleListSerializer():
    id = IntegerField(label='ID', read_only=True)
    title = CharField(max_length=100)
    content = CharField(style={'base_template': 'textarea.html'})
>>> article = Article.objects.get(pk=1)
>>> serializer = ArticleListSerializer(article)
>>> serializer
ArticleListSerializer(<Article: Article object (1)>):
    id = IntegerField(label='ID', read_only=True)
    title = CharField(max_length=100)
    content = CharField(style={'base_template': 'textarea.html'})
>>> serializer.data
{'id': 1, 'title': 'Hair each base dark guess garden accept.', 'content': 'Religious ball another laugh light million. Federal public power another.\nDuring always recent maintain major others bank. Say place address. Wife tough outside system must. Develop road especially.'}
```
- QuerySet 객체 serialize  
단일 객체 인스턴스가 아니고 QuerySet 혹은 객체 목록일 경우, `many = True` 값을 넣어줘야 함
```shell
>>> articles = Article.objects.all()
>>> serializer = ArticleListSerializer(articles, many=True)
>>> serializer.data
[OrderedDict([('id', 1), ('title', 'Hair each base dark guess garden accept.')...,
```

# Build RESTful API
## GET
### GET - List
게시글 데이터 목록 조회  
DRF에서 `@api_view` 데코레이터 작성은 필수임  
```python
# urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('articles/', views.article_list),
] # 본 예시에서는 app_name이나 urlpatterns-path-name 필요 없음
```
```python
# serializers.py
from rest_framework import serializers
from .models import Article, Comment

class ArticleListSerializer(serializers.ModelSerializer):

    class Meta:
        model = Article
        fields = ('id', 'title', 'content',)
```
```python
# articles/views.py
from rest_framework.response import Response
from rest_framework.decorators import api_view

from .models import Article
from .serializers import ArticleListSerializer

@api_view(['GET'])  # 안에 아무값도 없으면 ['GET']이 기본값
def article_list(request):
    articles = Article.objects.all()
    serializer = ArticleListSerializer(articles, many=True)
    return Response(serializer.data)
```

### GET - Detail
단일 게시글 조회  
```python
# serializers.py
class ArticleSerializer(serializers.ModelSerializer):

    class Meta:
        model = Article
        fields = '__all__'
```
```python
# urls.py
urlpatterns = [
    ...,
    path('articles/<int:article_pk>', views.article_detail)
]
```
```python
# views.py
from .serializers import ArticleListSerializer, ArticleSerializer

@api_view(['GET'])
def article_detail(request, article_pk):
    article = Article.objects.get(pk=article_pk)  # 단일 모델이기 때문에 many=True 불필요
    serializer = ArticleSerializer(article)
    return Response(serializer.data)
```

## POST
요청에 대한 데이터 생성이 성공하면 `201 Created` Https 상태 코드를, 응답하고 실패했을 경우에는 `400 Bad request`를 응답  
```python
# articles/views.py
from rest_framework.response import Response
from rest_framework.decorators import api_view

from rest_framework import status

from .models import Article
from .serializers import ArticleListSerializer

@api_view(['GET', 'POST'])  # 안에 아무값도 없으면 ['GET']이 기본값
def article_list(request):
    if request.method == 'GET':
        articles = Article.objects.all()
        serializer = ArticleListSerializer(articles, many=True)
        return Response(serializer.data)
    elif request.method == 'POST':
        serializer = ArticleSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```
- Raising an exception on invalid data  
유효하지 않은 데이터에 대해 예외 발생 시키기   
    - is_valid()는 유효성 검사 오류가 있는 경우 ValidationError 예외를 발생시키는 선택적 `raise_exception` 인자를 사용할 수 있음  
    - DRF에서 제공하는 기본 예외 처리기에 의해 자동으로 처리되며 기본적으로 400를 return 
```python
@api_view(['GET', 'POST'])  # 안에 아무값도 없으면 ['GET']이 기본값
def article_list(request):
    if request.method == 'GET':
        ...
    elif request.method == 'POST':
        serializer = ArticleSerializer(data=request.data)
        if serializer.is_valid(raise_exception=True):
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        # return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```

## DELETE
게시글 데이터 삭제  
요청에 대한 데이터 삭제가 성공적으로 이루어졌을 경우 204 No Content 상태코드 응답(명령을 수행했고, 더 이상 제공할 데이터가 없는 경우)
```python
@api_view(['GET', 'DELETE'])
def article_detail(request, article_pk):
    article = Article.objects.get(pk=article_pk)  # 단일 모델이기 때문에 many=True 불필요

    if request.method == 'GET':
        serializer = ArticleSerializer(article)
        return Response(serializer.data)

    elif request.method == 'DELETE':
        article.delete()
        return Response(serializer.response, status=status.HTTP_204_NO_CONTENT)        
```

## PUT
게시글 데이터 수정  
요청에 대한 데이터 수정을 성공적으로 수행했을 경우 200 OK 상태 코드 응답
```python
@api_view(['GET', 'DELETE', 'PUT'])
def article_detail(request, article_pk):
    article = Article.objects.get(pk=article_pk)  # 단일 모델이기 때문에 many=True 불필요

    if request.method == 'GET':
        serializer = ArticleSerializer(article)
        return Response(serializer.data)

    elif request.method == 'PUT':
        serializer = ArticleSerializer(article, data=request.data)  # instance에 해당하는 값이 맨 앞에 들어감 
        # serializer = ArticleSerializer(instance = article, data=request.data)
        if serializer.is_valid(raise_exception=True):
            serializer.save()
            return Response(serializer.data)  # 200 STATUS 라서 별도로 작성하지 않음 

    elif request.method == 'DELETE':
        article.delete()
        return Response(serializer.response, status=status.HTTP_204_NO_CONTENT) 
```

# N:1 Relation - Comment
## GET
```python
# models.py
class Comment(models.Model):
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```
### GET-List
```python
# serializers.py
from .models import Comment, Article

class CommentSerializer(serializers.ModelSerializer):
    
    class Meta:
        model = Comment
        fields = '__all__'
```
```python
# urls.py
urlpatterns = [
    ...,
    path('comments/', views.comment_list),
]
```
```python
# views.py
from .models import Article, Comment
from .serializers import ArticleListSerializer, ArticleSerializer, CommentSerializer

@api_view(['GET'])
def comment_list(request):
    if request.method == 'GET':
        comments = Comment.objects.all()
        serializer = CommentSerializer(comments, many=True)
        return Response(serializer.data)
```
### GET-Detail
```python
# urls.py
urlpatterns = [
    ...,
    path('comments/<int:comment_pk>', views.comment_detail),
]
```
```python
# views.py
@api_view(['GET'])
def comment_detail(request, comment_pk):
    if request.method == 'GET':
        comment = Comment.objects.get(pk=comment_pk)
        serializer = CommentSerializer(comment)
        return Response(serializer.data)
```

## POST 
단일 댓글 데이터 생성
```python
# urls.py
urlpatterns = [
    ...,
    url('articles/<int:article_pk>/comments/', views.comment_create),
]
```
```python
# views.py
@api_view(['POST'])
def comment_create(request, article_pk):
    article = Article.objects.get(pk=article_pk)
    serializer = CommentSerializer(data=request.data)
    if serializer.is_valid(raise_exception=True):
        serializer.save(article=article)
        return Response(serializer.data, status=status.HTTP_201_CREATED) 
```
- Passing Additional attributes to `.save()`
    - models.py에서는 'commit=False'라는 인자를 넣어주었음 -> 인스턴스 생성하고 거기에 article 넣고 그 다음 저장 
    - CommentSerializer를 통해 Serialize되는 과정에서 파라미터로 넘어온 article_pk에 해당하는 article 객체를 추가적인 데이터를 넘겨 저장
```python
# serializer.save() 
# ->
# serializer.save(article=article) 
```

> [에러 발생]  
CommentSerializer에서 article field 데이터 또한 사용자로부터 입력을 받도록 설정되어 있음  
읽기 전용 필드 설정을 해주어야 함


### 읽기 전용 필드 설정 
- `read_only_fields` 를 사용하여 외래 키 필드를 `읽기 전용 필드`로 설정
- 데이터를 전송하는 시점에 해당 필드를 유효성 검사에서 제외시키고 데이터 조회 시에는 출력되도록 함 
```python
# serializers.py
class CommentSerializers(serializers.ModelSerializer):

    class Meta:
        model = Comment
        fields = '__all__'
        read_only_fields = ('article',)
```

## DELETE & PUT
```python
# views.py
@api_view(['GET', 'PUT', 'DELETE'])
def comment_detail(request, comment_pk):
    comment = Comment.objects.get(pk=comment_pk)
    if request.method == 'GET':
        serializer = CommentSerializer(comment)
        return Response(serializer.data)
    elif request.method == 'DELETE':
        comment.delete()
        return Response(status = status.HTTP_204_NO_CONTENT)
    elif request.method == 'PUT':
        serializer = CommentSerializer(comment, data=request.data)
        if serializer.is_valid(raise_exceptions=True):
            serializer.save()
            return Response(serializer.data)
```

# N:1 - 역참조 데이터 조회
## 1. 특정 게시글에 작성된 댓글 목록 출력
- 기존 필드를 override
    - 게시글 조회 시 해당 게시글의 댓글 목록까지 함께 출력  
    - Serializer는 기존 필드를 override 하거나 추가적인 필드를 구성할 수 있음 
### 1. PrimaryKeyRelatedFields()
```python
# serializers.py
class ArticleSerializers(serializers.ModelSerializer):
    # comment의 pk만 가져옴
    comment_set = serializers.PrimaryKeyRelatedField(many=True, read_only=True)
    # read_only = True --> 읽기전용 

    class Meta:
        model = Article
        fields = '__all__'
```
- models.py에서 related_name을 통해 이름 변경 가능 
    - related_name = ''
- 역참조 시 생성되는 comment_set을 override 할 수 있음 
```python
# models.py
class Comment(models.Model):
    article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name='comments')
    content = models.TextField()
    ...
```
### 2. Nested Relationships
- 모델 관계 상으로 참조된 대상은 참조하는 대상의 표현에 포함되거나 중첩(nested)될 수 있음 
- 이러한 중첩된 관계는 serializers를 필드로 사용하여 표현할 수 있음 
    - 두 클래스의 상/하 위치를 변경해야 함
```python
# serializers.py
class CommentSerializer(serializers.ModelSerializer):
    
    class Meta:
        model = Comment
        fields = '__all__'
        read_only_fields = ('article',)

class ArticleSerializer(serializers.ModelSerializer):
    # comment 역참조 내용 다 가져옴
    comment_set = CommentSerializer(many=True, read_only=True
    )
    class Meta:
        model = Article
        fields = '__all__'
```
## 2. 특성 게시글에 작성된 댓글의 개수 출력
- 새로운 필드 추가 - Article Detail
    - 게시글 조회 시 해당 게시글의 댓글 개수까지 같이 표시하기
```python
class ArticleSerializer(serializers.ModelSerializer):
    # comment 역참조 내용 다 가져옴
    comment_set = CommentSerializer(many=True, read_only=True
    comment_count = serializers.IntegerField(source='comment_set.count', read_only=True)
    )
    class Meta:
        model = Article
        fields = '__all__'
```
- `source` 
    - 필드를 채우는 데 사용할 속성의 이름
    - 점 표기법(dotted notation)을 사용하여 속성을 탐색할 수 있음

> [주의] read_only_fields  
특정 필드를 override 혹은 추가한 경우에는 read_only_fields에 적용되지 않으므로 별도로 해당 변수마다 'read_only=True'를 넣어줘야함  
물리적으로 테이블에 comment_set과 comment_count는 존재하지 않기 때문

# Django shortcuts functions
django shortcut package  
- render, redirect, get_object_or_404, get_list_or_404 등 개발에 도움이 되는 함수와 클래스 제공 

## get_object_or_404 & get_list_or_404
- 사용 이유 : 클라이언트 입장에서 "서버에서 에러가 발생하여 수행할 수 없음(500)"이라는 원인을 알 수 없는 에러를 마주하기 보다는, 서버가 적절한 예외를 처리하고 클라이언트에게 보다 정확한 에러 메시지를 출력해주는 것이 중요함
### get_object_or_404
모델 manager object에서는 get을 호출하지만 해당 객체가 없을 경우에는 Http404를 raise함
```python
# views.py
from django.shortcuts import get_object_or_404

# article = Article.objects.get(pk=article_pk)
# comment = Comment.objects.get(pk=comment_pk)
# 위 코드를 아래 코드로 변경
article = Article.objects.get_object_or_404(pk=article_pk)
comment = Comment.objects.get_object_or_404(pk=comment_pk)
```

### get_list_or_404
모델 manager object에서는 filter을 호출하지만 해당 객체가 없을 경우에는 Http404를 raise함
```python
from django.shortcuts import get_list_or_404

# article = Article.objects.all()
# comment = Comment.objects.all()
# 위 코드를 아래 코드로 변경
articles = Article.objects.get_list_or_404(Article)
comments = Comment.objects.get_list_or_404(Comment)
```