# Fixtures
Fixtures를 사용해 모델에 초기 데이터를 제공하는 방법  
- 기본 경로  
`app_name/fixtures`  
Django는 설치된 모든 app의 디렉토리애서 fixtures 폴더 이후로 fixtures파일을 찾는다  
- 생성(추출) `dumpdata`
    - 응용 프로그램과 관련된 데이터베이스의 모든 데이터를 표준 출력으로 출력  
    - 여러 모델을 하나의 json 파일로 만들 수 있음 
    - 후에 각 앱 폴더 안에 fixtures폴더를 만들고 해당 json 파일들을 해당 폴더에 넣어줌
```shell
python manage.py dumpdata [app_name][.Model_name][app_name][.Model_name]... > {file_name}.json
```
```python
# example
python manage.py dumpdata articles.article > articles.json
# python manage.py dumpdata --indent 4 articles.article > articles.json
```
- 로드 `loaddata`
```shell
python manage.py loaddata {file_name}.json
```
```python
# example
python manage.py loaddata articles.json
```