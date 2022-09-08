# Django
서버를 구현하는 웹 프레임워크  
프레임 워크_Framework: 서비스 개발에 필요한 기능들을 미리 구현하여 모아놓은 것  
- 특정 프로그램을 개발하기 위한 여러 도구들과 규약을 제공하는 것
- 소프트웨어의 생산성과 품질을 높임

> #### Django를 배워야하는 이유
> 1. Python으로 작성된 프레임워크
> 2. 수많은 여러 유용한 기능들
> 3. 검증된 웹 프레임워크
>   - 화해, Toss, 두나무, 당근 마켓, 요기요 등
>   - 유명한 서비스들이 많이 사용한다는 것 > 안정적으로 서비스를 할 수 있다는 검증

## WWW(world wide web)

### Client and Server
대부분의 웹 서비스는 클라이언트-서버 구조를 기반으로 동작  
어떠한 자원resource를 달라고 요청request하는 쪽 - client  
자원을 제공response해주는 쪽 - server

#### 클라이언트
웹 사용자의 인터넷에 연결된 장치  
e.g. wi-fi에 연결된 컴퓨터 혹은 모바일  
e.g. Chrome / Firefox와 같은 웹 브라우저  
서비스를 요청하는 주체(request)

#### 서버
웹 페이지, 사이트 혹은 웹을 저장하는 컴퓨터  
클라이언트가 웹페이지에 접근하려고 할 때 서버에 클라이언트 컴퓨터로 웹 페이지 데이터를 응답하여 사용자의 웹 브라우저에 표시됨  
요청에 대해 서비스를 응답하는 주체(response)

### Web Browser와 Web Page
웹 브라우저 : 웹 페이지에서 찾아 보여주고, 사용자가 하이퍼링크를 통하여 다른 페이지로 이동할 수 있도록 하는 프로그램  
웹 페이지 파일을 우리가 보는 화면으로 바꾸어주는(렌더링, Rendering) 프로그램  

웹 페이지 : 우리가 보는 화면 한장 한장
- 정적 웹 페이지(Static Web Page)  
    - 한 번 작성된 HTML파일의 내용이 변하지 않고 모든 사용자에게 동일한 모습으로 전달됨  
    - 서버에 미리 저장된 HTML 파일 그대로 전달된 웹페이지  
    - 같은 상황에서 모든 사용자에게 동일한 정보를 표시
- 동적 웹 페이지(Dynamic Web Page)
  - 사용자의 요청에 따라 웹 페이지에 추가적인 수정이 되어 클라이언트에게 전달되는 웹 페이지
  - 웹 페이지의 내용을 바꿔주는 주체 - 서버
  - 서버에서 동작하고 있는 프로그램이 웹 페이지를 변경  
  - 다양한 서비사이드 프로그래밍 언어(Python, Java, C++ 등) 사용 가능, 파일을 처리하고 데이터베이스와의 상호작용이 이루어짐


## MTV Design Pattern
#### Design Pattern
각기 다른 기능을 가진 다양한 응용 소프트웨어를 개발할 때 공통적인 설계가 존재하며, 이를 처리하는 해결책 사이에도 공통점이 있음 -> 패턴  
자주 사용되는 구조와 해결책을 건축의 공법처럼 **일반적인 구조화**를 해둔 것  
- 목적  
  특정 문맥에서 공통적으로 발생하는 문제에 대해 재사용 가능한 해결책을 제시  
  다수의 엔지니어들이 일반화된 패턴으로 소프트웨어 개발을 할 수 있도록한 규칙, 커뮤니케이션의 효율성을 높이는 방법  

##### **MVC**(Model-View-Conroller)  
데이터 및 논리제어를 구현하는 데 널리 사용되는 소프트웨어 디자인 패턴  
각 부분을 독립적으로 개발할 수 있어, 하나를 수정하고 싶을 때 모두 건들지 않아도 됨 -> 개발 효율성 및 유지보수 용이, 다수의 팀원으로 개발하기 용이
1. Model: 데이터와 관련된 로직 관리
2. View: 레이아웃과 화면을 처리
3. Controller: 명령을 Model과 View 부분으로 연결  
  
### MTV Design Patter
Django에 적용된 디자인 패턴으로 MVC 디자인 패턴을 기반으로 조금 변형된 패턴  
1. Model: 데이터와 관련된 로직 관리  
   응용프로그램의 데이터 구조를 정의하고 데이터베이스의 기록을 관리
2. Template: 레이아웃과 화면 처리  
   화면상의 사용자 인터페이스 구조와 레이아웃을 정의  
   MVC패턴에서 View의 역할
3. View: Model & Template과 관련한 로직을 처리하여 응답을 반환  
   클라이언트의 요청에 대해 처리를 분기  
   MVC패턴에서 Controller의 역할

> 데이터가 필요하다면 Model에 접근하여 데이터를 가져오고, 가져온 데이터를 template로 보내 화면을 구성하고, 구성된 화면을 응답으로 만들어 client에게 반환

![MVC](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbSqV1T%2FbtrpRXjBEOj%2FkeDZnehItOnHslVnekvnFK%2Fimg.png)


## Django 기본설정

##### 가상환경설정
- 가상환경 생성
`python -m venv venv`  

- 가상환경 실행   
`source venv/bin/activate` ( MAC OS )
`source venv/Scripts/activate` ( Windows OS )

- interpreter 설정 
`현재 경로의 venv/Scripts/의 python`으로 설정

- 가상환경 deactive
`deactive`

##### Django 설치
- 설치 전 가상환경 설정 및 활성화를 마치고 진행  
  `pip install django==3.2.13`

> [참고]  
LTS(Long Term Support) : 장기 지원 버전  
일반적인 경우보다 장기간에 걸쳐 지원하도록 고안된 sw의 버전  
컴퓨터 소프트웨어의 제품 수명주기 관리 정책  
배포자는 LTS확정을 통하여 장기적이고 안정적인 지원을 보장

- 패키지 목록 생성  
  `pip freeze > requirements.txt`
  - requirements.txt의 파일을 모두 설치하고자 할 때   
    `pip install -r requirements.txt`
- 프로젝트 생성  
  `django-admin startproject [project_name] .`
- 서버 실행  
  `python manage.py runserver`

##### 프로젝트 구조
- \__init__.py
  - python에게 이 디렉토리를 하나의 python package로 다루도록 지시
  - 별도로 추가 코드를 작성하지 않음
- asgi.py
  - Asynchronous Server Gateway Interface
  - Django application이 비동기식 웹 서버와 연결 및 소통하는 것을 도움
- settings.py
  - Django 프로젝트 설정을 관리
- urls.py 
  - 사이트의 url과 적절한 views의 연결을 지정
- wsgi.py
  - Web Server Gateway Interface
  - Django 어플리케이션이 웹서버와 연결 및 소통하는 것을 도움
- manage.py
  - Django 프로젝트와 다양한 방법으로 상호작용하는 커맨드라인 유틸리티
  ```python
  # manage.py Usage
  python manage.py <command [options]>
  ```
##### Django Application
- 앱 생성  
  `python manage.py startapp [app_name 복수형]`

##### 애플리케이션 구조
- admin.py
  -관리자용 페이지를 설정하는 곳
- app.py
  - 앱의 정보가 작성된 곳
- models.py
  - 어플리케이션에서 사용하는 Model을 정의하는 곳
  - MTV의 M
- tests.py
  - 프로젝트의 테스트 코드를 작성하는 곳
- views.py
  - view 함수들이 정의되는 곳
  - MTV 패턴의 V  

##### 애플리케이션 등록  
  프로젝트에서 앱을 사용하기 위하여 반드시 INSTALLED_APPS 리스트에 추가하여야 함
  - INSTALLED_APPS : Django installation에 활성화 된 모든 앱을 지정하는 문자열 목록  
  - **주의**  
  **반드시 생성 후 등록할 것**  
  INSTALLED_APPS에 먼저 작성 후 생성하려 하면 앱이 생성되지 않기 때문
  ```python 
  # settings.py
  INSTALLED_APPS = [
    # local apps
    'articles',

    # Third party apps

    # Django apps
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
  ]
  ```

#### Project & Application
- Projet 
  - collection of apps
  - 앱의 집합
  - 프로젝트에는 여러 앱이 포함될 수 있으며, 앱은 여러 프로젝트에 포함되어있을 수 있음

- Application
  - 앱은 실제 요청을 처리하고 페이지를 보여주는 등의 역할을 담당 
  - 앱은 하나의 역할 및 기능 단위로 작성하는 것을 권장 

## 요청과 응답  
URL > VIEW > TEMPLATE 순의 작성 순서로 데이터 흐름 이해  

### URLs
```python
# urls.py
from django.contrib import admin
from django.urls import path
from articles import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('index/', views.index),
    path('greeting/', views.greeting),
]
```
### View
HTTP요청을 수신하고 HTTP응답을 반환하는 함수 작성  
Template에게 HTTP응답 서식을 맡김  
```python
# view.py
from django.shortcuts import render

# Create your views here.
def index(request):
    return render(request, 'index.html')

def greeting(request):
    # return render(request, 'greeting.html', {'name': 'Isabel'})
    foods = ['apple', 'banana', 'coconut',]
    info = {
        'name': 'Isabel'
    }
    context = {
        'foods' : foods,
        'info' : info,
    }
    return render(request, 'greeting.html', context)
```
#### render()
`render(request, template_name, context)`
- 주어진 템플릿을 주어진 컨텍스트 데이터와 결합하고 렌더링 된 텍스트와 함께 HttpResponse(응답) 객체를 반환하는 함수  
1. request : 응답을 생성하는 데 사용되는 요청 객체
2. template_name : 템플릿의 전체 이름 또는 템플릿 이름의 경로
3. context : 템플릿에서 사용할 데이터(dictionary 타입)


### Templates
실제 내용을 보여주는 데 사용되는 파일  
파일 구조나 레이아웃을 정의  
- app_name/templates/
- 주의!  
  **템플릿 폴더 이름은 반드시 templates여야 함** 
```html
<!--articles/templates/index.html-->
<!DOCTYPE html>
<html lang="en">
<head>
  <!--생략-->
</head>
<body>
  <h1>만나서 반가워요</h1>
  <a href="/greeting">greeting</a>
</body>
</html>
```

> **데이터의 흐름 순서**  
URL > View > Template   
코드 작성도 동일한 순서로! 

> [기타 설정]
Language_Code : 모든 사용자에게 제공되는 번역을 결정  
USE_I18이 활성(True)되어야 함  
TIME_ZONE : 데이터베이스 연결의 시간대를 나타내는 문자열 지정  
USE_TZ이 활성화(True)되고 이 옵션이 설정된 경우 데이터베이스에서 날짜와 시간을 읽으면, UTC 대신 새로 설정한 시간대의 인식 날짜&시간이 반환됨

```python
# settings.py
LANGUAGE_CODE = 'ko-kr'
TIME_ZONE = 'Asia/Seoul'
```
## Django Template
데이터 표현을 제어하는 도구 / 표현에 관련된 로직    
Django Template를 이용한 HTML 정적 부분과 동적 컨텐츠 삽입  
Template System의 기본 목표를 숙지

### Django Template Language(DTL)
Django Template에서 사용하는 built-in template system  
- 조건, 반복, 변수 치환, 필터 등의 기능 제공 
  - Python처럼 일부 프로그래밍 구조(if, for 등)을 사용할 수 있지만 python 코드로 실행되는 것은 아님 
  - Django Template System은 단순히 Python이 HTML에 포함된 것이 아님을 주의  
  - 프로그ㅐㄹ밍적 로직이 아니라 프레젠테이션을 표현하기 위한 것임을 명심! 

### DTL syntax
#### 1. Variable
`{{ variable }}`  
- 변수명은 영어, 숫자, (_)밑줄로 구성될 수 있으나, 밑줄로는 시작할 수 없음  
  - 공백이나 구두점은 사용할 수 없음
- dot(.)을 사용하여 변수 속성에 접근할 수 있음
- render()의 세번째 인자로, {'key':'value'}와 같이 딕셔너리 형태로 전달되며, 여기서 정의한 key에 해당하는 문자열이 template에서 사용가능한 변수명이 됨  
```python
# views.py
def greeting(request):
    foods = ['apple', 'banana', 'coconut']
    info = {
        'name' : 'Isabel'
    }
    context = {
        'foods' : foods,
        'info' : info,
    }
    return render(request, 'greeting.html', context)
```
```django
# greeting.html
<p>저는 {{foods.0}}을 가장 좋아합니다</p>
<p>안녕하세요, 저는 {{info.name}}입니다. </p>
```

#### 2. Filters
`{{ variable|filter }}`  
- 표시할 변수를 수정할 때 사용 
  - name변수를 모두 소문자료 출력 {{ name|lower }}  
- 60개의 built-in template filters 제공
- chained가 가능하며 일부 필터는 인자를 받기도 함 (e.g. {{ name|truncatewords:30 }})
```python
# views.py
def dinner(request):
    foods = ['족발', '팔보채', '스시', '과일']
    pick = random.choice(foods)
    context = {
        'foods' : foods,
        'pick' : pick,
    }
    return render(request, 'dinner.html', context)
```
```django
# dinner.html
<p>{{pick}}은 {{pick|length}} 글자입니다.</p>
<p>{{foods|join:", "}}</p>
```

#### 3. Tags
`{% tag %}`
- 출력 텍스트를 만들거나, 반복 또는 논리를 수행하여 제어 흐름을 만드는 등 변수보다 복잡한 일들을 수행  
- 일부 태그는 시작과 종료 태그가 필요  
  - `{% if %}` / `{% for %}`
- 약 24개의 built-in template tags를 제공
```django 
<p>메뉴판</p>
    <ul>
      {% for food in foods %}
        <li>{{ food }}</li>
      {% endfor %}
    </ul>
```
#### 4. Comments
`{# #}`
- Django Template에서 라인의 주석을 표현하기 위해 사용
- 아래처럼 유효하지 않은 템플릿 코드가 표함될 수 있음 
  - {# {% if %} text {% enif %} #}
- 한줄 주석에만 사용할 수 있음
- 여러 줄 주석은 {% comment %}와 {% endcomment %}사이에 입력
```django
{% comment %}
  주석
  주석
{% endcomment %}
```

## Template Inheritace 템플릿 상속
코드의 재사용성을 위해  
템플릿 상속을 사용하면 사이트의 모든 공통 요소를 포함하고, 하위 템플릿이 재정의(override)할 수 있는 블록을 정의하는 기본 **'skeleton'** 템플릿을 만들 수 있음

- `{% extends '' %}`
  - 자식(하위)템플릿이 부모 템플릿을 확장한다는 것을 알림
  -  반드시 템플릿 **최상단**에 작성되어야 함 -> 2개 이상 사용할 수 없음  

- `{% block content %}{% endblock content %}`
  - 하위 템플릿에서 재지정(override)할 수 있는 블록을 정의
  - 하위 템플릿이 채울 수 있는 공간
  - 가독성을 높이기 위해서 선택적으로 endblock 태그에 이름을 지정할 수 있음(안 써도 됨)

```django
<!--base.html-->
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- bootstrap CDN 작성 -->
    <title>document</title>    
  </head>
  <body>
    {% block content %}
    {% endblock content %}
    <!-- bootstrap CDN 작성 -->
  </body>
</html>
```
```django
<!-- index.html -->
{% extends 'base.html' %}

{% block content %}
  <h1>만나서 반가워요!</h1>
  <a href="/greeting/">greeting</a>
  <a href="/dinner/">dinner</a>
{% endblock content %}
```

##### 추가 템플릿 경로 추가하기
- base.html의 위치를 앱 안의 template 디렉토리가 아닌 프로젝트 최상단의 templates 디렉토리 안에 위치하고 싶다면?
- 기본 template 경로가 아닌 다른 경로를 추가하기 위해 다음 코드 작성   
`'DIRS': [BASE_DIR / 'templates',],`
```python
# settings.py

TEMPLATES = [
  {
    # 'BACKEND': '...',
    'DIRS': [BASE_DIR / 'templates',],
    # 'APP_DIRS':True,
    ...
  }
]
```
```directory
articles/
firstpjt/
templates/
    base.html
```

>[참고] BASE_DIR 
>- settings.py에서 특정 경로를 절대 경로로 편하게 작성할 수 있도록 Django에서 미리 지정해둔 경로 값 
>- 객체 지향 파일 시스템 경로
>   - 운영체제별로 파일 경로 표기법이 다르기 때문에 어떤 운영체제에서 실행되더라도 각 운영체제 표기법에 맞게 해석될 수 있도록 하기 위하여 사용  
```django
# settings.py
BASE_DIR = Path(__file__).resolve().parent.parent
```

# Sending and Retrieving form data
### Client & Server Architecture
- 웹은 다음과 같이 가장 기본적으로 클라이언트-서버 아키텍처를 사용
  - 클라이언트가 서버에 요청을 보내고, 서버는 클라이언트의 요청에 응답
- 클라이언트 측에서 HTML form은 HTTP요청을 서버에 보내는 가장 쉬운 방법
- 이를 통하여 사용자는 HTTP 요청에서 전달할 정보를 제공할 수 있음


## Sending form data(Client)
### HTML < form > element
데이터가 전송되는 방식을 정의   
웹에서 사용자 정보를 입력하는 여러 방식(text, button, submit 등)을 제공, **사용자로부터 할당된 데이터를 서버로 전송하는 역할 담당**
- 데이터를 어디action로 어떤 방식method으로 보낼 것인가
#### ACTION
- 입력 데이터가 전송될 URL지정  
- 데이터를 어디로 보낼 것인지를 지정하는 것  
- 중요! **유효한 URL일 것**  
  > 만약 속성을 지정하지 않으면 데이터는 현재 form이 있는 페이지의 URL로 보내짐  
#### METHOD
- 데이터를 어떻게 보낼 것인지 정의  
- 입력 데이터의  HTTP request methods를 지정  
- HTML form 데이터 전송방식 : **GET / POST**

```django
{% extends 'base.html' %}

{% block content %}
  <h1>Throw</h1>
  <form action="#" mehtod="#"></form>
{% endblock content %}
```

### HTML < input > element
사용자로부터 데이터를 입력받기 위하여 사용  
- 'type'속성에 따라 동작 방식이 달라짐  
- 지정하지 않은 경우, 기본값은 'text'

#### HTML input's attribute
##### name
- form을 통해 데이터를 submit할 때 name속성에 설정된 값을 서버로 전송하고, 서버는 **name**속성에 설정된 값을 통해 사용자가 입력한 **데이터에 접근**할 수 있음  
- GET/POST 방식으로 서버에 전달하는 파라미터로 매핑하는 것 (name - key, value - value)
  - GET방식에서는 URL에서 `?key=value&key=value/`형식으로 데이터 전달
```python
# urls.py
  path('throw/', views.throw),

# views.py
def throw(request):
    return render(request, 'throw.html')
```
```django
{% extends 'base.html' %}

{% block content %}
    <h1>Throw</h1>
    <form action="#" method="#">
        <label for="message">Throw</label>
        <input type="text" id="message" name="message">
        <input type="submit">
    </form>

{% endblock content %}
```

### HTTP request methods
- HTTP
  - HTML문서와 같은 리소스(데이터, 자원)을 가져올 수 있도록 해주는 프로토콜(규칙, 규약)
  - 웹에서 이루어지는 모든 데이터 교환의 기초
  - HTTP는 주어진 리소스가 수행할 원하는 작업을 나타내는 request methods를 정의
- 자원에 대한 행위(수행하고자 하는 동작)을 정의
- 주어진 resource자원에 수행하기를 원하는 행동을 나타냄
- **GET, POST, PUT, DELETE**
  
#### GET
- 서버로부터 정보를 조회하는 데 사용(리소스 요청)
- 데이터를 가져올 때만 사용해야
- 데이터를 서버로 전송할 때 Query String Parameters를 통해 전송
  - 데이터는 URL에 포함되어 서버로 보내짐
- 명시적 표현을 위해 대문자 사용
```django
<form action="#" method="GET">
    ...
</form>
```

##### Query String Parameters
사용자가 입력 데이터를 전달하는 방법 중 하나로 url주소에 데이터를 파라미터를 통해 넘기는 것  
- 문자열은 `&(앰퍼샌드)`로 연결된 key=value 쌍으로 구성되며, 기본 URL과 `?(물음표)`로 구분됨
  - https://host:port/path?key=value&key=value
- == Query String
- 정해진 주소 이후에 '물음표'를 쓰는 것으로 시작
- 파라미터가 여러 개일 경우 '&'로 여러 개의 파라미터를 넘길 수 있음



## Retrieving the data(Server)
- 데이터 가져오기(검색하기)  
- 서버는 클라이언트로 받은 key-value 쌍의 목록과 같은 데이터를 받게 됨  
- 목록에 접근하는 방법은 사용하는 특정 프레임워크에 따라 상이
```python
# views.py
def catch(request):
    return render(request, 'catch.html')
    
# urls.py
  path('catch/', views.catch)
```
```django
<!-- catch.html -->
{% extends 'base.html' %}

{% block content %}
    <h1>Catch</h1>
    <h2>여기서 데이터 받음</h2>
    <a href="/throw/"> 다시 던지러 </a>
{% endblock content %}
```
throw.html 파일의 form의 action도 적어줘야함
```django
<!-- throw.html -->
<form action="/catch/" method="GET">
    <label for="message">Throw</label>
    <input type="text" id="message" name="message">
    <input type="submit">
</form>
```

#### 데이터 가져오기
throw 페이지의 form이 보낸 데이터는 catch 페이지의 url에 포함되어 서버로 보내짐
```url
http://127.0.0.1:8000/catch/?message=데이터
```
> view함수의 첫번째 인자 **request**를 확인
```python
# views.py
def catch(request):
    message = request.GET.get('message')
    context = {
        'message' : message, 
    }
    return render(request, 'catch.html', context)
```
```django
{% extends 'base.html' %}

{% block content %}
    <h1>Catch</h1>
    <h2>여기서 데이터 {{ message }} 받음</h2>
    <a href="/throw/"> 다시 던지러 </a>
{% endblock content %}
```

#### Request and Response objects
- 요청과 응답 객체 흐름
1. 페이지가 요청되면 Django는 요청에 대한 메타데이터를 포함하는 HttpRequest object 생성
2. 해당하는 적절한 view 함수를 로드하고 HttpRequest를 첫번째 인자로 전달
3. view함수는 HttpResponse object를 반환

## Django Urls
### Trailing URL Slashes
- Django는 URL 끝에 `/`(trailing slash)가 없다면 자동으로 붙여주는 것이 기본 설정
  - 모든 주소가 '/'로 끝나도록 구성되어있음
  - 모든 프레임워크가 위처럼 동작하는 것은 아님
  - Django의 url 설계 철학 상 기술적인 측면에서 foo.com/bar 와 foo.com/bar/는 서로 다른 URL임
  - Django는 URL을 정규화하여 검색 엔진 로봇이 혼동하지 않도록 함

>[참고] URL 정규화  
정규 URL(오리지널로 평가되어야 할 URL)을 명시하는 것  
복수 페이지에서 같은 컨텐츠가 존재하는 것을 방지

### Variable Routing
템플릿의 많은 부분이 중복되고, 일부분만 변경되는 상황에서 비슷한 URL과 템플릿을 계속 만드는 것은 불필요   
Variable routing: URL 주소를 변수로 사용하는 것  
URL 일부를 변수로 지정하여 view함수의 인자로 넘길 수 있음  
변수 값에 따라 하나의 path()에 여러 페이지를 연결시킬 수 있음 

#### Variable Routing 작성
- 변수는 '<>'에 정의하며 view함수의 인자로 할당됨 
- 기본타입은 string이며, 그 외 4가지가 있음
  - 1. str 
    - '/'를 제외하고 비어있지 않은 모든 문자열
    - 작성하지 않을 경우 기본값
  - 2. int
    - 0 또는 양의 정수와 매치
  - 3. slug
  - 4. uuid
  - 5. path

```python
# urls.py
from articles import views

urlpatterns = [
  ...,
  # path('hello.<str:name>/', views.hello),
  path('hello/<name>/', views.hello),
]

# articles/views.py
def hello(request, name):
  context = {
    'name' : name,
  }
  return render(request, 'hello.html', context)
```

```django
<!-- hello.html -->
{% extends 'base.html' %}

{% block content%}
  <h1> 만나서 반갑습니다. {{ name }} </h1>
{% endblock %}
```
> [참고] Routing  
> 어떤 네트워크 안에서 통신 데이터를 보낼 때 최적의 경로를 선택하는 과정  

### App URL mapping
- 앱이 점점 늘어날 수록 urls.py를 각 app에 매핑하여야 혼동을 방지할 수 있음
- app의 view 함수가 많아지면서 사용하는 path() 또한 늘어나고, app 또한 더 많이 작성될 것이기 때문에 프로젝트의 urls.py에서 모두 관리하는 것은 프로젝트 유지보수에 좋지 않음
- 두번째 app인 pages를 생성 및 등록 

> - 각 앱의 view 함수를 다른 이름으로 import할 수 있음
>    ```python
>   from articles import views as articles_views  
>   from pages import views as pages_views
>   ```
> but 너무 불편하고 귀찮은 방법임

#### **하나의 프로젝트에 여러 앱이 존재한다면, 각각 앱 안에 urls.py를 만들고 프로젝트 urls.py에서 각 앱의 urls.py 파일로 URL 매핑을 위탁할 수 있음**
```python
# articles/urls.py
from django.urls import path
from . import views
urlpatters = [
  path('index/', views.index),
  path('greeting/', views.greeting),
  path('dinner/', views.dinner),
  path('throw/', views.throw),
  path('catch/', views.catch),
  path('hello/<str:name>', views.hello)
]

# pages/urls.py
from django.urls import path
urlpatters = [

]
```

- **Including other URLconfs**  
  - urlpattern은 언제든지 다른 URLconf 모듈을 포함(include)할 수 있음  
  - include되는 app의 url.py에 urlpatterns가 작성되어 있지 않다면 에러가 발생  
    - 빈 리스트라도 작성되어있어야 함  
    ```python
    # firstpjt/urls.py
    from django.contrib import admin      
    from django.urls import path, include

    urlpatters = [
      path('admin/', admin.site.urls),
      path('articles/', include('articles.urls')),
      path('pages/', include('pages.urls')),
    ]
    ```

  - http: // 127.0.0.1:8000 / index / > `http://127.0.0.1:8000/articles/index/`


##### include()
  - 다른 URLconf(app1/urls.py)들을 참조할 수 있도록 돕는 함수  
  - 함수 include()를 만나게 되면 URL의 그 시점까지 일치하는 부분을 잘라내고, 남은 문자열 부분을 후속 처리를 위해 include된 URLconf로 전달  

#### Naming URL patterns
링크에 URL을 직접 작성하는 것이 아니라 path() 함수의 name 인자를 정의하여 사용  
DTL tag 중 **URL 태그**를 사용하여 path 함수에 작성한 name 사용({% url '' %})  
```python
urlpatters = [
      path('index/', views.index, name='index'),
      path('greeting/', views.greeting, name='greeting'),
      path('dinner/', views.dinner, name='dinner'),
      ...
    ]
```

- URL tag
  - `{% url '' %}`
  - 주어진 URL 패턴 이름 및 선택적 매개변수와 일치하는 절대 경로 주소를 반환
  - 템플릿에 URL을 하드 코딩하지 않고도 DRY(do not repeat yourself) 원칙을 위반하지 않으면서 링크를 출력하는 방법  


