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


## CSS
Cascading Style Sheet  
스타일을 지정하기 위한 언어 `선택하고, 스타일을 지정한다.`  

CSS 구문은 `선택자`를 통해 스타일을 지정할 HTML 요소를 선택함  
각 쌍은 선택한 요소의 속성, 속성에 부여할 값을 의미함  
- 속성(property) : 어떤 스타일 기능을 변경할지를 선택
- 값(value) : 어떻게 스타일 기능을 변경할지를 선택

#### CSS 정의 방법
- 인라인(inline)
- 내부참조(embedding) - < style >< / style >
- 외부참조(link file) - < head >< link href="링크" rel="stylesheet" ></ head >

### CSS 선택자
> - 기본 선택자
>     - 전체 선택자, 요소 선택자
>     - 클래스 선택자, 아이디 선택자, 속성 선택자
> - 결합자(Combinators)
>     - 자손 결합자, 자식 결합자
>     - 일반 형제 결합자, 인접 형제 결합자
> - 의사 클래스 / 요소(Pseudo Class)
>     - 링크, 동적 의사 클래스
>     - 구조적 의사 클래스, 기타 의사 클래스, 의사 엘리먼트, 속성 선택자

- 요소 선택자  
HTML 태그를 직접 선택
- 클래스 선택자  
`.`로 시작하며 해당 클래스가 적용된 항목을 선택
- 아이디 선택자   
`#`로 시작하며, 해당 아이디가 적용된 항목을 선택   
일반적으로 하나의 문서에 1번만 사용  
여러번 사용하여도 동작은 하지만, 단일 id를 사용하는 것을 권장함  

#### CSS 적용 우선 순위(cascading order)  
1. 중요도(importance) - 사용시 주의  
`!important`
2. 우선순위(specifycity)  
`인라인 > id > class, 속성, pseudo-class > 요소, pseudo-element`
3. CSS 파일 로딩 순서


#### CSS 상속  
CSS는 상속을 통해 부모 요소의 속성을 자식에게 상속  
속성(property) 중에는 상속이 되는 것과 되지 않는 것이 있음  
- 상속 O
    - font, color, text-align, opacity, visibility ... 
- 상속 X
    - width, height, margin, padding, border, box-sizing, display(box model 관련 요소), position, top/right/bottom/left, z-index ... (position 관련 요소)

### CSS 기본 스타일

#### 크기 단위
- px  
모니터의 해상도의 한 화소인 '픽셀'기준  
배수 단위, 요소에 지정된 사이즈에 상대적인 사이즈를 가짐 

- %  
백분율 단위  
가변적인 레이아웃에서 자주 사용

- em  
(바로 위, 부모요소에 대한)상속의 영향을 받음  
배수 단위, 요소에 지정된 사이즈에 상대적인 사이즈를 가짐

- rem  
(바로 위, 부모요소에 대한)상속의 영향을 받지 않음  
최상위 요소(html)의 사이즈를 기준으로 배수 단위를 가짐  

- 크기 단위(viewport)  
웹 페이지를 방문한 유저에게 바로 보이게 되는 웹 컨텐츠의 영역(device 화면)  
디바이스의 viewport를 기준으로 상대적인 사이즈가 결정됨    
브라우저의 크기에 따라 크기가 변함  
vw, vh, vmin, vmax

- 색상 관련  
색상 키워드(red, black..), RGB 색상(rgb(0, 255, 0);), RGBA 색상(a는 투명도)   
HSL 색상 (background-color: hsl(0%, 100%, 50%);)   
색상, 채도, 명도를 통해 특정 색을 표현하는 방식  

### CSS 결합자(Combinators)
- 자손 결합자(' ')
    - selectorA 하위의 모든 selectorB 요소
- 자식 결합자( > )
    - selectorA 바로 아래의 selectorB 요소
- 일반 형제 결합자( ~ )
    - selectorA 형제 요소 중 뒤에 위치하는 모든 selectorB 요소
- 인접 형제 결합자( + )
    - selectorA 형제 요소 바로 뒤에 위치하는 selectorB 요소

### Box Model
- margin: 테두리 바깥의 외부 여백(배경색 지정X)
- border: 테두리
- padding: 테두리 안쪽의 내부 여백(배경색 지정O)
- content: 글이나 이미지 등 요소의 실제 내용

> #### box-sizing
- 기본적으로는 모든 요소의 box-sizing은 `content-box`  
padding을 제외한 순수 contents 영역만을 box로 지정  
- but, 일반적으로 영역을 볼 때에는 border까지의 너비를 보는 것을 원함  
`box-sizing : border-box` 로 지정  

### display
display에 따라 박스모델의 크기와 배치가 달라짐  

- display: block
    - 줄바꿈이 일어나는 요소  
    - 화면 크기 전체의 가로 폭을 차지  
    - 블록 레렙 요소 안에 인라인 레벨 요소가 들어갈 수 있음  
- display: inline
    - 줄바꿈이 일어나지 않는 행의 일부 요소  
    - content 너비만큼 가로 폭을 차지함  
    - width, height, margin-top, margin-bottom을 지정할 수 없음 
    - 상하여백은 line-height로 지정  

- 블록레벨요소 예시
    - div, ul ol, li, p, hr, form ... 
- 인라인레벨요소 예시
    - span, a, img, input, label, b, em, i, strong ...  


- display: inline-block
    - block과 inline레벨 요소의 툭징을 모두 가짐
    - inline처럼 한줄에 표시할 수도 있고, block처럼 width, height, margin 속성을 모두 지정할 수 있음 
- display: none 
    - 해당 요소를 화면에 표시자히 않고, 공간조차 부여되지 않음
    - hidden 과 비교

### CSS Position
문서상의 요소 위치를 지정
- static: 모든 태그의 기본 값(기준 위치)
    - 일반적인 요소의 배치 순서에 따름(좌측 상단)
    - 부모 요소 내에 배치될 때는 부모 요소의 위치를 기준으로 배치됨

1. relative : 상대 위치
- 자기 자신의 static 위치를 기준으로 이동(normal flow 유지)
- 레이아웃에서 요소가 차지하는 공간은 static일 때와 같음(normal position 대비 offset)
2. absolute : 절대 위치
- 요소를 일반적인 문서 흐름에서 제거 후 레이아웃에 공간을 차지하지 않음(normal flow에서 벗어남) 
- static이 아닌 가장 가까운 부모/조상요소를 기준으로 이동(없는 경우, 브라우저 화면 기준으로 이동)
3. fixed : 고정 위치 
- 요소를 일반적인 문서 흐름에서 제거 후 레이아웃에 공간을 차지하지 않음(normal flow에서 벗어남) 
- 부모 요소와 관계없이 viewport를 기준으로 이동함  
- 스크롤 시에도 항상 같은 곳에 위치
4. sticky : 스클롤에 따라 static -> fixed로 변경  
- 속성을 적용한 박스는 평소에 문서 안에서 position: static 상태와 같이 일반적인 흐름에 따르지만 스크롤 위치가 임계점에 닿으면 position:fixed와 같이 박스를 화면에 고정할 수 았는 속성  
e.g. 하단에 고정되어 있다가 스크롤과 함께 이동하여 어느정도에 다다르면 상단에 고정되는 상단 이동 버튼

> #### position으로 위치의 기준을 변경
> - relative: 본인의 원래 위치
> - absolute: 특정 부모의 위치
> - fixed: 화면의 위치
> - sticky: 기본적으로 static , 스크롤 이동에 따라 fixed로 변경ㄴ