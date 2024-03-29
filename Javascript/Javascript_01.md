##### Javascript를 배우는 이유
- Web 기술의 기반이 되는 언어   
- HTML 문서의 콘텐츠를 동적으로 변경할 수 있는 언어   
- WEB이라는 공간에서 채팅, 게임등 다양한 동작을 할 수 있게 된 기반  
- 다양한 분야로 확장이 가능함   
    - 단순히  web 조작을 넘어 서버 프로그래밍, 모바일 서비스, 컴퓨터 응용프로그래밍, 블록체인, 게임 개발 등 다양한 분야에서 활용이 가능한 언어가 됨  

##### 웹 브라우저의 역할
URL을 통해 Web을 탐색함  
HTML/CSS/JS를 이해한 뒤 해석하여 사용자에게 하나의 화면으로 보여줌  
웹 서비스 이용시 클라이언트의 역할을 함  

##### 웹 브라우저와 스크립트 언어
- 1993 Mosaic Web Browser 
    - 유저가 웹을 쉽게 탐색할 수 있게 버튼 등을 탑재한 GUI 기반의 웹 브라우저 
- 1994 Netscape Navigator
    - Mosaic Web Browser를 개선한 후속작으로 시장 점유율 80% 차지

-> 이 때까지는 정적 웹 페이지를 단순히 보여주는 용도였기 때문에 웹 브라우저에 탑재하여 웹 페이지를 동적으로 바꿔줄 Script 언어개발이 필요했음  
> Script 언어란 :  
    소스 코드를 기계어로 바꿔주는 컴파일러 없이 바로 실행 가능한 언어(단, 속도가 느림)

- Netscape에서 Script언어인 Mocha 개발
- 이후 LiveScript로 이름 변경 후 브라우저에 LiveScript를 해석해주는 Engine을 내장
- 이후 유명한 JAVA의 이름을 따서 Javascript로 이름 변경 
- 1995 Microsoft의 Internet Explorer 
    - Javascript를 그대로 복사한 JScript라는 언어를 제작 후 이를 탑제한 Web Browser인 Internet Explorer 출시
    - 이후 Javascript와 JScript는 각자의 기능을 추가하기 시작 
    - Javascript와 JScript가 각각 발전하면서 코드를 따로따로 개발해야하는 불편이 생김
- 1996-2000 ECMA 표준 발의 
    - Netscape가 정보 통신에 관한 규약을 만드는 비영리 단체 ECMA에게 Javascript 기반의 표준안 발의 제안, ECMAScript1 출시
    - 이후 여러 문법이 추가되며 ECMAScript의 버전이 올라감
    - But, Microsoft의 Internet Explorer - 우리는 Windows에 Internet Explorer 이미 탑재해놓음, 이래도 안씀 ? 
    - Internet Explorer의 시장 점유율 95% 이상으로 증가, ECMAScript 표준안을 무시하기로 함 
- 2001-2004 다양한 웹 브라우저의 등장 
    - ActionScript3라는 스크립트 언어를 기반으로 한 FireFox웹 브라우저 출시
    - Netscape Navigator & Internet Explorer & Firefox 지원을 위해 고통 받는 개발자들... 
    - 이후 Opera 등 다양한 웹 브라우저가 계속 시장에 출시됨 
- jQuery 등의 라이브러리 등장 
    - 각 브라우저의 엔진에 맞는 스크립트를 여러 번 작성하는 고통
    - 중간에 하나의 레이어를 두고 코딩하는 것 -> jQuery
        - jQuery 문법에 맞춰 작성하면 브라우저별로 엔진에 맞는 스크립트 변환을 jQuery가 알아서 변환을 해줌 
- 2008 Google의 Chrome의 등장과 대통합 시대 
    - V8이라는 강력한 엔지을 탑재한 Chrome 등장
        - Javascript 해석이 다른 웹 브라우저에 비해 월등히 빠름
    - Chrome의 성능 앞에서 다른 웹 브라우저들이 함께 표준안을 만들자고 제안
- 2009 ECMAScript5(ES5) 표준안 제정
- 2010 ECMAScript6(ES6) 표준안 제정

# Javascript
```html
<!-- hello.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- body 태그 안에서 바로 실행시킬 수도 있고 -->
    <script> 
        console.log('hello, javascript')
    </script>
</body>
<!-- body태그 밖에서 hello.js라는 javascript 파일을 불러와서 실행시킬 수도 있음 -->
<script src="hello.js"></script>
</html>
```
```js
// hello.js
console.log('hello, javascript');
```
- 웹 브라우저에서 개발자 도구 - 콘솔 창에서 바로 실행할 수도 있음
- 특별하게 웹 브라우저에서 바로 실행할 수 있는 JavaScript 문법들을 Vanilla JavaScript라고 부름

## Node.js로 실행하기
### 1. via `NVM`

- nvm이란?
    
    [https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)
    
    - "node.js의 버전 관리자"

**설치**

```bash
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

**설정 값 입력**

```bash
$ code ~/.zshrc
```

```bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```

```bash
$ source ~/.zshrc
```

```bash
$ nvm install 16.18.0
```

```bash
$ nvm use 16.18.0
```

```bash
$ node -v
v16.18.0
```
---
- 설치 확인 
```bash
node -v
npm -v
```
> [참고] npm(Node Package Manager)  
Javascript를 위한 패키지 관리자 (Python의 pip 같은) 

- javascript 파일 실행하기
```bash
node 01_hello.JavaScript
```

## Javascript 기초문법
#### 세미콜론
- 자바스크립트는 세미콜론을 선택적으로 사용 가능
- 세미콜론이 없으면 ASI에 의해 자동으로 세미콜론이 삽입됨
    - ASI(Automatic Semicolon Insertion)

#### 들여쓰기와 코드 블럭
- javascript는 2칸 들여쓰기
- 블럭(block)은 if, for, 함수에서 중괄호 `{}` 내부를 말함
    - javascript는 중괄호 { } 를 상룡하여 코드 블럭을 구분 
```js
if (isClean) {
    console.log('clean!')
}
```
#### 코드 스타일 가이드 
- 코딩 스타일의 핵심은 합의된 원칙과 일관성
- 코드의 품질에 직결되는 중요한 요소
    - 코드의 가독성, 유지보수, 팀원과의 커뮤니케이션 등 개발 과정 전체에 영향을 끼침
- javascript에도 코드 스타일 가이드 존재  
[Airbnb Javascript Style Guide](https://github.com/airbnb/javascript)


#### 주석
- 한 줄 주석 `//`
- 여러 줄 주석 `/* */` 
```js
/* 여러 줄 
주석은 이렇게
적용됨*/
// 한줄 주석은 이렇게
```

## 변수와 식별자
#### 식별자 정의와 특징
- 식별자 Identifier는 변수를 구분할 수 있는 변수명을 말함 
- 식별자는 반드시 문자, 달러($) 혹은 밑줄(_)으로 시작
- 대소문자를 구분, 클래스 명 외에는 모두 소문자로 시작
- 예약어 사용 불가능 (if, for, function 등)
---
- 카멜 케이스(camelCase, lower-camel-case)
    - 변수, 객체, 함수에 사용
- 파스칼 케이스(PascalCase, upper-camel-case)
    - 클래스, 생성자에 사용
- 대문자 스네이크 케이스(SNAKE_CASE)
    - `상수`(constants)에 사용
    - 상수: 개발자의 의도와 상관없이 변경될 가능성이 없는 값을 의미함

### 변수 선언 키워드 
1. let : 블록 스코프 지역 변수를 선언 (추가로 동시에 값을 초기화)
2. const : 블록 스코프 `읽기 전용 상수를 선언` (추가로 동시에 값을 초기화)
3. var : 변수를 선언 (추가로 동시에 값을 초기화)

##### [참고] 선언, 할당, 초기화  
- 선언(Declaration)
    - 변수를 생성하는 시점 혹은 행위
- 할당(Assignment)
    - 선언된 변수에 값을 저장하는 행위 혹은 시점
- 초기화(Initialization)
    - 선언된 변수에 처음으로 값을 저장하는 행위 혹은 시점
```js
let foo             // declaration
console.log()       // undefined

foo = 11            // assignment
console.log(foo)    // 11

let bar = 0         // 선언 + 할당
console.log(bar)    // 0
```

##### [참고] 블록 스코프(block scope)
- if, for, 함수 등의 중괄호 `{}` 내부를 가리킴
- 블록 스코프를 가지는 변수는 블록 바깥에서 접근 불가능
```js
let x = 1
if (x === 1) {
    let x = 2
    console.log(x)    // 2    
}
console.log(x)        // 1
```

### let
- 재할당 가능 & 재선언 불가능 
```js
let number = 10     // 1. 선언 및 초기값 할당 
number = 20         // 2. 재할당
```
```js
let number = 10     // 1. 선언 및 초기값 할당
let number = 20     // 2. 재선언 불가능
```
- `블럭 스코프`를 갖는 지역변수를 선언
- 선언과 동시에 원하는 값으로 초기화할 수 있음

### const
- 재할당 불가능 & 재선언 불가능
```js
const number = 10   // 1. 선언 및 초기값 할당
number = 20         // 2. 재할당 불가능
```
```js
const number = 10   // 1. 선언 및 초기값 할당
const number = 20   // 2. 재선언 불가능
```
- 선언시 반드시 초기값을 설정하여야 하며, 이후 값 변경 불가능
- let과 동일하게 `블록 스코프`를 가짐 

### var
- 재할당 가능 & 재선언 가능
- ES6 이전에 변수를 선언할 때 사용되던 키워드
- `Hoisting` 호이스팅 되는 특성으로 인해 예기치 못한 문제 발생 가능
    - 따라서 ES6 이후부터는 var 대신 const와 let을 사용하는 것을 권장
- `함수 스코프(function scope)`를 가짐
- **변수 선언시 var, const, let 키워드 중 하나를 사용하지 않으면 자동으로 var로 선언됨**

##### [참고] 함수 스코프(function scope)
함수의 중괄호 내부를 가리킴  
함수 스코프를 가지는 변수는 함수 바깥에서 접근 불가능
```js
function foo() {
    var x = 5
    console.log(x)  // 5
}
// ReferenceError : x is not defined
console.log(x)
```

##### [참고] HOISTING 호이스팅
- 변수를 선언 이전에 참조할 수 있는 현상(선언이 위로 끌여올려짐)
- var로 선언된 변수는 선언 이전에 참조할 수 있으며, 이러한 현상을 호이스팅이라고 함
- 변수 선언 이전의 위치에서 접근시 undefined 를 반환
```js
console.log(name)   // undefined 선언 이전에 참조

var name = 'isabel' // 선언
```
```js
var name            // undefined로 초기화
console.log(name)   

var name = 'isabel'
```
- Javascript에서 변수들은 실제 실행시에 코드의 최상단으로 끌어 올려지게 되며 hoisted 이러한 이유 때문에 var로 선언된 변수는 선언 시에 undefined로 값이 초기화되는 과정이 동시에 일어남
- let, const는 호이스팅이 일어나면 에러를 발생시킴
```js
console.log(username)   // undefined
var username = 'isabel'

console.log(email)      // Uncaught ReferenceError
let email = 'isabel@gmail.com' 
    
console.log(age)        // Uncaught ReferenceError
const age = 20
```
- 변수를 선언하기 전에 접근이 가능한 것은 코드의 논리적인 흐름을 깨뜨리는 행위이며 이러한 것을 방지하기 위해 let, const가 추가됨
    - var는 앞으로 사용하지 않아야함
- but, 아직까지도 많은 기존의 Javascript 코드는 ES6 이전의 문법으로 작성되어 있으므로 호이스팅에 대한 이해는 필요함 
- Airbnb 스타일 가이드에서는 기본적으로 `const 사용을 권장`
    - 재할당하여야 하는 경우에만 let 사용
        - 반복문 내부에서 값이 계속 재할당되는 경우라던지 

## 데이터 타입
Javascript의 모든 값은 특정한 데이터 타입을 가짐  
- 원시 타입 Primitive type
- 참조 타입 Reference type
### Number
정수 혹은 실수형 숫자를 표현한느 자료형
```js
const a = 13
const b = -5
const c = 3.14      // float - 숫자표현
const d = 2.998e8   // 2.998 * 10^8 = 299,800,000
const e = Infinity
const f = -Infinity
const g = NaN   // Not a Number 를 나타내는 값
```
- NaN
    - Not-A-Number 숫자가 아님
    - Number.isNaN() 의 경우 주어진 값의 유형이 Number이고 값이 NaN이면 true, 아니면 false를 return
    - NaN을 반환하는 경우
        1. 숫자로서 읽을 수 없음(parseInt("어쩌구"), Number(undefined))
        2. 결과가 허수인 수학 계산식(Math.sqrt(-1))
        3. 피연산자가 NaN(7 ** NaN)
        4. 정의할 수 없는 계산식 (0 * Infinity)
        5. 문자열을 포함하면서 덧셈이 아닌 계산식( "가" / 3 )

### String
문자열을 표현하는 자료형  
- 작은 따옴표 혹은 큰 따옴표 모두 가능
```js
const sentence1 = "Ask and go to the blue"  // single quote
const sentence2 = "Ask and go to the blue"  // double quote

console.log(sentence1)
console.log(sentence2)
```
- 곱셈, 나눗셈, 뺄셈은 안되지만 덧셈을 통해 문자열을 붙일 수는 있음
```js
const firstName = 'Tony'
const lastName = 'Stark'
const fullName = firstName + lastName
```
- Quote를 사용하면 선언 시 줄 바꿈이 안됨 
- escape sequence를 사용할 수 있기 때문에 `\n`을 사용하여야 함`
```js
// BAD
const word = "hello
Mr.Big" 
// Uncaught SyntaxError : Invalid or unexpected token

// GOOD
const word1 = "hello \n Mr.Big"
console.log(word1)
```
### Template Literal
- `Template Literal`을 사용하면 줄 바꿈이 되며, 문자열 사이에 변수도 삽입 가능(백틱 '`')
- 단, escape sequence를 사용할 수 없음 (== python의 'f-string')
```js
const word2 = `hello
mr.Big`
console.log(word2)

const age = 10
const message = `Isabel is ${age} years old.`
console.log(message)
```
- 내장된 표현식을 허용하는 문자열 작성 방식
- ES6+부터 지원
- Backtick(``)을 이용하며, 여러 줄에 걸쳐 문자열을 정의할 수도 있고, Javascript의 변수를 문자열 안에 바로 연결할 수 있는 이점이 생김 
- 표현식을 넣을 수 잇는데 이는 `$`와 중괄호 (` ${expression} `)로 표기

### Empty Value
- 값이 존재하지 않음을 표현하는 값으로 Javascript에서는 `null`과 `undefined`가 존재 
- 동일한 역할을 하는 이 두 개의 키워드가 존재하는 이유는 단순한 Javascript의 설계 실수
- 큰 차이를 두지 말고 interchangeable하게 사용할 수 있도록 권장함 
#### Null
null 값을 나타내는 특별한 키워드  
변수의 `값이 없음을 의도적으로 표현`힐 때 사용하는 데이터 타입
```js
let lastName = null
console.log(lastName)    // null
``` 
#### undefined
값이 정의되어 있지 않음을 표현하는 값  
변수 선언 이후 `직접 값을 할당하지 않으면 자동으로 할당됨`
```js
let firstName           // 선언만 하고 할당하지 않음
console.log(firstName)  // undefined
```
#### null&undefined
null과 undefined의 가장 대표적인 차이점은 typeof 연산자를 통해 타입을 확인했을 때 나타남
```js
typeof null         // "object"
typeof undefined    // "undefined"
```
- null이 원시타입임에도 불구하고 object로 출력되는 이유는 javascript설계 당시의 버그가 아직도 해결되지 못한 것
- 이미 null타입에 의존성을 띄고 있는 많은 legacy code들 / 프로그램들이 망가질 수 있기 때문(하위 호환 유지)

##### 참고 
```js
console.log(0 == null)  // false
console.log(0 == undefined)  // false
console.log(null == undefined)  // true
```

### Boolean
- true / false
- 참과 거짓을 표현하는 값
- 조건문 또는 반복문에서 유용하게 사용
    - 조건문 또는 반복문에서 boolean이 아닌 데이터 타입은 `자동 형변환 규칙`에 따라 true / false로 변환됨  
---

- undefined - 항상 false  
- null - 항상 false  
- Number - 0, -0, NaN은 false, 나머지는 true  
- String - ''(빈 문자열)은 false, 나머지는 true  
- Object - 항상 true  

---

## 연산자
### 할당 연산자
- 오른쪽에 있는 피연산자의 평가결과를 왼쪽 피연산자에 할당하는 연산자
- 다양한 연산에 대한 단축 연산자 지원
- increment / decrement 연산자
    - increment (++) : 피연산자의 값을 1증가시키는 연산자
    - decrement (--) : 피연산자의 값을 1감소시키는 연산자
    - += / -= 와 같이 더 분명한 표현을 적는 것을 권장

```js
let c = 0
c += 10     // c에 10 더함
c -= 3      // c에 3을 뺌
c *= 10     // c에 10을 곱합
c++         // c에 1을 더함
c--         // c에 1을 뺌
```

### 비교 연산자
- 피연산자들을 비교하고 결과값을 boolean으로 반환하는 연산자   
- 문자열은 유니코드 값을 사용하며 표준 사전 순서를 기반으로 비교  
```js
3 > 2   // true
3 < 2   // false

'A' < 'B' // true
'Z' < 'a'  // true   소문자가 대문자보다 더 크다 
'가' < '나' // true
```

### 동등 연산자(`==`)
- 두 피연산자가 같은 값으로 평가되는지 비교 후 boolean 값을 반환 
- 비교할 때 `암묵적 타입 변환`을 통해 타입을 일치시킨 후 같은 값인지 비교 
- 두 피연산자가 모두 객체일 경우, 메모리의 같은 객체를 바라보는지 판별 
- `예상치 못한 결과가 발생할 수 있으므로 특별한 경우를 제외하고는 사용하지 않음` 
```js
const a = 1
const b = '1'

console.log(a == b)     // true
console.log(a == true)  // true

// 자동 형변환 예시
console.log(8 * null)       // 0, null 은 0
console.log('5' - 1)        // 4
console.log('5' + 1)        // '51'
console.log('five' * 2)     // NaN
```

### 일치 연산자(`===`)
- 두 피연산자의 값과 타입이 모두 갑은 경우 true를 반환
- 같은 객체를 가리키거나, 같은 타입이면서 같은 값인지를 비교 
- 엄격한 비교가 이뤄지며 암묵적 타입 변환이 발생하지 않음  
    - 엄격한 비교 : 두 비교 대상의 타입과 값 모두 같은지 비교하는 방식
```js
const a = 1
const b = '1'

console.log(a === b)     // false
console.log(a === Number(b))  // true
```

### 논리 연산자 
- and 연산은 `&&`
- or 연산은 `||`
- not 연산은 `!`
- 단축 평가 지원
    - 앞에서 결정되면 뒤는 보지 않음
    - false && true => false
    - true || false => true

### 삼항 연산자 (Ternary Operator)
- 3개의 피연산자를 사용하여 조건에 따라 값을 반환하는 연산자
- 가장 앞의 조건식이 참이면 `:`콜론 앞의 값이 반환되며, false일 경우 `:` 뒤의 값이 반환되는 연산자
- 삼항 연산자의 결과 값이기 때문에 변수에 할당 가능
```js
true ? 1 : 2        // 1
false ? 1 : 2       // 2

const result = Math.PI > 5 ? 'Yep' : 'Nope'
console.log(result)     // Nope
```

## 조건문
- if, switch

### `if` statement
- 조건 표현식의 결과값을 boolean 타입으로 변환 후 참/거짓을 판단
- if, else if, else 
- 조건은 소괄호 안에 작성 
- 실행할 코드는 중괄호 안에 작성 
- 블록 스코프 생성
```js
const name = 'manager'

if (name === 'admin') {
    console.log('hi, admin')
} else if (name === 'manager') {
    console.log('hi, manager')
} else {
    console.log(`hi, ${name}`)
}
```

### `switch` statement
- 조건 표현식의 결과값이 어느 값(case)에 해당하는지 판별
- 표현식(expression)의 결과값을 이용한 조건문
- 표현식의 결과값과 case문의 오른쪽 값을 비교
- break 및 default문은 [선택적]으로 사용 가능
- break문이 없는 경우 break문을 만나거나 default문을 실행할 때까지 다음 조건문 실행
- 블록 스코프 생성
```js
switch(expression) {
    case 'first_value' : {
        // do something
        [break]
    }
    case 'second_value' : {
        // do something
        [break]
    }
    [default : {
        // do something
    }]
}
```
- 아래 경우 모든 console이 출력됨 (`Fall-through`)
    - break를 각 case에 작성해주면 중간에 중단됨
```js
const name = 'isabel'

switch(name) {
    case 'isabel' : {
        console.log('hello, ms.isabel')
        // break
    }
    case 'manager' : {
        console.log('hello, manager')
        // break
    }
    default : {
        console.log(`hello, ${name}`)
    }
}
```
- 주로 특정 변수의 값에 따라 조건을 분기할 때 활용
    - 조건이 많아질 경우 if문보다 가독성이 좋을 수 있음

## 반복문
- while, for, for ... in, for ... of
### while
- 조건문이 참이면 문장을 계속 시행
```js
while(condition) {
    // do something
}
```
```js
let i = 0     // 재할당 되게 하려고 let 선언

while (i < 6) {
    console.log(i)
    i += 1
}
// 0, 1, 2, 3, 4, 5
```

### for
- 특정한 조건이 거짓으로 판별될 때까지 반복
```js
for ([초기문]; [조건문]; [증감문]) {
    // do something
}
```
```js
for (let i = 0; i < 6; i++) {
    // 코드 블럭
    console.log(i)
}
// 0, 1, 2, 3, 4, 5
// 1. 반복문 진입 및 변수 i 선언
// 2. 조건문 평가 후 코드 블럭 실행
// 3. 코드 블럭 실행 이후 i 값 증가
```

### for ... in
- 객체(object)의 속성을 순회할 때 사용
- 배열도 순회 가능하지만 인덱스 순으로 순회한다는 보장이 없으므로 권장하지 않음 (`순서 보장 X`)
- javascript에서의 객체는 key=value 값으로 이루어져있는 python의 dictionary와 유사함 
```js
for (variable in object) {
    statements
}
```
```js
const fruit = {a: 'apple', b:'banana'}

for (const key in fruits) {
    console.log(key)  // a, b
    console.log(fruits[key])  // apple, banana
}
```

### for ... of
- 반복 가능한 객체를 순회할 때 사용
- 반복 가능한(iterable)객체의 종류 : `Array, Set, String...`
```js
for (variable of object) {
    statements
}
```
```js
const numbers = [0, 1, 2, 3]
for (const number of numbers) {
    console.log(number) // 0, 1, 2, 3
}
```

#### for ... in과 for ... of
- for ... in은 속성 이름을 통해 반복 (객체)
- for ... of는 속성 값을 통해 반복 
 
##### [참고] for ...in, for ...of와 const
- 일반적인 for문 `for(let i = 0; i < arr.length; i++) {...}`의 경우에는 최초 정의한 i를 재할ㄹ당하면서 사용하기 때문에 const를 사용하면 에러가 발생한다. 
- for ...in, for ...of의 경우에는 재할당이 아니라, 매 반복 시 해당 변수를 새로 정의하여 사용하므로 const를 선언하여도 에러가 발생하지 않는다. 
```js
const arr = [3, 5, 7]

for (const i in arr){
    console.log(i) // 0, 1, 2
}
for (const i of arr){
    console.log(i) // 3, 5, 7
}
```

# 함수
참조 타입 중 하나로 function 타입에 속함
- 함수 선언식 function declaration
- 함수 표현식 function expression

## 함수의 정의
### 함수 선언식 function declaration
- 일반적인 프로그래밍 언어의 함수 정의 방식
```js
function functionName() {
    // do something
}
```
```js
function add (num1, num2) {
    return num1 + num2
}

add(2, 7)  // 9
```
### 함수 표현식 function expression
- 표현식 내에서 함수를 정의하는 방식
- 함수 표현식은 함수의 이름을 생략한 익명함수로 정의 가능
```js
변수키워드 functionName = function () {
    // do something
}
```
```js
const sub = function (num1, num2) {
    return num1 - num2
}
sub(2, 1)   // 1
```
- 함수 표현식에서 함수 이름을 면시하는 것도 가능
    - 다만 이 경우 함수 이름은 호출에 사용되지 못하고 디버깅 용도로 사용됨
```js
const mySub = function namedSub(num1, num2) {
    return num1 - num2
}
mySub(2, 1)   // 1
namedSub(1, 2) // ReferenceError: namedSub is not defined 
```

### 기본 인자 default arguments
- 인자 작성 `=` 문자 뒤 기본 인자 선언 가능
```js
const greeting = function (name='Anonymous') {
    return `Hi ${name}`
}
greeting()  // Hi Anonymous
```

### 매개변수와 인자의 개수 불일치 허용
- 매개변수보다 인자의 개수가 많을 경우
```js
const noArgs = function () {
    return 0
}
noArgs(1, 2, 3) // 0

const towArgs = function(arg1, arg2) {
    return [arg1, arg2]
}
twoArgs(1, 2, 3)  // [1, 2]
```
- 매개변수보다 인자의 개수가 적을 경우
```js
const threeArgs = function (arg1, arg2, arg3) {
    return [arg1, arg2, arg3]
}
threeArgs()   // [ undefined, undefined, undefined ]
threeArgs(1)    // [ 1, undefined, undefined ]
threeArgs(1, 2)   // [ 1, 2, undefined ]
```

### Spread Syntax(...)
전개 구문 
- 전개구문을 사용하면 배열이나 문자열과 같이 반복 가능한 객체를 배열의 경우는 요소, 함수의 경우는 인자로 확장할 수 있음  
#### 배열과의 사용
```js
let parts = ['shoulders', 'knees']
let lyrics = ['head', ...parts, 'and', 'toes']
// [ 'head', 'shoulders', 'knees', 'and', 'toes' ]
```
#### 함수와의 사용 rest parameters
정해지지 않은 수의 매개변수를 배열로 받음
```js
function func(a, b, ...theArgs){

}
```
```js
const restOpr = function(arg1, arg2, ...restArgs){
    return [arg1, arg2, restArgs]
}

restOpr(1, 2, 3, 4, 5)
restOpr(1, 2)

// [ 1, 2, [ 3, 4, 5 ] ]
// [ 1, 2, [] ]
```
## 선언식과 표현식
```js
// 함수 표현식
const add = function(){ } // function
// 함수 선언식 
function sub(args) { }  // function
```
### 호이스팅 hoisting - 선언식
- 함수 선언식으로 정의한 함수는 var로 정의한 변수처럼 호이스팅이 발생 
- 함수 호출 이후에 선언하여도 동작
```js
add(2, 7) // 9

function  add(num1, num2) {
    return num1 + num2
}
```
### 호이스팅 hoisting - 표현식
- 함수 표현식으로 선언한 함수는 함수 정의 전에 호출 시 에러 발생
- 함수 표현식으로 정의된 함수는 변수로 평가되어 변수의 scope 규칙을 따름 
```js
sub(7, 2)  //ReferenceError: Cannot access 'sub' before initialization 
// 

const sub = function (num1, num2){
    return num1 - num2
}
```
### 화살표 함수
- 함수를 비교적 간결하게 정의할 수 있는 문법
- function 키워드와 중괄호를 이용한 구문을 짧게 사용하기 위해 탄생 
    1. function 키워드 생략 가능
    2. 함수 매개변수가 하나뿐이라면 `()`도 생략 가능
    3. 함수의 내용이 한 줄이라면 `{}`와 `return`을 생략할 수 있음

- 화살표 함수는 항상 익명 함수
    - ==함수 표현식에서만 사용가능 
- **명확성과 일관성을 위해 인자의 소괄호는 없애지 않는 것을 권장**
```js
const greeting = function(name) {
    return `Hi ${name}`
}

// 1단계 : function 키워드 삭제
const greeting = (name) => {
    return `Hi ${name}`
}

// 2단계 : 인자가 1개일 경우에만 ()생략 가능
const greeting = name => {
    return `Hi ${name}`
}

// 3단계 : 함수 바디가 return 을 표현한 표현식 1개일 경우에는 { } & return 삭제 가능
const greeting = name => `Hi ${name}`

// airbnb 스타일 가이드
const greeting = (name) => `Hi ${name}`
```

#### 응용
```js
// 1. 인자가 없다면? () / _ 로 표시 가능
let noArgs = () => 'No Args'
noArgs = _ => 'No args'

// 2-1. object를 return 한다면
let returnObject = () => {return {key:'value'}} // return을 명시로 적어준다. 

// 2-2. return을 적지 않으려면 괄호를 붙여야 한다.
returnObject = () => ({key: 'value'})
```


### 즉시 실행 함수(IIFE, Immediately Invoked Function Expression)
- 선언과 동시에 실행되는 함수
- 함수의 선언 끝에 '()'를 추가하여 선언되자마자 실행하는 형태
- '()'에 값을 넣어 인자로 넘겨줄 수 있음 
- 즉시 실행 함수는 선언과 동시에 실행되기 때문에 같은 함수를 다시 호출할 수 없음 
- 이러한 특징으로 살려 초기화 부분에 많이 사용
- 일회성 함수이므로 익명함수로 사용하는 것이 일반적
```js
(function (num) {return num ** 3 })(2)  // 8
(num => num ** 3)(2)  // 8
```


# Array
- Javascript의 데이터 타입 중 참조 타입에 해당하는 타입은 array와 object이며 객체라고 말함  
- 객체는 속성들의 모음(collection)
- 객체 안쪽의 속성들은 메모리에 할당되어있고 해당 객체는 메모리의 시작 주소값을 가리키고 있는 형태로 이루어져 있음 
## 배열
- 키와 속성들을 담고 있는 참조 타입의 객체 object
- 순서를 보장함
- 주로 대괄호를 이용하여 생성하고, 0을 포함한 양의 정수 인덱스로 특정 값에 접근 가능 (python 처럼 arr[-1] 등의 형식으로 접근 불가)
- 배열의 길이는 array.length 형태로 접근 가능 (array[array.length-1] 등의 방식으로는 접근 가능 )
```js
const numbers = [1, 2, 3, 4, 5]

console.log(numbers[0])     // 1
console.log(numbers[-1])    // undefined
console.log(numbers.length) // 5

console.log(numbers[numbers.length-1])  // 5
console.log(numbers[numbers.length-2])  // 4
console.log(numbers[numbers.length-3])  // 3
console.log(numbers[numbers.length-4])  // 2
console.log(numbers[numbers.length-5])  // 1
```
## Array Helper Methods
- array.reserve()
원본 배열 요소들의 순서를 반대로 정렬
```js
const numbers = [1, 2, 3, 4, 5]
numbers.reserve()
```
- array.push()  
배열의 가장 뒤에 오소 추가
- array.pop()  
배열의 마지막 요소 제거
```js
const numbers = [1, 2, 3, 4, 5]
numbers.push(100)
console.log(numbers)    // [1, 2, 3, 4, 5, 100]
numbers.pop()
console.log(numbers)    // [1, 2, 3, 4, 5]
```
- array.unshift()  
배열의 가장 앞에 요소를 추가
- array.shift()  
배열의 가장 앞에 요소를 제거
- array.includes(value)  
배열에 특정 값이 존재하는지 판별 후 참/거짓 반환 
- array.indexOf(value)  
배열의 특정 값이 존재하는지 확인 후, 가장 첫번째로 찾은 요소의 인덱스를 반환    
해당 값이 없을 경우 -1 반환
```js
const numbers = [1, 2, 3, 4, 5]
let result
result = numbers.indexOf(3)  // 2
result = numbers.indexOf(100)  // -1
```
- array.join([separator])  
배열의 모든 요소를 연결하여 반환  
separator(구분자)는 선택적으로 지정 가능하며, 생략시 쉼표(,)가 기본  
```js
const numbers = [1, 2, 3, 4, 5]
let result

result = numbers.join()  // 1,2,3,4,5
result = numbers.join('')  // 12345
result = numbers.join(' ')  // 1 2 3 4 5
result = numbers.join('-')  // 1-2-3-4-5
```
## Array Helper Methods
배열을 순회하며 특정 로직을 수행하는 메서드  
메서드 호출 시 인자로 `callback 함수`를 받는 것이 특징  
callback 함수 : 어떤 함수의 내부에서 실행될 목적으로 인자로 넘겨받는 함수  

### Array Helper Methods - forEach
```js
array.forEach((element, index, array) =? {
    // do something
})
```
- 인자로 주어지는 함수(콜백함수)를 배열의 각 요소에 대해 한 번 씩 실행
    - element : 배열의 요소
    - index : 배열 요소의 인덱스
    - array : 배열 자체 
- return 없음
- element는 필수 인자, index, 맨 뒤의 array는 선택 인자
```js
const colors = ['red', 'blue', 'white']

const printClr = function (color) {
    console.log(color)
}
colors.forEach(printClr)

colors.forEach(function (color){
    console.log(color)
})

colors.forEach((color) => {
    console.log(color)
})

colors.forEach((color) => { console.log(color) } )
```

### Array Helper Methods - map
```js
array.map((element, index, array) -> {
    // do something
})
```
- 배열의 각 요소에 대해 콜백 함수를 한 번씩 실행
- 콜백 함수의 반환 값을 요소로 하는 새로운 배열 반환 
- 기존 배열 전체를 다른 형태로 바꿀 때 유용  
- forEach + return 이라고 생각해보기

```js
const numbers = [1, 2, 3, 4, 5]

const doubleElement = function (number) {
    return number * 2
}

const newArray = numbers.map(doubleElement)

const newArray2 = numbers.map(function (number) {
    return number * 2
})

const newArray3 = numbers.map( (number) => number * 2 )

console.log(newArray3)
```
### Array Helper Methods - filter
```js
array.filter((element, index, array) =>{
    // do something
})
```
- 배열의 각 요소에 대해 콜백 함수를 한번씩 실행
- 콜백 함수의 반호나 값이 참인 요소들만 모아서 새로운 배열 반환  
- 기존 배열의 요소들을 필터링할 때 유용
```js
const products = [
    { name: 'cucmber', type : 'vegetable' },
    { name: 'banana', type : 'fruit' }, 
    { name: 'carrot', type : 'vegetable' },
    { name: 'apple', type : 'fruit' }
]

const fruitFilter = function (product) {
    return product.type === 'fruit'
}

const newArray = products.filter(fruitFilter)

const newArray1 = products.filter(function (product) {
    return product.type === 'fruit'
})

const newArray2 = products.filter( (product)  => 
    product.type === 'fruit'
)

console.log(newArray2)
```

### Array Helper Methods - reduce
```js
array.reduce((acc, element, index, array) => {
    // do something
}, initialValue)
```
- 인자로 주어지는 함수(콜백함수)를 배열의 각 요소에 대해 한 번씩 실행해서, 하나의 결과 값을 반환  
- 배열을 하나의 값으로 계산하는 동작이 필요할 때 사용(총합, 평균 등)  
- reduce 메서드의 주요 매개변수
    - acc
        - 이전 callback 함수의 반환값이 누적되는 변수
    - initialValue(optional)
        - 최초 callback함수 호출시 acc에 할당되는 값, default값은 배열의 첫번째값
- reduce의 첫번째 매개변수인 콜백함수의 첫번째 매개변수('acc')는 누적된 값
- reduce의 두번째 매개변수인 'initialValue'는 누적될 값의 초기값, 지정하지 않을 시 첫번째 요소의 값이 됨  
- **빈 배열의 경우 initialValue를 제공하지 않으면 에러발생** 
```js
const numbers = [90, 80, 70, 100]

// result 누적된 수
const sumNumbers = numbers.reduce(function (result, number) {
    return result + number
}, 0)

const sumNum = numbers.reduce(( result, number )=> {
    return result + number
}, 0)

const sumNumb = numbers.reduce((result, number )=> result + number, 0)

const AvgNumb = numbers.reduce((result, number) => result + number, 0) / numbers.length

console.log(sumNumb)
```

### Array Helper Methods - find
```js
array.find((element, index, array)) {
    // do something
}
```
- 배열의 각 요소에 대해 콜백 함수를 한 번씩 실행
- 콜백 함수의 반환 값이 참이면, 조건을 만족하는 첫번째 요소를 반환 
- 찾는 값이 배열에 없으면 undefined를 반환
```js
const avengers = [
    { name: 'Tony Stark', age: 45},
    { name: 'Chris Evans', age: 80},
    { name: 'Thor', age: 456},
]

const avenger = avengers.find((avenger) => {
    return avenger.name === 'Tony Stark';
})

console.log(avenger)
```

### Array Helper Methods - some
```js
array.some((element, index, array)) => {
    // do something
}
```
- 배열의 요소 중 하나라도 주어진 판별 함수를 통과하면 참을 반환  
- 모든 요소가 통과하지 못하면 거짓 반환  
- 빈 배열은 항상 false 반환  
```js
const arr = [1, 2, 3, 4, 5]

const result = arr.some(function (elem) {
    return elem % 2 === 0
})

const result = arr.some((elem) => elem % 2 === 0) 
console.log(result)         // true
```
### Array Helper Methods - every
```js
array.every((element, index, array)) => {
    // do something
}
```
- 배열의 모든 요소가 주어진 판별 함수를 통과하면 참을 반환  
- 하나의 요소라도 통과하지 못하면 거짓 반환  
- 빈 배열은 항상 true 반환  
```js
const arr = [1, 2, 3, 4, 5]
const result = arr.every(function(elem) {
    return elem % 2 ===0
})

console.log(result)              // falsef
```

# Object 객체
- 객체는 속성의 집합이며, 중괄호 내부에 key와 value 의 쌍으로 표현
- Key는 문자열 타입만 가능  
    - key 이름에 띄어쓰기 등 구분자가 있으면 따옴표로 묶어서 표현
- value는 모든 타입(함수 포함) 가능
- 객체 요소 접근은 점`.` 또는 대괄호 `[]`로 가능
    - key 이름에 띄어쓰기 같은 구분자가 있으면 대괄호 접근만 가능
```js
const myInfo = {
    name: "Jack",
    phoneNumber: "123456",
    'samsung products' : {  // 이것도 key이지만 띄어쓰기가 있어서 작은 따옴표로 묶어줘야함
        buds: "Galaxy Buds pro",
        galaxy: 'Galaxy s99',
    },
}
console.log(myInfo.name)
console.log(myInfo['name'])
console.log(myInfo["samsung products"]) // 위 경우에는 대괄호로만 접근 가능
// console.log(myInfo.samsung product) 이렇게는 접근 못함
console.log(myInfo["samsung products"].galaxy)
```

## 객체 관련 문법
### 1. 속성명 
객체를 정의할 때 key와 할당하는 변수의 이름이 같으면 예시처럼 축약 가능
```js
var books = ['learning javascript', 'learning python']
var magazines = ['vogue', 'science']

// ES5
var bookShop = {
    books: books,
    magazines: magazines,
}
console.log(bookShop)

// ES6
const bookShop = {
    books, 
    magazines,
}
console.log(bookShop)
```

### 2. method명 축약
메서드 선언 시 function 키워드 생략 가능
```js
// ES5
var obj = {
    greeting: function (){
        console.log('hi!')
    }
}
obj.greeting() 

// ES6+ 
const obj = {
    greeting() {
        console.log('hi!')
    }
}
obj.greeting()
```
### 3. 계산된 속성 (computed property name)
객체를 정의할 때 key의 이름을 표현식을 이용하여 동적으로 생성 가능
```js
const key = 'country'
const value = ['Korea', 'USA', 'Japan', 'China']

const myObj = {
    [key]: value,
}
console.log(myObj) // { country: [ 'Korea', 'USA', 'Japan', 'China' ] }
```

### 4. [중요] 구조 분해 할당(destructing assignment)
배열 또는 객체를 분해하여 속성을 변수에 쉽게 할당할 수 있는 문법
```js
const userInformation = {
    name: 'ssafy Kim',
    userId: 'ssafyStudent1234',
    phoneNumber: '010-1234-4567',
    email: 'ssafy@sssafy.com',
}
// 구조분해할당이 안되는 경우
// const name = userInformation.name
// const userId = userInformation.userId
// const phoneNumber = userInformation.phoneNumber
// const email = userInformation.email

// 구조분해할당을 한 경우
const { name } = userInformation
const { userId } = userInformation
const { phoneNumber } = userInformation
const { email } = userInformation

// 여러 개도 가능
// const {name, userId } = userInformation
const {name, userId, phoneNumber, email } = userInformation
```

### 5. Spread syntax (...)
배열과 마찬가지로 전개구문을 사용해 객체 내부에서 객체 전개 가능  
얕은 복사에 활용가능
```js
const obj = {b: 2, c: 3, d: 4}
const newObj = {a: 1, ...obj, e: 5}

console.log(newObj)  //{ a: 1, b: 2, c: 3, d: 4, e: 5 }
```

### JSON
Javascript Object Notation  
Key-Value 형태로 이루어진 자료 표기법  
Javascript의 Object와 유사한 구조를 가지고 있지만 Object는 그 자체로 타입이고, JSON은 형식이 있는 `문자열`
JSON을 Object로 사용하기 위해서는 변환 작업이 필요함 
```js
const jsonData = {
    coffee: 'Americano',
    iceCream: 'Magnum',
}

// Object -> JSON
const objToJson = JSON.stringify(jsonData)
console.log(objToJson)
console.log(typeof objToJson)

// JSON -> Object
const jsonToObj = JSON.parse(objToJson)
console.log(jsonToObj)
console.log(typeof jsonToObj)
console.log(jsonToObj.coffee)

// json을 사용하면 사람이 읽기도 쉽고, 코딩을 하기도 편함
// {"coffee":"Americano","iceCream":"Magnum"}
// string
// { coffee: 'Americano', iceCream: 'Magnum' }
// object
```

##### [참고] 배열은 객체다
배열은 키와 속성들을 담고 있는 참조 타입의 객체  
배열은 인덱스를 키로 가지며 length 프로퍼티를 갖는 특수한 객체
```js
Object.getOwnPropertyDescriptors([1,2,3])
/*
{
  '0': { value: 1, writable: true, enumerable: true, configurable: true },
  '1': { value: 2, writable: true, enumerable: true, configurable: true },
  '2': { value: 3, writable: true, enumerable: true, configurable: true },
  length: { value: 3, writable: true, enumerable: false, configurable: false }
}
*/
```

