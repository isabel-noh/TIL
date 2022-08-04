
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

## Grid system
### Flexbox
[1분코딩 flex 참고](https://studiomeal.com/archives/197)  

#### CSS Flexible box Layout
행과 열의 형태로 아이탬들을 배치하는 1차원 레이아웃 모델  
- 축  
    - main axis(메인 축)
    - cross axis(교차 축)
- 구성 요소
    - Flex Container(부모 요소)
    - Flex Item(자식 요소)

`display: flex` : 부모의 요소(**Flex Container**)에 flex 선언  
* 부모 요소에 flex를 적용하지 않으면 그 아래 자식들에게 justify-content 등의 속성이 적용되지 않음  
* 기본 width: 내용물의 크기만큼으로 지정됨    

> ##### 비교 : flex vs inline-flex  
> - flex : Block 특성의 Flex Container를 정의  
> - inline-flex : Inline 특성의 Flex Container를 정의  
>`Flex Container(부모요소)`를 block으로 처리하여 한줄을 다 차지하고 다음 블럭을 >아래로 이어지게 하느냐 , inline으로 처리하여 다음 블럭이 옆에 오게 하느냐의 차이

#### flex-direction
main axis 기준 방향 설정
- row
- row-reverse
- column
- column-reverse

#### flex-wrap
아이템이 컨테이너를 벗어나는 경우, 해당 영역 내에 배치되도록 설정    
즉, 컨테이너 밖으로 벗어나지 않도록 함
- wrap (아이템이 컨테이너 밖을 벗어나게 되면, 줄내림을 하여 정렬함)
- wrap-reverse
- nowrap (아이템이 컨테이너 밖을 벗어나게 되면, 각 아이템의 width를 줄여서 컨테이너 안에 꽉 맞춤)

#### flex-flow
- flex-direction와 flex-wrap의 shorthand  
e.g. flex-flow: row nowwrap;

#### justify-content(main axis)
main axis를 기준으로 공간 배분  
- flex-start : 아이템들을 axis 시작점으로
- flex-end : 아이템들을 axis 끝점으로
- center 
- space-between
- space-around
- space-evenly
 
#### align-content(cross axis)
cross axis를 기준으로 공간 배분(아이템이 한 줄로 배치되는 경우 확인할 수 없음)
- flex-start
- flex-end
- center 
- space-between
- space-around
- space-evenly
 
#### align-items
모든 아이템들을 cross axis를 기준으로 정렬
- stretch
- flex-start
- flex-end
- center
- baseline

#### align-self
개별 아이템을 cross axis 기준으로 정렬  
**주의! 해당 속성은 container에 적용하는 것이 아니라 item에 적용**  
- stretch
- flex-start
- flex-end
- center 

##### 기타
- flex-grow: 남은 영역으로 아이템에 분배
- order : 배치 순서
```html
<div class="flex_item grow-1 order-3">1</div>
<div class="flex_item grow-1">2</div>
<div class="flex_item order-1">3</div>
<div class="flex_item order-2">4</div>
```

### Float 
박스를 오른쪽 혹은 왼쪽으로 이동시켜 텍스트를 포함하여 인라인 요소들이 주변을 wrapping 하게 함  
요소들이 normal flow를 벗어나게 함
```css
float: none; /*기본값*/
float: right; /*요소를 오른쪽에 띄움*/
float: left; /*요소를 왼쪽에 띄움*/
```

> #### box1에만 float을 적용하고, 그 아래에는 적용하고 싶지 않을 땐? 
```html
<head>
    <style>
        .left:{
            float: left;
        }
        .clearfix{ /*clearfix라는 클래스의 박스 외부의 float을 초기화하여줌*/
            content: "";
            display: block;
            clear: both; /*float 속성을 해제*/
        }
    </style>
</head>
<body>
    <header class="clearfix">
        <div class="box1 left">box1</div>
    </header>
    <div class="box2">box2</div>
    <div class="box3">box3</div>
    <div class="box4">box4</div>
</body>
```

## Bootstrap
#### CDN
- Content Delivery(Distribution) Network  
- 컨텐츠(CSS, JS, Image, Text 등)을 효율적으로 전달하기 위해 여러 노드에 가진 네트워크에 데이터를 제공하는 시스템  
    - 개별 end-user의 가까운 서버를 통해 빠르게 전달 가능(지리적 이점)  
    - 외부서버를 활용함으로써 본인 서버의 부하가 적어짐  

### spacing(Margin & Padding)
```html
<div class="mt-3 ms-5">bootstrap-spacing</div>  
<!-- m : property  
t : sides  
3 : size   
-> margin top 3 -->
```

- property
    - m : for classes that set *margin*
    - p : for classes that set *padding*
- sides
    - t : for classes that set *margin-top* or *padding-top*
    - b : for classes that set *bottom*
    - s : for classes that set *start point*
    - e : for classes that set *end point*
    - x : for classes that set *\*-left* and *\*-right*
    - y : for classes that set *\*-top* and *\*-bottom*
    - blank : for classes that set a margin or padding on *all 4 sides* of the elements
- size
    - 0 : for classes that eliminate the margin or padding by setting it to 0
    - 1 : (by default) for classes that set the margin or padding to \$spacer \* .25 (0.25rem)
    - 2 : (by default) for classes that set the margin or padding to \$spacer \* .5  (0.5rem)
    - 3 : (by default) for classes that set the margin or padding to \$spacer  (1rem)
    - 4 : (by default) for classes that set the margin or padding to \$spacer \* 1.5  (1.5rem)
    - 5 : (by default) for classes that set the margin or padding to \$spacer \* 3  (3rem)
    - auto : for classes that set the margin to auto

```
mx-0?   
가로(왼쪽, 오른쪽) margin 0  
mx-auto?  
수평 중앙 정렬, 가로 가운데 정렬   
py-0?
위 아래 padding 0
```

#### Responsive Web Design
- 다양한 화면 크기를 가진 디바이스들이 등장함에 따라 responsive web design 개념이 등장  
- 반응형 웹은 별도 기술 이름이 아니고 웹 디자인에 대한 접근 방식, 반응형 레잉아웃 작성에 도움이 되는 사례들의 모음 등을 기술하는 데 사용되는 용어
- e.g. Media Queries, Flexbox, Bootstrap Grid System, The viewport meta tag .. 

### Grid system
요소들의 디자인과 배치에 도움을 주는 시스템  
> - 기본요소  
> Column : 실제 컨텐츠를 포함하는 부분  
> Gutter : 칼럼과 칼럼 사이의 공간 (사이 간격)  
> Container : Column들을 담고 있는 공간  

부트스트랩 그리드 시스템은 flexbox로 제작됨  
container, rows, column으로 컨텐츠를 배치하고 정렬  
- **12개의 column**
- **6개의 grid breakpoints**

#### offset
열에 .col-*-offset-* class를 추가하면 오른쪽으로 열을 이동시킬 수 있다.  
`<div class="col-md-2 col-md-offset-4">`의 경우, viewport 너비가 992px 이상이면 .col-md-4 만큼 오른쪽으로 이동한 후 .col-md-2 만큼의 너비를 갖는 열을 표시한다.