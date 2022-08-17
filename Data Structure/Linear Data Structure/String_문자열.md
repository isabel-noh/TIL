# 문자열
1967년 미국에서 ASCII(American Standard Code for Information Interchange)라는 문제 인코딩 표준 제정  
ASCII : 7bit 인코딩으로 128문자를 표현하며 33개의 출력 불가능한 제어문자들과 공백을 비롯한 95개의 출력가능한 문자들로 이루어짐  
확장 아스키 : 표준 문자 이외의 악센트 문자, 도형문자, 특수문자, 특수기호 등 부가적인 문자를 128개 추가할 수 있게 하는 부호  

[참고]
strlen()함수 만들어보기
```python
def strlen(a): # '\0'을 만나면 '\0'을 제외한 글자수를 리턴하는 함수를 만들어보세요
    # while문을 활용
    idx = 0
    # while a[idx] != '\0':
    #     idx += 1
    while 1:
        if a[idx] == '\0':
            return idx
        idx += 1
a = ['a', 'b', 'c', '\0']
print(strlen(a))
```
### python에서 문자열 처리
- char 타입 없음 
- 텍스트 데이터의 취급방법이 통일되어있음  
- 문자열 기호
    - '', "", ''' ''', """ """
    - '+' 연결(Concatenation) : 문자열 + 문자열 이어붙여주는 역할
    - '\*' 반복 : 문자열* 수 : 수만큼 문자열 반복
    
문자열은 sequence 자료형 
indexing, slicing 가능
immutable
replace(), find(), split(), isalpha(),



### 패턴 매칭에 사용되는 알고리즘
- 고지식한 패턴 검색 알고리즘
- 카프-라빈 알고리즘
- KMP 알고리즘
- 보이어-무어 알고리즘


## KMP 알고리즘
매칭이 실패했을 때 돌아갈 곳을 계산한다.  
