# Django Authentication System
`django.contrib.auth`

- Authentication
- Authorization

### Substituting a custom User Model
User Model도 CRUD랑 마찬가지
- 'Custom User Model'로 대체
- Django는 현재 프로젝트에서 사용할 user model을 결정하는 `AUTH_USER_MODEL` 설정값으로 Default User Model을 재정의(override)할 수 있게 함   

##### AUTH_USER_MODEL
: 프로젝트에서 User을 나타내기 위해 사용되는 모델  
- 프로젝트가 시작될 때 설정해야함(모델을 만들고 migrate한 뒤에는 변경 불가)  
- 다음과 같은 기본 값을 가지고 있음(setting.py상에는 안보이지만 settings.py가 상속받은 global_settings.py에 기본으로 설정되어 있음)
```python
# settings.py
AUTH_USER_MODEL = 'auth.User'
```

#### 'Custom User Model'로 대체하기
1. AbstractUser을 상속받는 커스텀 User Class 작성
    - 기존 user 클래스도 AbstractUser을 상속받기 때문에 커스텀 User Class도 같은 모습을 가지게 됨
2. Django 프로젝트에서 User를 나타내는 데 사용하는 모델(auth.User)을 방금 생성한 커스텀 User 모델(accounts.User)로 지정
3. admin.py에 커스텀 User 모델을 등록
    - 등록하지 않으면 user.site에서 확인할 수 없음

```python
# step1
# accounts/models.py
from django.db import models
from django.contrib.auth.models import AbstractUser

# Create your models here.
class User(AbstractUser):
    pass
```
```python
# step2
# crud(project)/settings.py 맨 하단에
AUTH_USER_MODEL = 'accounts.User'
```
```python
# step3
# accounts/admin.py
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin
from .models import User

# Register your models here.
# admin site에 등록
admin.site.register(User, UserAdmin)
```

> [참고] AbstractUser  
관리자 권한과 함께 완전한 기능을 가지고 있는 User Model을 구현하는 추상 기본클래스  
> ##### Abstract base class(추상 기본 클래스)
> - 몇 가지 공통 정보를 여러 다른 모델에 넣을 때 사용되는 클래스
> - 본인은 테이블에 올라가지 않지만, 다른 하위 클래스에게 기능을 상속해 주는 목적 (= 데이터베이스 테이블을 만드는 데 사용되지 않으며, 대신 다른 모델의 기본 클래스로 사용되는 경우, 해당 필드가 하위 클래스의 필드에 추가됨)


### 데이터베이스 초기화하는 법
데이터 베이스 초기화 후 마이그레이션 (프로젝트 중간일 경우)  
1. migration 파일 삭제
    - migration 폴더 및 \__init__.py는 삭제하지 않음
    - 번호가 붙은 파일만 삭제한다고 보면 됨
2. db.sqlite3 삭제
3. migrations 진행
    - $ python manage.py makemigrations
    - $ python manage.py migrate

> ##### 반드시 User 모델을 대체해야하는가?
- Django는 새 프로젝트를 시작하는 경우 비록 기본 User모델이 충분하더라도 **커스텀 User모델을 설정**하는 것을 강력 권고
- 커스텀 User모델은 기본 User모델과 동일하게 작동하면서도 필요한 경우 나중에 맞춤 설정할 수 있기 때문
    - 단 User모델 대체 작업은 프로젝트의 모든 migrations 혹은 첫 migrate를 실행하기 전에 마쳐야 함


## HTTP Cookies
### HTTP(Hyper Text Transfer Protocol)  
HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는 프로토콜(규약, 규칙)  
- WEB(WWW)에서 이루어지는 데이터 교환의 기초  
= 클라이언트-서버 프로토콜
- 요청(requests): 클라이언트(브라우저)에 의해서 전송되는 메시지
- 응답(response): 서버에서 응답으로 전송되는 메시지
#### HTTP 특징
1. 비연결지향(connectionless)
- 서버는 요청에 대한 응답을 보낸 후 연결을 끊음
    - 우리는 네이버의 메인 페이지를 보고 있을 때 계속 네이버와 연결이 되어 있는 것이 아니라 우리는 네이버에 데이터를 요청하고 네이버는 우리에게 메인 페이지 데이터를 보내주고(응답) 연결을 끊음

2. 무상태(stateless)
- 연결을 끊는 순간 클라이언트와 서버 간의 통신은 끝나며 상태정보가 유지되지 않음
- 클라이언트와 서버가 주고받는 메시지들은 서로 완전히 독립적

##### 그러면 어떻게 로그인 상태를 유지하는 걸까?
우리가 웹 사이트를 이동해도 로그인 상태는 유지됨  
-> 서버와 클라이언트 간의 지속적인 상태 유지를 위하여 **쿠키와 세션**이 존재함

### 쿠키
HTTP 쿠키는 상태가 있는 세션을 만들도록 해 줌
- 쿠키 생명(Lifetime)
1. Session Cookie
2. Persistent Cookie

### 세션
사이트와 특정 브라우저 사이의 'state'(상태)를 유지시키는 것 


## Authentication in Web requests

### AuthenticationForm
로그인을 위한 built-in form  
로그인하고자 하는 사용자의 정보를 얻음  
 데이터가 유효한지 검증  

### Login
#### login()
`login(request, user, backend=None)`  
인증된 사용자를 로그인시키는 로직으로 view 함수에서 사용됨  
현재 세션에 연결하려는 인증된 사용자가 있는 경우 사용  

### Logout
유저의 세션을 삭제
#### logout()
`logout(request)`  
HTTPRequest 객체를 인자로 받고 반환값이 없음  
사용자가 로그인 하지 않은 경우에도 오류를 발생시키지 않음  
1. 현재 요청에 대한 session data를 DB에서 삭제
2. 클라이언트의 쿠키에서도 session_id를 삭제  
   
다른 사람이 동일한 웹 브라우저를 사용하여 로그인하고, 이전 사용자의 세션 데이터에 액세스하는 것을 방지하기 위함  


```python
# accounts/views.py
from django.shortcuts import render, redirect
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import logout as auth_logout

def logout(request):
    auth_logout(request)
    return redirect('articles:index')
```
```python
# accounts/urls.py
from django.urls import path
from . import views

app_name = 'accounts'
urlpatterns=[
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout'),
]
```
```django
<!-- base.html -->
<form action="{% url 'accounts:logout' %}" method="POST">
    {% csrf_token %}
    <input type="submit" value="logout">
</form>
```

## Authentication with User
User Object와 User CRUD   
- 회원가입, 회원탈퇴, 회원정보수정, 비밀번호 변경

### 회원가입
User - Create  / UserCreationForm built-in form을 사용  
#### UserCreationForm  
주어진 username과 password로 권한이 없는 새 유저를 생성하는 ModelForm
- username(from the user model)
- password1
- password2


### 커스텀 유저 모델을 사용하려면 다시 작성하거나 확장해야하는 forms
1. UserCreationForm
2. UserChangeForm  

두 form 모두 class Meta: model = User가 등록된 form이기 때문에 반드시 확장 및 커스텀 하여야 함