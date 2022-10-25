### Browser APIs
웹 브라우저에 내장된 API로, 현재 컴퓨터 환경에 관한 데이터를 제공하거나 여러가지 유용하고 복잡한 일을 수행   
- DOM
- Geolocation API
- WebGL 등
# DOM
**문서 객체 모델 Document Object Model**   
- 문서의 구조화된 표현을 제공하며 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공
    - 문서 구조, 스타일, 내용 등으 변경할 수 있게 도움
    - HTML 콘텐츠를 추가, 제거, 변경하고, 동적으로 페이지에 스타일을 추가하는 등 HTML/CSS를 조작할 수 있음 
- 문서가 구조화되어 있으며 각 요소는 객체(object)로 취급
- 단순한 속성 접근, 메서드 활용 뿐만 아니라 프로그래밍 언어적 특성을 활용한 조작 가능 
---
- DOM은 문서를 논리 트리로 표현
- DOM 메서드를 사용하면 프로그래밍적으로 트리에 접근할 수 있고 이를 통해 문서의 구조, 스타일, 컨텐츠를 변경할 수 있음 
---
- 웹 페이지는 일종의 문서Document
- 이 문서는 웹 브라우저를 통해 그 내용이 해석되어 웹 브라우저 화면에 나타나거나 HTML 코드 자체로 나타나기도 함
- DOM은 동일한 문서를 표현하고, 저장하고, 조작하는 방법을 제공 
- DOM은 웹페이지의 객체 지향 표현이며, Javascript와 같은 스크립트 언어를 이용하여 DOM을 수정할 수 있음  

### Window object
- DOM을 표현하는 창 
- 가장 최상위 객체 (작성 시 생략 가능)
- 탭 기능이 있는 브라우저에서는 각각의 탭을 각각의 window객체로 나타냄 
```js
// window 객체
window
// Window {window: Window, self: Window, document: document, name: '', location: Location, …}

// 새 탭 열기
window.open()
// Window {window: Window, self: Window, document: document, name: '', location: Location, …}

// 경고 대화 상자 표시
window.alert()

// 인쇄 대화 상자 표시
window.print()
```

### document object
- 브라우저가 불러온 웹 페이지  
- 페이지 컨텐츠의 진입점 역할을 하며, `<body>` 등과 같은 수많은 다른 요소들을 포함하고 있음
```js
document // == window.document
document.title = 'ssafy' //document의 title 태그를 변경 
```
##### [참고] 파싱 Parsing
- 구문 분석, 해석
- 브라우저가 문자열을 해석하여 DOM tree로 만드는 과정

## DOM 조작
- Document가 제공하는 기능을 사용해 웹 페이지 문서 조작하기
- 선 선택 후 조작 
1. 선택(select)
2. 조작(manipulation)
    - 생성, 추가, 삭제 등

### 선택 관련 메서드 
- `document.querySelector(selector)`
    - 제공한 선택자와 일치하는 element 한 개 선택
    - 제공한 CSS selector를 만족하는 `첫 번째` element 객체를 반환
    - 없다면 null 반환
- `document.querySelectorAll(selector)`
    - 제공한 선택자와 일치하는 `여러` element 선택
    - 매칭할 하나 이상의 셀렉터를 포함하는 유효한 CSS selector를 인자(문자열)로 받음
    - 제공한 CSS selector를 만족하는 NodeList를 반환

```html
<body>
  <h1 id="title">DOM 조작</h1>
  <p class="text">querySelector</p>
  <p class="text">querySelectorAll</p>
  <ul>
    <li>Javascript</li>
    <li>Python</li>
  </ul>
<script>
    document.querySelector('#id')  // id가 title에 해당하는 element 선택
    console.log(document.querySelector('#title'))
    // <h1 id="title">DOM 조작</h1>

    document.querySelectorAll('.className') // className에 해당하는 element 모두 선택
    console.log(document.querySelectorAll('.text')
    // NodeList(2) [p.text, p.text]

    document.querySelector('.className')  // 첫번째 element 선택
    console.log(document.querySelector('.text'))
    // <p class="text">querySelector</p>

    document.querySelectorAll('ul > li ')  // ul 태그 아래의 li 태그들을 모두 선택
    document.querySelectorAll('body > ul > li ')  // copy selector을 통해 경로를 복사할 수 있음
    // NodeList(2) [li, li]
</script>
```
##### [참고] NodeList
- index로만 각 항목에 접근 가능
- 배열의 `forEach`메서드 및 다양한 배열 메서드 사용 가능
- querySelectorAll()에 의해 반환되는 NodeList는 DOM 변경사항을 실시간으로 반영하지 않음 
    - 경우에 따라, NodeList는 live collection으로 DOM의 변경사항을 실시간으로 콜렉션에 반영한다. (e.g. Node.childNodes는 live collection을 반환)
    - 하지만 다른 경우, 예를 들어 document.querySelectorAll()은 정적 collection을 반환한다. 
```js
liTags = document.querySelectorAll('body > ul > li ')
liTags.forEach((element) => {
    console.log(element)
})
```

### 조작 관련 메서드 (생성)
- `document.createElement(tagName)`
    - **작성한 tagName의 HTML요소를 생성하여 반환**
- `Node.innerText`
    - Node 객체와 그 자손의 텍스트 컨텐츠(DOMString)를 표현 - 해당 요소 내부의 raw text
    - 사람이 읽을 수 있는 요소만 남김
    - 줄바꿈을 인식하고 숨겨진 내용을 무시
    - 최종적으로 스타일링이 적용된 모습을 표현 
- `Node.appendChild()`
    - 위에서는 태그를 만들고 내용을 작성했지만 적용되지는 않음 -> 누군가의 자식으로 넣어줘야, 즉 appendChild()를 해줘야 적용이 됨
    - 한 Node를 특정 부모 Node의 자식 NodeList 중 마지막 자식으로 삽입 
    - 한번에 오직 하나의 Node만 추가할 수 있음
    - **추가된 Node 객체를 반환**
    - 만약 주어진 Node가 이미 문서에 존재하는 다른 Node를 참조한다면 현재 위치에서 새로운 위치로 이동
- `Node.removeChild()`
    - DOM에서 자식 Node를 제거
    - 제거된 Node를 반환

```js
// h1 요소 element 를 만들고
const title = document.createElement('h1')

// 텍스트를 추가하고
title.innerText = 'DOM 조작'

// 선택자로 div태그를 가져와서
const titleParent = document.querySelector('div')

// div 태그의 자식 요소로 추가
titleParent.appendChild(title)

// div 태그의 h1요소 삭제
titleParent.removeChild(title)
```

### 조작 관련 메서드(속성 조회 및 설정)
- `Element.getAttribute(attributeName)`
    - 해당 요소의 지정된 값(문자열)을 **반환**
    - 인자(attributeName)는 값을 얻고자 하는 속성의 이름
- `Element.setAttribute(name, value)`
    - 지정된 요소의 값을 **설정**
    - 속성이 이미 존재하면 값을 **갱신**
    - 존재하지 않으면 지정된 이름과 값으로 새 속성을 **추가**'

```js
// a tag 생성 및 컨텐츠 추가
const aTag = document.createElement('a')
aTag.innerText = 'google'

// div 태그의 자식 태그로 a 태그 추가
const div = document.querySelector('div')
div.appendChild(aTag)

// a 태그의 href 속성 추가
aTag.setAttribute('href', 'https://google.com')
console.log(aTag.getAttribute('href'))

//h1 tag 선택 및 클래스 목록 조회
const h1 = document.querySelector('h1')
console.log(h1.classList)

//클래스가 존재한다면 제거하고 false를 반환
// 존재하지 않는다면 클래스를 추가하고 true를 반환
h1.classList.toggle('blue')
console.log(h1.classList)
```
##### [참고]classList - Methods
- toggle(String)  
클래스의 유무를 체크해서 없으면 add하고 true를 리턴하고, 있으면 remove를 하고 false를 리턴한다.

- add(String)  
지정한 클래스 값을 추가한다.  
만약 추가하려는 클래스가 이미 존재한다면 무시.

- remove(String)  
지정한 클래스 값을 제거한다.  
존재하지 않는 클래스라면? 에러 발생 X

- contains(String)  
지정한 클래스 값이 존재하는지 확인.  
true, false 값을 반환.  
  
- replace(old, new)  
old class를 new class로 대체  

- item(Number)  
인덱스 값을 활용하여 클래스 값을 반환  
---

# Event
- 이벤트란 프로그래밍 하고 있는 시스템에서 일어나는 사건(action) 혹은 발생(occurrence)인데, 우리가 원한다면 그것들에 어떠한 방식으로 응답할 수 있도록 시스템이 말해주는 것
- 클릭 말고도 웹에는 다양한 Event가 존재함
    - 키보드 키 입력, 브라우저 닫기, 데이터 제출, 텍스트 복사 등

## Event object
- 네트워크 활동이나 사용자와의 상호작용 같은 사건의 발생을 알리기 위한 객체
- DOM 요소는 Event를 **수신**
- 받은 Event를 **처리**할 수 있음
    - Event처리는 주로 addEventListener()라는 Event처리기(Event handler)를 사용하여 다양한 html 요소에 부착하게 됨  

### Event handler - addEventListener()
대상(EventTarget)에 특정 Event(type)가 발생하면, 할 일(listener-callback함수)을 등록한다  
`EventTarget.addEventListener(type, listener[, options])`
- 지정한 Event가 대상에 전달될 때마다 호출할 함수를 설정 
- Event를 지원하는 모든 객체 (Element, Document, Window 등)를 대상(EventTarget)으로 지정가능 

#### EventTarget.addEventListener(`type`, listener[, options])
- 반응할 Event 유형을 나타내는 대소문자 구분 문자열
- 대표 이벤트 : input, click, submit ... (그외 Mozilla 참고)

#### EventTarget.addEventListener(type, `listener`[, options])
- 지정된 타입의 Event를 수신할 객체
- Javascript function 객체(콜백 함수)여야 함
- **콜백 함수는 발생한 Event의 데이터를 가진 Event 기반 객체를 유일한 매개변수로 받음** 

```html
<body>
  <button id="btn">버튼</button>
  <p id="counter">0</p>
  
  <script>
    const btn = document.querySelector('#btn')
    // 초기값 count 선언
    let count = 0
    // event handler  -- btn이 클릭될 때마다 아래 함수가 실행됨
    btn.addEventListener('click', function(event) {

      count += 1

      // id가 counter인 태그의 안의 내용을 변경시킴
      const pTag = document.querySelector('#counter')
      pTag.innerText = count
    })
  </script>
</body>
```

```html
<body>
  <input type="text" id="text-input">
  <p></p>
  <script>
    const textInput = document.querySelector('#text-input')
    textInput.addEventListener('input', function(event) {
      console.log(event)
      console.log(event.target)  // <input type="text" id="text-input">
      console.log(event.target.value)  // input 태그안에 들어가는 내용
      
      const pTag = document.querySelector('p')
      pTag.innerText = event.target.value
    })
    
  </script>
</body>
```

```html
<body>
  <h1></h1>
  <button id="btn">클릭</button>
  <input type="text">

  <script>
    const inputTag = document.querySelector('input')
    const btn = document.querySelector('#btn')

    // input에 값이 입력되면 이벤트 함수 실행
    inputTag.addEventListener('input', function(event) {
      const h1Tag = document.querySelector('h1')  // h1 태그 선택
      h1Tag.innerText = event.target.value  // input에 입력된 값을 h1태그 컨텐츠로 변경
    })

    // 버튼이 클릭되면 이벤트 함수 실행
    btn.addEventListener('click', function(event) {
      const h1Tag = document.querySelector('h1')  // h1 태그 선택
      // 클래스 blue를 토글하기
      h1Tag.classList.toggle('blue')  // class이름만 넣기
    })
  </script>
</body>
```

### event 취소
- `event.preventDefault()`
    - 현재 Event의 기본 동작을 중단
    - HTML 요소의 기본 동작을 작동하지 않게 막음
    - HTML 요소의 기본 동작 예시
        - a tag: 클릭 시 특정 주소로 이동
        - form tag: form 데이터 전송
```js
<body>
  <div>
    <h1>정말 중요한 내용</h1>
  </div>
  <script>
    const h1Tag = document.querySelector('h1')
    h1Tag.addEventListener('copy', function (event) {
        event.preventDefault()
        alert('삐빅 복사를 할 수 없습니다.')
    })
  </script>
</body>
```
- 로또번호 만들기
```html
<body>
  <h1>로또 추천 번호</h1>
  <button id="lotto-btn">행운 번호 받기</button>
  <div id="result"></div>

  <!-- lodash library -->
  <script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
  <script>
    const btn = document.querySelector('#lotto-btn')
    btn.addEventListener('click', function (event) {
      
      // 공이 들어갈 컨테이너 생성
      const balls = document.createElement('div')
      balls.classList.add('ball-container')  // 해당 요소에 클래스 속성 값을 추가, 같은 클래스 명이 있는 경우 무시

      // 랜덤한 숫자 6개 (lodash 활용)
      const numbers = _.sampleSize(_.range(1, 46), 6)
      console.log(typeof(numbers), numbers) // object - array

      // 공 만들기
      numbers.forEach(element => {
        const ball = document.createElement('div')  
        ball.classList.add('ball')  // ball이라는 클래스 속성 값을 추가
        ball.innerText = element  // ball의 innerText에 각 랜덤 숫자 넣어주기
        ball.style.backgroundColor = 'crimson'
        balls.appendChild(ball)  // ball들을 balls div에 추가
      });

      // 공 컨테이너를 결과 영역의 자식으로 넣기
      const resultDiv = document.querySelector('#result')
      result.appendChild(balls)
    })

  </script>
</body>
```

##### [참고] lodash
- 모듈성, 성능 및 추가 기능을 제공하는 Javascript 유틸리티 라이브러리
- array, object 등 자료구조를 다룰 때 사용하는 유용하고, 간편한 유틸리티 함수들을 제공 
- reverse, sortBy, range, random ... 
- https://lodash.com/
---

- todo app 만들기
```html
<body>
  <form action="#">
    <input type="text" class="inputData">
    <input type="submit" value="Add">
  </form>
  <ul></ul>

  <script>
    const formTag = document.querySelector('form')
    
    formTag.addEventListener('submit', function (event) {
      
      // form의 기본 event 막기
      event.preventDefault()
      
      const inputTag = document.querySelector('.inputData')
      const data = inputTag.value

      // 데이터가 있을 때만 이벤트 시행
      if (data.trim()){
        const listTag = document.createElement('li')
        listTag.innerText = data

        const ulTag = document.querySelector('ul')
        ulTag.appendChild(listTag)
        
        event.target.reset()

      } else {
        alert('내용이 없습니다. ')
      }
    })
  </script>
</body>
```

# this
- 어떠한 `object`를 가리키는 키워드 
    - java에서의 this와 python에서의 self는 인스턴스 자기자신을 가리킴
- Javascript의 함수는 호출될 때 this를 암묵적으로 전달받음
- Javascript에서의 this는 일반적인 프로그래밍 언어에서의 this와 다름 (다른 언어의 this는 어디서 호출되었는지에 따라 달라짐)
- Javascript는 해당 `함수 호출 방식`에 따라 `this에 바인딩되는 객체가 달라짐`
- 함수를 선언할 때 this에 객체가 결정되는 것이 아니고, 함수를 호출할 때 함수가 어떻게 호출되었는지에 따라 동적으로 결정됨

## this INDEX
1. 전역 문맥에서의 this
2. 함수 문맥에서의 this
    - 단순 호출
    - Method(객체의 메서드로서)
    - Nested(함수 안에 콜백함수로 있을 때)

### 전역문맥에서의 this
- 브라우저의 전역 객체인 window를 가리킴
    - 전역객체는 모든 객체의 유일한 최상위 객체를 의미
```js
console.log(this) // window
// node.js에서는 global
```

### 함수문맥에서의 this
- this값은 함수를 호출한 방법에 의해 결정됨 
- 함수 내부에서의 this값은 함수를 호출한 방법에 의해 좌우됨
1. 단순호출
    - 전역객체를 가리킴
    - 전역은 브라우저에서는 window, Node.js에서는 global을 의미함

2. Method(Function in Object, 객체의 메서드로서)
    - 메서드로 선언하고 호출한다면, 객체의 메서드로서 `해당 객체가 바인딩`됨
    - 객체 안의 메서드는 본인을 호출한 this를 메서드로 가리킴
```js
const myObj = {
    data: 1,
    myFunc(){
        console.log(this)      // myObj
        console.log(this.data) // 1
    }
}
myObj.myFunc()  // myObj 
```

3. Nested(Function 키워드)
    - forEach의 콜백함수에서의 this가 메서드의 객체를 가리키지 못하고 window 전역객체를 가리킴
    - 콜백함수는 단순호출 -> 가리키는 객체가 window임
    - 이를 해결하기 위해 `화살표 함수`사용
```js
const myObj = {
    numbers: [1],
    myFunc(){
        console.log(this) // myObj
        //여기 아래의 this는 myObj
        this.numbers.forEach(function (number) {
            console.log(number) // 1
            console.log(this)   // window - function으로 단순 호출 방식으로 사용되었기 때문 
        })
    }
}
```
```js
// 화살표 함수를 사용한 경우
const myObj = {
    numbers: [1],
    myFunc(){
        console.log(this) // myObj
        //여기 아래의 this는 myObj
        this.numbers.forEach( (number) => {
            console.log(number) // 1
            console.log(this)   // myObj 
        })
    }
}
```
    - 이전에 일반 function 키워드와 달리 메서드의 객체를 가리킴
    - 화살표 함수에서 this는 자신을 감싼 정적 범위
    - 자동으로 한 단계 상위의 scope의 context를 binding

- 화살표 함수
    - 화살표 함수는 호출의 위차와 상관없이 상위 스코프를 가리킴(Lexical scope this)
    - function 함수는 호출되는 위치에 따라 달라짐
    - 함수 내의 함수상황에서 화살표 함수를 쓰는 것을 권장 
- Lexical scope
    - 함수를 어디서 호출했는지가 아니라 `어디에 선언했는지`에 따라 결정
    - Static scope 라고도 함

### this & addEventListener
- addEventListener에서의 콜백 함수는 function 키워드를 사용하는 경우 addEventListener를 호출한 대상(event.target)을 가리킴
- 일반 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정되는 것이 아니고, 함수를 호출할 때 함수가 어떻게 호출되었는지에 따라 this에 바인딩할 객체가 동적으로 결정된다
- 화살표 함수의 경우 상위 스코프를 가리키기 때문에 window객체가 바인딩 됨
- 화살표함수는 스코프의 영향을 받지않고 스코프 외부에 접근하여 윈도우를 참조한다
- 화살표 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정된다. 동적으로 결정되는 일반 함수와는 달리 화살표 함수의 this 언제나 상위 스코프의 this를 가리킨다. 
- `addEventListener 콜백함수는 function 키워드 쓰기!`