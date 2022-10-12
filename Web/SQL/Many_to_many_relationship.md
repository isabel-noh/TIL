# M : N관계(Many to Many Relationship)
M:N   
한 테이블의 9개 이상의 레코드가 다른 테이블의 0개 이상의 레코드와 관련된 경우  
양쪽 모두에서 N:1의 관계를 가짐  

> [참고] 데이터 모델링  
> 주어진 개념으로부터 논리적인 데이터 모델을 구성하는 작업  
> 물리적인 데이터베이스 모델로 만들어 고객의 요구에 따라 특정 정ㅇ보 시스템의 데이터베이스에 반영하는 작업  

- target model : 관계 필드를 가지지 않은 모델
    - N:1관계에서의 외래 키를 가지지 않은 모델 - Article
- source model : 관계 필드를 가진 모델
    - N:1관계에서의 외래 키를 가진 모델 - Comment

#### N : 1의 한계 
```python
In [1]: doctor1 = Doctor.objects.create(name='alice')

In [2]: doctor2 = Doctor.objects.create(name='bella')

In [3]: patient1 = Patient.objects.create(name='carol', doctor=doctor1)

In [4]: patient2 = Patient.objects.create(name='peter', doctor=doctor2)

In [9]: patient3 = Patient.objects.create(name='carol', doctor=doctor2)
```
- 동일한 환자임에도 다른 의사에게 예약하기 위해서는 객체를 새로 생성해서 예약을 진행해야 함 
    - 새로운 환자 객체를 생성할 수 밖에 없음  
- 외래 키 컬럼에 1, 2 형태로 참조하는 것은 integer 타입이 아니기 때문에 불가능함  
- then, 예약테이블을 생성하자

### 중개 모델
- 환자 모델의 외래 키를 삭제하고 별도의 예약모델을 새로 작성 
- 예약 모델은 의사와 환자에 각각 N:1 관계를 가짐

```python
# hospital / models.py
from django.db import models

# Create your models here.
class Doctor(models.Model):
    name = models.TextField()

    def __str__(self):
        return f'{self.pk}번 의사 {self.name}'


class Patient(models.Model):
    # doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    name = models.TextField()

    def __str__(self):
        return f'{self.pk}번 환자 {self.name}'

class Reservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
    
    def __str__(self):
        return f'{self.doctor_id}번 의사의 {self.patient_id}번 환자'
```
```python
In [1]: doctor1 = Doctor.objects.create(name='alice')

In [2]: patient1 = Patient.objects.create(name='carol')

In [3]: Reservation.objects.create(doctor=doctor1, patient=patient1)
Out[3]: <Reservation: 1번 의사의 1번 환자>
```

```python
# 의사의 역참조(의사1번에게 어떤 예약들이 잡혀있는지)
In [8]: doctor1.reservation_set.all()
Out[8]: <QuerySet [<Reservation: 1번 의사의 1번 환자>, <Reservation: 1번 의사의 2번 환자>]>
# 환자의 역참조(환자1번이 예약한 병원 예약들)
In [5]: patient1.reservation_set.all()
Out[5]: <QuerySet [<Reservation: 1번 의사의 1번 환자>]>
```

### Django ManyToManyField
- 환자 모델에 Django ManyToManyField 작성
- **주의! model 변경시, migrations파일 삭제 및 db.sqlite3 파일 삭제 하여야 함**
```python
# hospital / models.py
from django.db import models

# Create your models here.
class Doctor(models.Model):
    name = models.TextField()

    def __str__(self):
        return f'{self.pk}번 의사 {self.name}'


class Patient(models.Model):
    doctors = models.ManyToManyField(Doctor)
    name = models.TextField()

    def __str__(self):
        return f'{self.pk}번 환자 {self.name}'

# class Reservation(models.Model):
#     doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
#     patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
    
#     def __str__(self):
#         return f'{self.doctor_id}번 의사의 {self.patient_id}번 환자'
```
- Reservation class를 생성하지 않아도 ManyToManyField를 사용함으로써 hospital_patient_doctors 자동으로 중개테이블이 생성됨  
- `models.ManyToManyField`는 Doctor에 써도 되고, Patient에 써도 됨. 기능상으로는 전혀 차이가 없으나 차후에 Doctor과 Patient의 관계에서 models.ManyToManyField를 쓴 쪽이 사용하지 않은 쪽을 참조, 안 쓴 쪽이 사용한 쪽을 역참조하여야 함. (위의 경우 Patient가 Doctor을 참조, Doctor이 Patient를 역참조함)

```python
In [1]: doctor1 = Doctor.objects.create(name='alice')

In [2]: patient1 = Patient.objects.create(name='carol')

In [3]: patient2 = Patient.objects.create(name='catherine')

In [4]: patient1.doctors.all()
Out[4]: <QuerySet []>
# 환자가 의사를 예약함
In [5]: patient1.doctors.add(doctor1)
# 참조
In [6]: patient1.doctors.all()
Out[6]: <QuerySet [<Doctor: 1번 의사 alice>]>
# 역참조
In [7]: doctor1.patient_set.all()
Out[7]: <QuerySet [<Patient: 1번 환자 carol>]>
# 의사가 환자를 예약잡아줌
In [8]: doctor1.patient_set.add(patient2)
# 역참조 
In [10]: doctor1.patient_set.all()
Out[10]: <QuerySet [<Patient: 1번 환자 carol>, <Patient: 2번 환자 catherine>]>
```

- 예약 취소하기
```python
# 의사가 환자 예약 취소 (역참조)
In [11]: doctor1.patient_set.remove(patient1)
# 환자가 예약 취소 (참조)
In [12]: patient2.doctors.remove(doctor1)
```

**Django는 ManyToManyField를 통해 중개 테이블을 자동으로 생성함**  




## ManyToManyField()
ManyToManyField(to, **options)  
- 다대다 관계 설정 시 사용하는 모델 필드 
- 하나의 필수 위치인자(M:N 관계로 설정할 모델 클래스)가 필요
- 모델 필드의 RelatedManager를 사용하여 관련 개체를 추가, 제거 혹은 생성할 수 있음  
    - add(), remove(), create(), clear().. 

### related_name
target model이 source model을 역참조 시의 manager name을 정함  
== ForeignKey()의 related_name
```python
class Patient(models.Model):
    # related_name 작성
    doctors = models.ManyToManyField(Doctor, related_name='patients')
    name = models.TextField()

    def __str__(self):
        return f'{self.pk}번 환자 {self.name}'
```
전에는 patient_set으로 역참조를 해주었지만 related_name을 사용하여서 related_name인 'patients'로 역참조를 하게 변경할 수 있음
```python
In [1]: doctor1 = Doctor.objects.create(name='alice')

In [3]: patient1 = Patient.objects.create(name='chong')

In [4]: doctor1.patients.add(patient1)
```

### through
중개 테이블을 수동으로 지정하려는 경우, `through` 옵션을 사용하여 사용하려는 중개 테이블을 나타내는 Django model을 지정할 수 있음  
- 일반적으로 `중개 테이블에 추가 데이터를 사용` 하여 다대다 관계와 연결하려는 경우 사용된다  
```python
from django.db import models

class Doctor(models.Model):
    name = models.TextField()

    def __str__(self):
        return f'{self.pk}번 의사 {self.name}'


class Patient(models.Model):
    doctors = models.ManyToManyField(Doctor, related_name='patients', through='Reservation')
    name = models.TextField()

    def __str__(self):
        return f'{self.pk}번 환자 {self.name}'

class Reservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
    symptom = models.TextField()
    reserved_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f'{self.doctor_id}번 의사의 {self.patient_id}번 환자'
```

- 추가 데이터를 사용하여 다대다 관계 생성 - 예약 생성
`through_defaults={'key':'value'}`
```python
# Reservation 중개 테이블을 통해 예약 생성
In [4]: reservation1 = Reservation.objects.create(doctor=doctor1, patient=patient1, symptom='headache')
In [5]: reservation1.save()
# 환자 입장에서의 예약 생성
In [8]: patient2.doctors.add(doctor1, through_defaults={'symptom':'flu'})
```

### symmetrical
- 기본 값: True
- 동일한 모델(on self)을 가리키는 정의(재귀적 참조)에서만 사용
```python
# example
class Person(models.Model):
    # A가 B랑 친구야! > B도 A랑 친구야! 
    friends = models.ManyToManyField('self')
    # A가 B랑 친구야! > B도 A랑 친구야 ? ? ? 아닐걸 (대칭이 아닌 관계 )
    # friends = models.ManyToManyField('self', symmetrical=False)
```
- True일 경우, _set매니저를 추가하지 않음 
- source 모델의 인스턴스가 target 모델의 인스턴스를 참조하면 자동으로 target 모델 인스턴스도 source 모델 인스턴스를 자동으로 참조하도록 함(대칭)
- 대칭을 원하지 않는 경우 False로 설정
    - Follow 기능 구현과 관련

### Related Manager
Django는 모델간 N:1 혹은 M:N 관계가 설정되면 역참조시에 사용할 수 있는 manager을 생성함   
- 모델 생성시에 사용했던 `objects`라는 매니저를 통해 queryset api를 사용했던 것처럼 related manager을 통해 queryset api를 사용할 수 있음  
- 같은 이름의 메서드여도 각 관계에 따라 다르게 사용 및 동작 됨 
    - N:1에서는 target model 객체만 사용가능
    - N:M에서는 관련된 두 객체에서 모두 사용가능
- 메서드 종류 
    - add(), remove(), create(), clear(), set() ... 

#### Methods(N:M 관계 기준)
##### add()
지정된 객체를 관젼 객체 집합에 추가  
이미 존재하는 관계에 사용하면 관계가 복제되지 않음  
모델 인스턴스, 필드값PK를 인자로 허용  

##### remove()
관련 객체 집합에서 지정된 모델 개체를 제거  
내부적으로는 QuerySet.delete()를 사용하여 관계를 삭제함  
모델 인스턴스, 필드값PK를 인자로 허용  

#### 중개 테이블 필드 생성 규칙
1. source model 및 target model이 다른 경우
- id
- <containing_model>_id
- <other_model>_id
2. ManyToManyField가 동일한 모델을 가리키는 경우
- id
- `from_<model>_id`
- `to_<model>_id`

## LIKE 좋아요 기능 구현하기
### 모델 관계 설정
```python
class Article(models.Model):
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    likes_users = models.ManyToManyField(settings.AUTH_USER_MODEL)
    title = models.CharField(max_length=10)
    content = models.TextField()
```
makemigrations 이후 에러 발생! 
```python
ERROR
articles.Article.likes_users: (fields.E304) Reverse accessor for 'articles.Article.likes_users' clashes with reverse accessor for 'articles.Article.user'.
        HINT: Add or change a related_name argument to the definition for 'articles.Article.likes_users' or 'articles.Article.user'.
articles.Article.user: (fields.E304) Reverse accessor for 'articles.Article.user' clashes with reverse accessor for 'articles.Article.likes_users'.
        HINT: Add or change a related_name argument to the definition for 'articles.Article.user' or 'articles.Article.likes_users'.
```
- like_users 필드 생성 시 자동으로 역참조에는 '.article_set'매니저가 생성됨 
- 하지만 이전 N:1(article-user)관계에서 이미 해당 매니저를 사용중임 
    - user.article_set.all() : 해당 유저가 작성한 모든 게시글 조회
    - user가 작성한 글들(user.article_set)과 user과 좋아요를 누른 글(user.article_set)을 구분할 수 있어야 함 
- user과 관계된 ForeignKey 혹은 ManyToManyField 중 하나에 `related_name을 작성해야 함`
```python
    likes_users = models.ManyToManyField(settings.AUTH_USER_MODEL, related_name='like_articles')
```

---
- User-Article 간 사용가능한 related manager 정리
    - article.user - 게시글을 작성한 유저 N :1
    - user.article_set - 유저가 작성한 게시글(역참조) N:1 
    - article.like_users - 게시글을 좋아요 한 유저 M:N
    - user.like_articles - 유저가 좋아요 한 게시글(역참조) M:N