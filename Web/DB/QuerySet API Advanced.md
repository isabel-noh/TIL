### Sorting Data
#### order_by()  
.order_by(*fields)  
- QuerySet의 정렬을 재정의  
- 기본적으로 `오름차순`으로 정렬하며, 필드명에 `-`을 작성하면 내림차순으로 정렬함  
- 인자로 `?`을 입력하면 랜덤으로 정렬  
```python
# 나이를 오름차순으로 정렬 후, 이름과 나이만 출력
User.objects.order_by('age').values('first_name', 'age')
# 나이를 내림차순으로 정렬 후, 이름과 나이만 출력
User.objects.order_by('-age').values('first_name', 'age')
```
#### values()
.values(*fields, **expressions)
- 모델 인스턴스가 아닌 딕셔너리 요소들을 가진 QuerySet을 반환
- *fields는 선택인자이며 조회하고자 하는 필드명을 가변인자로 입력받음  
    - 필드를 지정하면 각 딕셔너리에는 지정한 필드에 대한 key와 value값만을 출력
    - 입력하지 않았을 경우에는 각 딕셔너리에 레코드의 모든 필드에 대한 key와 value를 출력함
```python
# values() method 미사용
User.objects.filter(age=30)
# values() method 사용
User.objects.filter(age=30).values('first_name', 'age')
```
- 이름과 나이를 나이가 많은 순서대로 조회하기
```python
User.objects.order_by('-age').values('first_name','age')
```
- 이름과 나이, 계좌 잔고를 나이가 어린순으로, 만약 같은 나이라면 계좌잔고가 많은순으로 정렬하여 조회하기
```python
# 나이는 오름차순, 계좌잔고는 내림차순
User.objects.order_by('age','-balance').values('first_name', 'age', 'balance')
```

> [참고] order_by 주의사항  
다음과 같이 작성할 경우 앞의 호출은 모두 지워지고 마지막 호출만 적용됨 
> ```python
> User.objects.order_by('balance').order_by('-age')
> # == User.objects.order_by('-age')
> # 둘다 적용되게 하려면 User.objects.order_by('balance', '-age')
> ```

### Filtering Data
- 중복없이 모든 지역 조회하기
```python
User.objects.distinct().values('country')
```
- 지역 순으로 오름차순 정렬하여 중복없이 모든 지역 조회하기
```python
User.objects.distinct().order_by('country').values('country')
```
- 이름과 지역이 중복없이 모든 이름과 지역 조회하기
```python
User.objects.distinct().values('first_name', 'country')
```
- 이름과 지역 중복없이 지역 순으로 오름차순 정렬하여 모든 이름과 지역 조회하기
```python
User.objects.distinct().order_by('country').values('first_name', 'country')
```
- 나이가 30인 사람들의 이름 조회
```python
User.objects.filter(age=30).values('fist_name')
```
#### field lookups
SQL WHERE 절의 상세한 조건을 지정하는 방법    
QuerySet 메서드 filter(), exclude(), get()에 대한 키워드 인자로 사용됨  
`field__lookuptype=value` 필드명 뒤에 'double_underscore'(`__`) 이후 작성

- 나이가 30살 이상인 사람들의 이름과 나이 조회하기
```python
User.objects.filter(age__gte=30).values('first_name', 'age')
```
- 나이가 30살 이상이고 계좌 잔고가 50만원 초과인 사람들의 이름, 나이, 계좌 잔고 조회하기
```python
User.objects.filter(age__gte=30, balance__gt=500000).values('first_name', 'age', 'balance')
```

-------
# Improve Query
Query 개선하기 
- annotate
- select_related
- prefetch_related
## annotate
```python
    articles = Article.objects.annotate(Count('comment')).order_by('-pk')
```
## select_related
1:1 또는 1:N 참조 관계에서 사용  
SQL의 INNER JOIN을 사용하여 참조하는 테이블의 일부를 가져오고, SELECT FROM을 사용하여 관련된 필드들을 가져옴  
```python
    articles = Article.objects.select_related('user').order_by('-pk')
```

## prefetch_related
N:1 역참조 관계에서 사용 
```python
    articles = Article.objects.prefetch_related('comment_set').order_by('-pk')
```

#### 예시
```python
    articles = Article.objects.prefetch_related(
        Prefetch('comment_set', queryset=Comment.objects.select_related('user'))
    ).order_by('-pk')
```