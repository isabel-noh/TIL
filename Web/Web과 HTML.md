# WEB
#### 웹 사이트 구성요소
- 웹 사이트: 브라우저를 통해서 접속하는 웹 페이지들의 모음
- 웹 페이지: 글, 그림, 동영상 등 여러 정보를 담고 있으며 마우스 클릭으로 다른 웹 페이지로 이동하는 '링크'들이 들어있음  
이 여러 웹 페이지들을 연결한 것이 웹 사이트

#### 웹 사이트와 브라우저
- 웹 사이트는 브라우저를 통해 동작
- 브라우저마다 동작이 달라서 문제가 생기는 경우 있음 (파편화) -> `웹 표준`으로 해결하고자 함

#### 웹 표준
- 웹에서 표준으로 사용되는 기술이나 규칙 
- 어떤 브라우저든 웹 페이지가 동일하게 보이도록 함(Cross Browsing)
- by W3C, WHATWG - HTML Living Standard


## HTML
웹 페이지를 작성(구조화)하기 위한 언어
##### Hyper Text
참조(하이퍼링크)를 통해 사용자가 한 문서에서 다른 문서로 즉시 접근할 수 있는 텍스트
##### Markup Language
태그 (예시 ) <html></html>) 등을 이용하여 문서나 데이터의 구조를 명시하는 언어

### HTMl 기본구조
- HTML : 문서의 최상단 요소 (root)
- head : 문서 metadata 요소
    - 문서 제목, 인코딩, 스타일, 외부 파일 로딩 등
    - 일반적으로 브라우저에 나타나지 않는 내용을 내포함
- body : 문서 본문 요소  
실제 화면 구성과 관련된 내용  

#### head 예시
- < title > : 브라우저 상단 타이틀
- < meta > : 문서 레벨 메타데이터 요소
- < link > : 외부 리소스 연결 요소(favicon, css 등)
- < script > : 스크립트 요소(Javascript file/code)
- < style > : css 직접 작성
- < meta property:"og:*****" > : Open Graph Protocol 
    - 메타데이터를 표현하는 새로운 규약   
    - HTML 문서의 메타 데이터를 통해 문서의 정보를 전달
    - 메타 정보에 해당하는 제목, 설명 등을 쓸 수 있도록 정의 

#### 요소(element)
HTML 요소는 태그와 내용(contents)로 구성됨  
`<h1> contents </h1>`  
- HTML 요소는 시작태그와 종료태그, 그리고 그 태그들 사이에 위차한 내용으로 구성
- element는 태그로 내용을 감싸는 것, 그 정보의 성격과 의미를 나타냄
    - 내용이 없는 태그들도 존재함(닫는 태그 없음)  
    - `<br /> <hr /> <img /> <input /> `... 
- 요소는 중첩될 수 있음
    - 요소 중첩을 통해 하나의 문서를 구조화 할 수 있음
    - 하지만 태그의 관계를 주의해야함. 디버깅이 힘들 수 있음

#### 속성(attribute)
`<a href="https://google.com"</a> `  
href : 속성명  
" " 안의 내용 : 속성값  

- 태그의 부가적인 정보를 설정할 수 있음
    - 요소는 속성을 가질 수 있으며, 경로나 사이즈 등을 설정할 수 있음
    - 보통 속성 이름과 속성값이 한 쌍으로 이루어져 있음

##### HTML Global Attribute
- 태그와 상관없이 사용가능한 속성도 있음 (HTML Global Attribute)
- 몇몇 요소에는 아무 효과가 없을 수도 있음
- id : 문서 전체에서 유일한 고유 식별자 지정
- class : 공백으로 구분된 해당 요소의 클래스의 목록
- data-* : 페이지에 개인 사용자 정의 데이터를 저장하기 위해 사용
- style : inline style
- title : 요소에 대한 추가 정보 지정
- tabindex : 요소의 탭 순서
 
#### 시맨틱 태그(semantic tag)
HTML 태그가 특정 목적, 역할 및 의미적 가치를 가지는 것  
- < div >< / div >, < span >< / span >은 non-semantic tag

##### 시멘틱 태그를 사용해야 하는 이유
- 의미론적 마크업
    - 개발자 및 사용자 뿐만 아니라 검색엔진 등의 의미있는 정보의 그룹을 태그로 표현  
    - 요소의 의미가 명확해 지기 때문에 코드의 가독성을 높이고 유지보수를 쉽게 함
    - 검색 엔진 최적화(SEO)를 위해서 메타태그, 시멘틱 태그 등을 통한 마크업을 효과적으로 활용  

> #### 텍스트로 작성된 코드가 어떻게 웹 사이트가 되는 걸까?
> ##### 렌더링(Rendering)
> 웹 사이트 코드를 사용자가 보게되는 웹사이트로 바꾸는 과정
> ##### 돔 트리(DOM Tree - Document Object Model)  
> 텍스트 파일인 HTML 문서를 브라우저에서 렌더링 하기위한 요소  
> HTML 문서에 대한 모델을 구성함  
> HTML 문서 내의 각 요소에 접근/수정에 필요한 프로퍼티와 메서드를 제공함  

#### HTML 문서 구조화
- 그룹 컨텐츠
    - `<pre></pre>` : HTML에 작성한 내용을 그대로 표현  
    보통 고정폭 글꼴이 사용되고 공백 문자를 유지
    - `<blockquote></blockquote>` : 텍스트가 긴 인용문  
    주로 들여쓰기를 한 것으로 표현됨

- form
    - `<form>`은 정보(데이터)를 서버에 제출하기 위해 사용하는 태그  
    - `<form>` 기본 속성
        - **action** : form을 처리할 서버의 URL(데이터를 보낼 곳)
        - **method** : form을 제출할 때 사용할 HTTP 메서드 (GET or POST)
        - **enctype** : method가 post인 경우 데이터의 유형
            - application/x-www-form-urlencoded : 기본값
            - multipart/form-data : 파일 전송시(input type='file'인 경우)
            - (text/plain : HTML5 디버깅용) - 잘 사용되지 않음

- input
    - 다양한 타입을 가지는 입력 데이터 유형과 위젯이 제공됨  
    - 대표 속성  
     name : form control에 적용되는 이름   
     value : form control에 적용되는 값  
     required, readonly, autofocus, autocomplete, disabled 등  
    - type으로 email,text, password, number, file, radio, checkbox, color, date 등이 있음
    
- input & label
    - label을 클릭하여 자동으로 input으로 focus가 가게 하거나 활성화시킬 수 있음
    - < label for= "" >과 < input id="" > 으로 둘의 관계를 연관시킬 수 있음  

