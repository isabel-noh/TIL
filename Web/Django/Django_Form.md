### Form에 대한 Django의 역할
- 유효성 검사 도구 중 하나로 외부의 악의적 공격 및 데이터 손상에 대한 중요한 방어 수단
- 유효성 검사를 단순화하고 자동화할 수 있는 기능을 제공하여 개발자가 핵심 부분  개발에 집중할 수 있도록 도와주는 프레임워크

### Django Form에 관련된 처리 부분
1. 렌더링을 위한 데이터 준비 및 재구성
2. 데이터에 대한 HTML forms 생성
3. 클라이언트로부터 받은 데이터 수신 및 처리 

# Django Form Class
Django form 관리 시스템의 핵심 
- Form Class를 선언하는 것은 Model Class를 선언하는 것과 유사
    - 비슷한 이름의 필드 타입을 많이 가지고 있음
- Model과 마찬가지로 상속을 통해 선언
    - forms library의 Form Class를 상속받음
```python
# articles/forms.py
from django import forms

class ArticleForm(forms.Form):
    title = forms.CharField(max_length=10)
    content = forms.CharField()
```

- forms에는 TextField()가 없음
- 다른 파일 (e.g. models.py ...) 안에 작성해도 무관하지만, 관행적으로 **forms.py**에 작성하는 것을 권장
```python
# articles/views.py
from .forms import ArticleForm

def new(request):
    form = ArticleForm()
    context = {
        'form': form,
    }
    return render(request, 'articles/new.html', context)
```
```django
<!-- articles/new.html -->
{% extends 'base.html' %}

{% block content %}
  <h1>NEW</h1>
  <form action="{% url 'articles:create' %}" method="POST">
    {% csrf_token %}
    {% comment %} {{ form }}  {% endcomment %}
    {{ form.as_p }}
    <input type="submit">
  </form>
  <hr>
  <a href="{% url 'articles:index' %}">뒤로가기</a>
{% endblock content %}
```
- view 함수에서 정의한 ArticleForm의 인스턴스 form 하나로 input과 label 태그가 모두 랜더링됨
- 각 태그의 속성 값들 또한 자동으로 설정되어 있음

#### Form rendering options
- < label > & < input >쌍에 대한 3가지 출력옵션
1. **as_p()**
    - 각 필드가 단락(< p >)로 감싸져서 렌더링
2. as_ul()
    - 각 필드가 목록 항목(< li >)으로 감싸져서 렌더링
    - < ul > 태그는 직접 작성
3. as_table()
    - 각 필드가 테이블( < tr >)행으로 감싸져서 렌더링


#### Django의 2가지 HTML input 요소 표현
1. Form field  
입력에 대한 유쇼성 검사로직을 처리  
템플릿에서 직접 사용  
```python
forms.CharField()
```
2. Widgets  
웹 페이지의 HTML input 요소 렌더링을 담당   
Widgets는 반드시 form fields에 할당됨  
```python
forms.CharField(widget=forms.Textarea)
```

## Widget
- 웹 페이지의 HTML input 요소 렌더링을 담당
- 단순히 HTML 렌더링을 처리하는 기능만 있을뿐, 유효성 검증과는 아무런 관계가 없음 ( 웹 페이지에서 input element의 단순 raw한 렌더링만을 처리할 뿐)
```python
class ArticleForm(forms.Form):
    NATION_A = 'kr'
    NATION_B = 'ch'
    NATION_C = 'jp'
    NATIONS_CHOICES = [
        (NATION_A, '한국'),
        (NATION_B, '중국'),
        (NATION_C, '일본'),
    ]
    title = forms.CharField(max_length=10)
    content = forms.CharField(widget=forms.Textarea)
    nation = forms.ChoiceField(choices=NATIONS_CHOICES)
    # nation = forms.ChoiceField(choices=NATIONS_CHOICES, widget=forms.RadioSelect)
```

### ModelForm Class
Model을 통해 Form Class를 만들 수 있는 helper class
ModelForm은 Form과 똑같은 방식으로 View 함수에서 사용  

#### ModelForm 선언
- forms library에서 파생된 ModelForm 클래스를 상속받음  
- 정의한 ModelForm 클래스안에 Meta Class 선언  
- 어떤 모델을 기반으로 form을 작성할 것인지에 대한 정보를 Meta class에 지정
```python
# articles/forms.py
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    class Meta: # ModelForm에 대한 데이터 설정

        # 어떤 모델을 기반으로 할지
        model = Article  # 참조 값 (인스턴스화 X)
        # 어떤 모델 필드 중에서 어떤 것을 출력할지
        fields = '__all__'
        # exclude = ('title',)  # 해당 필드 제외시키기
```
- Meta Class의 model 속성이 참조할 모델을 받음
- 참조하는 모델에 정의된 field 정보를 Form에 적용
- field 속성에 '\__all__'를 사용하여 모델의 모든 필드를 포함
- exclude 속성을 사용하여 모델에 포함하지 않을 필드 지정
    - fields와 exclude를 함께 작성하여도 되나 권장 X


> [참고] Meta data  
> 데이터를 표현하기 위한 데이터  
> e.g. 사진 파일  
> 사진 데이터  
> 사진 데이터의 데이터 (촬영 시각, 렌즈, 조래개 값 등) == 사진 데이터에 대한 데이터(Meta data)

> [참고] 참조 값과 반환 값    
> 함수를 참고로 확인할 수 있음    
> - 첫번째 결과는 참조 값을 출력  
> - 두번째 결과는 반환 값을 출력
>```python
>def greeting():
>    return 'HELLO'
>print(greeting) # <function greeting at 0x10761caf0>
>print(greeting()) # HELLO
># view의 함수에 참조값을 그대로 넘김으로써, path 함수가 내부적으로 >해당 view함수를 필요할 때에 사용하기 위해서
>```

> **클래스도 마찬가지**  
> Article이라는 클래스를 호출하지 않고 작성하는 이유는 ArticleForm이 해당 클래스를 필요한 시점에 사용하기 위해서  
> +) 이 경우 인스턴스가 필요한 것이 아니라, 실제 Article 모델의 참조 값을 통하여 해당 클래스의 필드나 속성을 내부적으로 참조하기 위한 이유도 있음
>```python
>class ArticleForm(forms.ModelForm):
>    class Meta:
>        model = Article
>        fields = '__all__'
>```

> ##### Form과 ModelForm
> - Form과 ModelForm, 어느 것이 더 좋은 것이 아니라 역할이 다른것
> - Form
>    - 사용자로부터 받는 데이터가 DB와 연관되어있지 않은 경우
>    - DB에 영향을 미치지 않고 단순 데이터만 사용되는 경우
>    - e.g. 회원가입, 사용자의 데이터를 받아 인증 과정에서만 사용 후 별도로 DB에 저장하지 않음
> - ModelForm
>    - 사용자로부터 받는 데이터가 DB와 연관되어 있는 경우
>    -  데이터의 유효성 검사가 끝나면 데이터를 각각 어떤 레코드에 매핑해야 하는지 이미 알고 있기 때문에 바로 form.save()호출 가능

## ModelForm with view functions
### CREATE
```python
# articles/views.py
def create(request):
    form = ArticleForm(request.POST)
    if form.is_valid():
        form.save()
        return redirect('articles:index')
    return redirect('articles:new')
```
#### `is_valid`method
- 유효성 검사를 실행하고, 데이터가 유효한지 여부를 boolean으로 반환
- 데이터 유효성 검사를 보장하기 위한 많은 테스트에 대해 Django는 is_valid()를 제공하여 개발자의 편의를 도움
- is_valid()의 반환값이 False인 경우, form 인스턴스의 errors 속성에 '유효성 검증을 실패한 원인'이 딕셔너리 형태로 저장됨
```python
# articles/views.py
def create(request):
    form = ArticleForm(request.POST)
    if form.is_valid():
        article = form.save()
        return redirect('articles:detail', article.pk)
    print(f'에러: {form.errors}')
    return redirect('articles:new')
```
- 아래와 같은 구조로 코드를 작성하면 유효성 검증을 실패했을 때 사용자에게 실패 결과 메시지를 출력해줄 수 있음
```python
# articles/views.py
def create(request):
    form = ArticleForm(request.POST)
    if from.is_valid():
        article = form.save()
        return redirect('articles:detail', article.pk)
    # 사용자에게 실패 결과 메시지를 출력
    context = {
        'form': form,
    }
    return render(request, 'articles/new.html', context)
```

#### `save()` method


ㅇㄴㅇㄹㅇㄴ


### View Decorators
기존에 작성된 함수에 기능을 추가하고 싶을 때, 해당 함수를 **수정하지 않고 기능을 추가**해주는 함수  
#### Allowed HTTP methods   
django.views.decorators.http의 데코레이터를 활용하여 **요청 메서드를 기반으로 접근을 제한**할 수 있음  
일치하지 않는 메서드 요청이라면 405 Method Not Allowed를 반환  
1. `require_http_methods()` : 여러 개의 HTTP method로 제한 걸 수 있음   
2. `require_POST()` : view함수가 POST요청만 허용
3. `require_safe()` : Django에서는 view함수가 GET요청할 때, require_GET() 대신 require_safe()를 사용할 것을 권장

> ##### [참고] 405 Not Allowed Method  
> 요청 방법이 서버에 전달되었으나 사용 불가능한 상태



##### forms에서 widget사용하기
```python
from django import forms
from .models import Movie


GENRE_CHOICES = [
    ('comedy', '코미디'),
    ('horror', '공포'),
    ('romance', '로맨스'),
]

class MovieForm(forms.ModelForm):

    class Meta:
        model = Movie
        fields = '__all__'
        widgets = {
            'title' : forms.TextInput(attrs={'class': 'form-control', 'placeholder':'Title'}),
            'audience' : forms.TextInput(attrs={'class': 'form-control', 'placeholder':'Audience'}),
            'release_date' : forms.DateInput(attrs={'class': 'form-control', 'type':'date'}),
            'genre' : forms.Select(attrs={'class': 'form-control'}, choices=GENRE_CHOICES),
            'score' : forms.NumberInput(attrs={'class': 'form-control', 'type':'number', 'step':'0.5', 'min':'0.0', 'max':'5.0', 'placeholder':'Score'}),
            'poster_url' : forms.TextInput(attrs={'class': 'form-control', 'placeholder':'Poster url'}),
            'description' : forms.Textarea(attrs={'class': 'form-control', 'placeholder':'Description', 'rows':5}),
        }
```