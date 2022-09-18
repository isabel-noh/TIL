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

##### get_user_model()  
'현재 프로젝트에서 활성화된 유저 모델(active user model)'을 반환  
Django는 직접 User Model을 참조하지 않고 `get_user_model()`을 사용하기를 강력 권고
- 직접 User Model을 참조하지 않는 이유? 
    - e.g. 기존 User Model이 아닌 User Model을 커스텀한 경우, 커스텀 User Model을 자동으로 반환하여 주기 때문  



>[참고] UserCreationForm의 save()메서드  
>- user을 반환
>```python
>def save(self, commit=True):
>    user = super().save(commit=False)
>    user.set_password(self.cleaned_data["password1"])
>    if commit:
>        user.save()
>    return user
>```

ㄴㅇㄹ호ㅓㅏㅣ


> [참고] 탈퇴하면서 해당 유저의 세션정보도 함께 지우고 싶은 경우 
>```python
>def delete(request):
>    request.user.delete()
>    # 회원탈퇴할 때 로그아웃하고 탈퇴하려는 경우
>    auth_logout(request)
>    return redirect('articles:index')
>```
> 로그아웃을 먼저 하게 되면 해당 요청 객체의 정보가 먼저 없어져버리기 때문에 탈퇴에 필요한 유저 정보도 삭제되어 버림


### 회원정보 수정
회원정보 수정은 User정보를 Update하는 것이며 UserChangeForm built-in form 사용  
#### UserChangeForm
- 사용자의 정보 및 권한을 변경하기 위해 admin Interface에서 사용되는 ModelForm
- UserChangeForm 또한 ModelForm이기 때문에 instance 인자로 기존 User정보를 받는 구조 또한 동일 
- 이미 이전에 CustomerUserChangeForm으로 확장했기 때문에  CustomerUserChangeForm 사용 
```python
# urls.py
path('update/', views.update, name='update'),

# views.py
def update(request):
    if request.method == 'POST':
        form = CustomUserChangeForm(request.POST, instance=request.user) # modelForm의 첫번째 인자 - data > 여기서는 request.POST
        if form.is_valid():
            form.save()
            return redirect('articles:index')

    else:
        form = CustomUserChangeForm(instance=request.user)
    context = {
        'form': form,
    }
    return render(request, 'accounts/update.html', context)

# forms.py
class CustomUserChangeForm(UserChangeForm):
    class Meta(UserChangeForm.Meta):
        # django는 User을 직접 참조하는 것을 꺼림
        model = get_user_model()
        # 회원정보설정 페이지에서 보여주고싶은 요소를 지정 (원래 form에서는 최상위 사용자 권한 등 너무 다 보여주기 때문에 보여주고 싶은 요소만 선택지정)
        fields = ('email','first_name','last_name',)
```
```django
<!-- update.html -->
{% extends 'base.html' %}

{% block content %}
<h1>UPDATE_ACCOUNT</h1>
<form action="{% url 'accounts:update' %}" method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit">
</form>
{% endblock content %}

```
> [참고] UserChangeForm 사용시 문제점 
> - 일반 사용자가 접근하면 안되는 정보들(fields)까지 모두 수정이 가능해짐
>   - admin interface에서 사용하는 model form이기 때문 
> - 따라서 UserChangeForm을 상속받아 작성해 두었던 서브 클래스 CustomerUserChangeForm에서 접근가능한 필드를 수정하여야 함

### 비밀번호 변경 
#### PasswordChangeForm
- 사용자가 비밀번호를 변경할 수 있도록 하는 form
- 이전 비밀번호 입력 > 비밀번호 변경 
- SetPasswordForm(이전 비밀번호 입력 불요)를 상속받는 subclass
```python
# accounts/views.py
def change_password(request):
    if request.method == 'POST':
        form = PasswordChangeForm(request.user, request.POST)
        if form.is_valid():
            form.save()
            return redirect('articles:index')
    else:
        form = PasswordChangeForm(request.user)
    context = {
        'form': form,
    }
    return render(request, 'accounts/change_password.html', context)

# accounts/urls.py
from django.urls import path
from . import views

app_name = 'accounts'
urlpatterns=[
    ...
    path('password/', views.change_password, name='change_password'),
]

```
```django
<!-- accounts/change_password.html -->
{% extends 'base.html' %}

{% block content %}
  <h1>Change_Password</h1>
  <form action="{% url 'accounts:change_password' %}" method="POST" >
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit">
  </form>
{% endblock content %}
```

#### 암호 변경시 세션 무효화 방지하기
비밀번호가 변경되면 기존 세션과 회원정보가 일치하지 않게 되어 로그인 상태가 유지되지 못함   
##### update_session_auth_hash()
- update_session_auth_hash(request, user)
- 현재 요청(current request)과 새 session data가 파생될 업데이트된 사용자 객체를 가져오고, session data를 적절히 업데이트 함
- 암호가 변경되어도 로그아웃되지 않도록 새로운 password의 session data로 session update

```python
from django.contrib.auth import update_session_auth_hash

def change_password(request):
    if request.method == 'POST':
        form = PasswordChangeForm(request.user, request.POST)
        if form.is_valid():
            form.save()
            #
            update_session_auth_hash(request, form.user)
            #
            return redirect('articles:index')
    else:
        ...
```

### Limiting access to logged_in users
로그인 사용자에 대한 접근 제한  
1. The row way
    - `is_authenticated` attribute
2. The `login required` decorator

#### is_authenticated
- User model 속성 중 하나
- 사용자가 인증되었는지 여부 확인하는 방법
- 모든 User 인스턴스에 대해 항상 True인 읽기 전용 속성
    - Anonymous User에 대해서는 항상 False
- 일반적으로 request.user에서 이 속성을 사용(request.user.is_authenticated)
- **권한 permission과는 관련이 없으며, 사용자가 활성화active상태이거나 유효한 세션valid session을 가지고 있는지도 확인하지 않음**
> ```python
> class AbstractBaseUser(models.Model):
>    ...
>    def is_authenticated(self):
>    # Always returns True. This is a way to tell if the user has been _authenticated in templates.
> ```

- 로그인 여부에 따라 화면 구성을 달리하기 
```django
<!-- base.html -->
 <!-- 로그인된 사용자에게 보여줄 요소 -->
{% if request.user.is_authenticated %} 
<!-- 여기 위의 request는 settings.py / TEMPLATES / OPTIONS / django.template.context_processors.request 임 -->
    <h3>{{ user }}</h3>
    <form action="{% url 'accounts:logout' %}" method="POST">
        {% csrf_token %}
     <input type="submit" value="logout">
    </form>
    <form action="{% url 'accounts:delete' %}" method="POST">
        {% csrf_token %}
        <input type="submit" value="DELETE_ACCOUNT">
    </form>
    <a href="{% url 'accounts:update' %}">EDIT_ACCOUNT</a>
<!-- 비로그인 사용자에게 보여줄 요소 -->
{% else %}
    <a href="{% url 'accounts:signup' %}">Signup</a>
    <a href="{% url 'accounts:login' %}">Login</a>
{% endif %}
```
- 로그인된 회원이 로그인 시도시 메인화면으로 보내기
```python
def login(request):
    if request.user.is_authenticated:
        return redirect('articles:index')
    ...
```

#### login_required
- `@login_required` decorator
- 사용자가 로그인되어있으면 정상적으로 view함수 실행
- 로그인하지 않은 사용자의 경우 settings.py의 LOGIN_URL의 주소로 redirect
```python
# articles/views.py
from django.contrib.auth.decorators import login_required 

@login_required
@require_http_methods(['GET', 'POST'])  # GET, POST만 허용
def create(request):
    pass

@login_required
@require_http_methods(['GET', 'POST'])
def update(request, pk):
    pass
```

##### next query parameter
- /articles/create로 강제 접속 시도 -> 로그인 페이지로 리다이렉트 + url **(/accounts/login/?next=/articles/create/)**
- 인증 성공시 사용자가 redirect되어야하는 경로는 next라는 쿼리 문자열 매개변수에 저장됨 
- `next` query parameter : 로그인이 정상 진행되면 이전에 요청했던 주소로 redirect하기 위하여 Django가 제공하는 쿼리 스트링 파라미터
- 해당값을 처리할지 안할지는 자유이며 별도로 처리해주지 않으면 view에 설정한 redirect경로로 이동하게 됨
```python
def login(request):
    if request.user.is_authenticated:
        return redirect('articles:index')
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        # form = AuthenticationForm(request, data=request.POST)
        if form.is_valid():
            # 로그인
            auth_login(request, form.get_user())
            # return redirect('articles:index')
            # ------------------------------------
            return redirect(request.GET.get('next') or 'articles:index')
            # ------------------------------------
```
- [주의사항]  
만약 로그인 템플릿에서 form action이 작성되어 있다면 동작하지 않음  
해당 action주소가 next 파라미터가 작성되어 있는 현재 url이 아닌 '/accounts/login/'으로 요청을 보내게 되기 때문

##### 두 데코레이터로 인해 발생하는 구조적 문제
1. 먼저 비로그인상태로 게시물 삭제 시도 
2. delete view 함수의 @login_required로 인해 로그인 페이지로 redirect  
http://127.0.0.1:8000/accounts/login/?next=/articles/1/delete/
3. redirect로 이동한 페이지에서 로그인 
4. delete view 함수의 @require_POST로 인해 405 코드 발생  
405(Method Not Allowed) status code

> **두가지 문제 발생**  
> 1. redirect 과정에서 POST 요청 데이터 손실  
> 2. redirect로 인한 요청은 GET 요청 메소드로만 요청됨   
> @login_required는 GET request method를 처리할 수 있는 view 함수에서만 사용 

**해결방안**  
POST 메서드만 허용하는 delete 함수 내부에서는 is_authenticated()메서드 속성값을 활용하여 처리
```python
@require_POST # POST요청만 받도록 제한
def delete(request, pk):
    # ------------------------------------
    if request.user.is_authenticated:
    # ------------------------------------
        article = Article.objects.get(pk=pk)
        article.delete()
    return redirect('articles:index')
```