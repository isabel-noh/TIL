#### Node.js
- Javascript: 브라우저를 조작하는 유일한 언어
    - 브라우저 밖에서는 구동X
- Node.js: 자바스크립트를 구동하기 위한 런타임 환경 
    - 브라우저 밖에서도 구동할 수 있게 됨
    - Chrome V8엔진을 제공하여 여러 OS환경에서 실행할 수 있는 환경을 제공
    - Browser만 조작 가능했으나, 이제는 Server-Side-Programming 또한 가능해짐

#### NPM (Node Package Manager)
- Javascript 패키지 관리자
    - Python의 pip 같이 다양한 의존성 패키지를 관리
    - Node.js -> `npm`
- Node.js의 기본 패키지 관리자 (Node.js설치시 함께 설치됨)

# Vue CLI
Vue 개발을 위한 표준 도구   
프로젝트의 구성을 도와주는 역할   
확장 플러그인, GUI, Babel 등 다양한 tool 제공  

#### Quick Start
- 설치(global에 설치할 것이기 때문에 어느 위치에서 설치하던 상관없음)  
`$ npm install -g @vue/cli`
- 프로젝트 생성(vscode terminal에서)  
`$ vue create vue-cli`
- Vue 버전 선택(Vue2)  
`Default ([Vue 2] babel, eslint)` 선택  
- vue-cli 폴더로 이동  
`$ cd vue-cli`
- 서버 구동 / 프로젝트 실행    
`$ npm run serve`  
```shell
App running at:
  - Local:   http://localhost:8080/ 
  - Network: http://172.20.10.5:8080/
```

## Vue CLI 프로젝트 구조
![vueCli](https://user-images.githubusercontent.com/89833631/199371205-dfc15d96-5b4b-4037-98f5-140f020cb83d.png)
#### node_modules
- node.js 환경의 여러 의존성 모듈
- python의 venv와 비슷한 역할
    - .gitignore에 넣어주어야 함, Vue 프로젝트를 생성하면 자동으로 추가됨

#### node_modules - `Babel`
- 'Javascript compiler' - babel.config.js
- Javascript ES6+ 코드를 구버전으로 번역/변환해주는 도구
- Javascript의 파편화, 표준화의 영향으로 작성된 코드의 spectrum이 매우다양함
    - 최신 문법을 사용하여도 브라우저 버전 별로 동작하지 않는 상황이 발생
    - 버전에 따른 같은 의미의 다른 코드를 작성하는 등의 대응이 필요해짐
    - 이러한 문제를 해결하기 위해 등장한 도구
    - 원시 코드(최신 버전)을 목적 코드(legacy code, 구 버전)으로 옮기는 번역기가 등장하면서 코드가 특정 브라우저에서 동작하지 않는 상황에 대해 크게 고민하지 않아도 되게 됨

##### Babel 동작 예시
```js
// Babel Input : ES2015 arrow function
// 원시 코드
[1, 2, 3].map((n) => n + 1);

// Babel output : ES5 equivalent
// 목적 코드
[1, 2, 3].map(function(n){
    return n + 1;
});
```
#### node_modules - `Webpack`
- 'static module bundler'
- module 간 의존성 문제를 해결하기 위한 도구
- project에 필요한 모든 module을 mapping하고 내부적으로 종속성 그래프를 build함

#### Module
- 개발하는 application의 크기가 커지고 복잡해지면서 파일 하나에 모든 기능을 담기가 어려워짐
- 자연스럽게 파일을 여러 개로 분리하여 관리하게 되었고, 분리된 파일이 각각 module, 즉 js 파일 하나가 하나의 모듈이 됨
- 모듈은 대개 기능 단위로 분리되며, 클래스 하나 혹은 특정 목적을 가진 복수의 함수로 구성된 라이브러리 하나로 구성됨
- 여러 모듈 시스템
    - ESM(ECMA Script Module), AMD, CommonJS, UMD...

##### 모듈 의존성 문제
- 모듈의 수가 많아지고 라이브러리 혹은 모듈 간의 의존성이 깊어지면서 특정한 곳에서 발생한 문제가 어떤 모듈 간의 문제인지 파악하기가 어려워짐
- Webpack은 이 모듈 간의 의존성 문제를 해결하기 위해 등장하게 됨

#### Bundler
- `모듈 의존성 문제를 해결`해주는 작업 : Bundling
- Webpack은 이러한 문제를 해결해주는 Bundler 중 하나임
- 모듈들을 하나로 묶어주고 묶인 파일은 하나(혹은 여러 개)로 만들어짐
- 애플리케이션에 필요한 모든 종류의 파일들을 `모듈 단위로 나누어 최소한의 파일 묶음(번들)으로 만들어 냄`
- Bundling된 결과물은 `개별 모듈의 실행 순서에 영향을 받지 않고 동작하게 됨`
- snowpack, parcel, rollup.js 등의 webpack 이외에도 다양한 모듈 번들러 존재
- `Vue CLI는 이러한 Babel, Webpack 에 대한 초기 설정이 자동으로 됨`

##### Bundler의 장점
1. 네트워크 병목 현상 해결 - 여러 파일을 최적화 해서 하나의 파일로 묶기 때문에 주고 받는 파일의 크기를 줄여줆
2. 모듈 단위 코딩 - 유지 보수가 편함, 코드의 가독성 향상
3. 다양한 서드파티 기능 이용
    - Webpack의 경우 Babel-loader과 같은 다양한 로더를 이용해서 모던 자바스크립트나 SASS를 사용할 수 있다.

#### package.json
- 프로젝트의 종속성 목록과 지원되는 브라우저에 대한 구성 옵션을 포함

#### package-lock.json
- node_modules에 설치되는 모듈과 관련된 모든 의존성을 설정 및 관리
- 협업 및 배포 환경에서 정확히 동일한 종속성을 설치하도록 보장하는 표현
- 사용할 패키지의 버전을 고정
- 개발 과정간의 의존성 패키지 충돌 방지 
- python의 requirements.txt 역할

#### public/index.html
- Vue 앱의 뼈대가 되는 html
- Vue 앱과 연결될 요소가 있음

#### src/
- src/assets: 정적 파일을 저장하는 디렉토리
- src/components: 하위 컴포넌트들이 위치
- src/App.vue: 최상위 컴포넌트, public/index.html과 연결됨
- src/main.js
    - webpack이 빌드를 시작할 때 가장 먼저 불러오는 entry point
    - public/index.html과 src/App.vue를 연결시키는 작업이 이루어지는 곳
    - Vue 전역에서 활용할 모듈을 등록할 수 있는 파일

## SFC
### Component
- UI를 독립적이고 재사용 가능한 조각들로 나눈 것
    - 기능별로 분화한 코드 조각
- CS에서는 다시 사용할 수 있는 범용성을 위해 개발된 소프트웨어 구성 요소를 의미
- 하나의 app을 구성할 때 중첩된 컴포넌트들의 tree로 구성하는 것이 보편적
    - Vue에서는 src/App.vue를 root node로 하는 tree구조
- 컴포넌트는 유지보수를 쉽게 만들어 줄 뿐만 아니라 재사용성 측면에서도 매우 강력한 기능을 제공
- 웹 서비스는 여러 개의 컴포넌트로 이루어져 있음
- 하나의 컴포넌트를 만들어 반복되는 UI를 쉽게 처리할 수 있음

#### component in Vue
- 이름이 있는 재사용 가능한 Vue instance
- Vue instance는?
    - 앞 수업에서 만들었던 `const app = new Vue({})`에서의 `app`이 컴포넌트임

### SFC (Single File Component)
- 하나의 `.vue` 파일이 하나의 `Vue instance`, 하나의 `컴포넌트`
    - Single File Component
- Vue instance에서는 HTML, CSS, Javascript 코드를 한번에 관리
    - Vue instance를 `기능 단위로 작성`하는 것이 핵심
- 컴포넌트 기반 개발의 핵심 기능

### Vue Component
![Vue Component](https://user-images.githubusercontent.com/89833631/199374047-289b1ec5-2721-4108-a8fe-e6acce997a64.png)
- 템플릿 (HTML)
    - HTML의 Body 부분
    - 눈으로 보여지는 요소 작성
    - 다른 컴포넌트를 HTML 요소처럼 추가 가능
- 스크립트(Javascript)
    - Javascript 코드가 작성되는 곳
    - 컴포넌트 정보, 데이터, 메서드 등 vue 인스턴스를 구성하는 대부분이 작성됨
    - 파일 자체가 인스턴스이기 때문에 const app = new Vue({})의 코드가 사라지게 됨
- 스타일(CSS)
    - 컴포넌트의 스타일을 담당

#### Vue component 정리
- 컴포넌트들이 tree구조를 이루어 하나의 페이지를 만듦
- root에 해당한느 최상단의 component가 `App.vue`
- 이 App.vue를 index.html과 연결
    - index.html 파일 하나만을 rendering
    - `SPA`

### Vue Component 실습
#### MyComponent.vue
1. src/components 안에 파일 생성 
2. script에 이름 등록
3. template에 요소 추가
```vue
<template>
    <!-- 3번 -->
  <div>
    <h1>이거는 내가 만든 새로운 컴포넌트임</h1>
  </div>
</template>

<script>
export default {
    name:'MyComponent', // 2. 파일이름과 맞춰 주기! 
}
</script>

<style>

</style>
```
>[주의] templates 안에는 반드시 하나의 요소만 추가 가능  
> - 비어있으면 안됨
> - 해당 요소 안에 추가 요소를 작성하여야 함

#### component 등록 step3
1. 불러오기
2. 등록하기
3. 보여주기 
##### 1. 불러오기
`import {instance name} from {위치}`  
- instance name은 instance 생성 시 작성한 이름
- `@`는 src의 shortcut
- `.vue` 생략 가능
##### 2. 등록하기
```vue
export default {
    name: 'App',
    components:{
        MyComponent,
    }
}
```
##### 3. 보여주기
`<MyComponent/>`  
- 닫는 태그만 있는 요소처럼 사용
```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- 3. 보여주기 -->
    <MyComponent/>
  </div>
</template>

<script>
// 1. 불러오기
import MyComponent from '@/components/MyComponent'; // 절대경로 생략 가능, .vue 생략 가능

export default {
  name: 'App',
  components: {
    // 2. 등록하기
    MyComponent,
  }
}
</script>

<style>
#app {
  ...
}
</style>

```
#### 하위 컴포넌트 등록하기
```vue
<!-- MyComponentItem.vue -->
<template>
  <div>
    <!-- 보여주기 -->
    <h3>MyComponentItem</h3>
  </div>
</template>

<script>
export default {
    // 등록하기
    name:'MyComponentItem',
}
</script>

<style>

</style>
```
```vue
<!-- MyComponent.vue -->
<template>
    <!-- 3번 -->
  <div>
    <h1>Hello, SSAFY</h1>
    <!-- MyComponentItem 하위 컴포넌트 보여주기 -->
    <MyComponentItem />
  </div>
</template>

<script>
// 하위 컴포넌트 import 
import MyComponentItem from './MyComponentItem.vue';
export default {
    name:'MyComponent', // 2. 파일이름과 맞춰 주기! 
    // MyComponentItem 하위 컴포넌트 등록
    components:{
        MyComponentItem,
    }
}
</script>

<style>
</style>
```

### 이름 규칙 지정
https://vue2.hphk.io/v2/style-guide/#%EC%8B%B1%EA%B8%80-%ED%8C%8C%EC%9D%BC-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EC%9D%B4%EB%A6%84-%EA%B7%9C%EC%B9%99-%EC%A7%80%EC%A0%95-casing-%EB%A7%A4%EC%9A%B0-%EC%B6%94%EC%B2%9C%ED%95%A8
#### 싱글 파일 컴포넌트 이름 규칙 지정(casing)
Filenames of single-file components should either be always `PascalCase` or always `kebab-case`.    
하나만 선택해서 사용할 것 -> 우리는 파스칼 케이스   
```file
components/
|- MyComponent.vue
```

#### 베이스 컴포넌트 이름
Base components (a.k.a. presentational, dumb, or pure components) that apply app-specific styling and conventions should all begin with a specific prefix, such as Base, App, or V.  
베이스 컴포넌트일 경우, 파일명 앞에 `Base`붙여주기
```file
components/
|- BaseButton.vue
|- BaseTable.vue
|- BaseIcon.vue
```

#### 싱글 인스턴스 컴포넌트 이름
Components that should only ever have a single active instance should begin with the The prefix, to denote that there can be only one.  
어디에 소속되어있거나 단독으로 쓰이는 것이 아닌 컴포넌트의 경우에는 파일명 앞에 `The` 붙여주기  
```file
components/
|- TheHeading.vue
|- TheSidebar.vue
```

#### 강한 연관성을 가진 컴포넌트 이름
Child components that are tightly coupled with their parent should include the parent component name as a prefix.    
강한 연관성, 소속되어 있는 컴포넌트들의 이름을 정할 때는, 부모 컴포넌트의 이름을 앞에 붙여주기  
```file
components/
|- TodoList.vue
|- TodoListItem.vue
|- TodoListItemButton.vue
```

