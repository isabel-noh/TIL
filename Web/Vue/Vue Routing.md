# UX&UI
### UX(User Experience)
- 유저와 가장 가까이에 있는 분야, 데이터를 기반으로 유저를 조사하고 분석하여 개발자, 디자이너가 이해할 수 있게 소통
- 유저가 느끼는 경험, 느낌, 태도, 행동을 디자인
    - e.g.) 로딩이 너무 길어서 사용하고 싶지 않았던 사이트...

> - 좋은 UX를 설계하기 위해서  
>   - 사람들의 마음과 생각을 이하ㅐ하고 정리하여 제품에 녹여내는 과정 필요  
>   - 유저 리서치, 데이터 설계 및 정제, 유저 시나리오, 프로토타입 설계 등 필요

### UI(User Interface)
- 유저에게 보여지는 화면을 디자인
- UX를 고려한 디자인을 반영
- 이 과정에서 기능 개선 혹은 추가가 필요한 경우, Front-end 개발자와 가장 많이 소통
- 통일된 디자인을 위한 디자인 시스템, 소통을 위한 중간 산출물, 프르토 타입 등이 필요

##### [참고] Interface
- 서로 다른 두 개의 시스템, 장치 사이에서 정보나 신호를 주고받는 경우의 접점
    - 사용자가 기기를 쉽게 동작시키는 데 도움을 주는 시스템
    - e.g.) CLI(command-line interface)나 GUI(Graphic User Interface)를 사용하여 컴퓨터를 조작

##### 관련 직무
- UX (UX Researcher, User Researcher)
    - 구글: 사용자의 경험을 이해하기 위한 통계 모델을 설계
    - MX: 리서치를 기획하고 사용자에 대한 지표를 정의
    - Meta: 정성적인 방법과 정량적인 방법을 사용하여 사용자를 조사
- UI (Product Designer, Interaction Designer)
    - 구글: 다양한 디자인 프로토타이핑 툴을 사용하여 개발 가이드를 제공
    - MS: 시각 디자인을 고려해서 체계적인 디자인 컨셉을 보여줌
    - Meta: 제품을 이해하고 더 나은 UI Flow와 사용자 경험을 디자인

> [참고] HCI(Human Computer Interaction)
> - 인간과 컴퓨터 사이의 상호작용에 대한 학문

# Prototyping
### software prototyping
- 애플리케이션의 프로토타입을 만드는 것
- 개발중인 sw프로그램의 완성되기 전 버전을 만드는 것
- 한 번에 완성된 버전이 나올 수 없기 때문에 중간중간에 현재 상태를 체크

#### prototyping tool
- `Figma`
    - 웹 기반 시스템을 가짐 (웹 환경에서 동작) : 모든 작업 내역이 웹에 저장됨
    - 실시간으로 팀원들이 협업할 수 있음
    - 다양한 플러그인 존재 (VScode 확장 프로그램 등)


# Routing
네트워크에서 경로를 선택하는 프로세스  
웹 서비스의 라우팅: `유저가 방문한 URL에 대해 적절한 결과를 응답하는 것`    
e.g.) /articles/index/에 접근하면 articles의 index에 대한 결과를 보내줌  

#### Routing in SSR
- Server가 라우팅을 통제
- URL로 요청이 들어오면 응답으로 완성된 HTML 제공
    - Django로 보낸 요청의 응답 HTML은 완성본
- Routing(URL)에 대한 결정권을 서버가 가짐

#### Routing in CSR(in SPA)
- 서버는 하나의 HTML(index.html)만 제공
- 이후 모든 동작은 하나의 HTML 문서 위에서 javascript 코드를 활용
- DOM을 그리는 데 필요한 추가적인 데이터가 있다면 axios와 같은 AJAX 요청을 보낼 수 있는 도구를 사용하여 데이터를 가져오고 처리
- 하나의 URL만 가질 수 있음

##### Routing이 없다면? 
- 유저가 URL을 통한 페이지의 변화를 감지할 수 없음
- 페이지가 무엇을 렌더링 중인지에 대한 상태를 알 수 없음
    - 새로고침 시 처음 페이지로 돌아감
    - 링크를 공유하면 처음 페이지만 공유 가능
- 브라우저의 뒤로 가기 기능을 사용할 수 없음 

## Vue Router
- Vue 공식 라우터
- SPA 상에서 라우팅을 쉽게 개발할 수 있는 기능 제공
- routes에 컴포넌트를 매핑한 후, 어떤 URL에서 렌더링할지를 알려줌
    - SPA를 MPA처럼 URL을 이동하면서 사용가능
    - SPA의 단점 중 하나인 URL이 변경되지 않는다는 문제를 해결
- [참고] MAP(Multiple Page Application)
    - 여러 개의 페이지로 구성된 애플리케이션
    - SSR 방식으로 rendering

### Vue Router 시작하기
```shell
vue create project_name    // vue project 생성
cd vue project_name        // 디렉토리 이동
vue add router             // vue CLI를 통해 router plugin wjrdyd
```
> [주의] 기존에 프로젝트를 진행하고 있던 도중에 router를 추가하면 App.vue를 덮어 쓰므로 필요한 경우, 명령을 실행하기 전에 파일을 백업해두어야 함

- history mode 사용 여부 `Y`
```shell
Use history mode for router? (Requires proper server setup for index fallback in production) (Y/n) => Y
```

#### History mode
- 브라우저의 History API를 활용한 방식
    - 새로고침없이 URL 이동 기록을 남길 수 있음
    - URL 구조로 사용 가능 ( e.g.) http://localhost:8080`/index`
- [참고] History Mode를 사용하지 않으면 Default값인 hash mode로 설정됨('#'을 통해 URL을 구분하는 방식) 
    - e.g.) http://localhost:8080`#index`

### router-link
- a태그와 비슷한 기능 ->`URL을 이동시킴`
    - routes에 등록된 컴포넌트와 mapping됨
    - history mode에서 router-link는 클릭 이벤트를 차단하여 a 태그와 달리 브라우저가 페이지를 다시 load하지 않게 함
- 목표 경로는 `to`속성으로 지정됨
    - < router-link to="/" >Home</ router-link >
- 기능에 맞게 HTML에서 a태그로 rendering되지만, 필요에 따라 다른 태그로 바꿀 수 있음

### router-view
- 주어진 URL에 대해 일치하는 컴포넌트를 렌더링하는 컴포넌트
    - < router-view/>
- 실제 component가 DOM에 부착되어 보이는 자리를 의미
- router-link를 클릭하면 routes에 mapping된 컴포넌트를 렌더링함
- Django의 block tag와 유사 

### src/router/index.js
- router에 관련된 정보 및 설정이 작성되는 곳
- Django의 urls.py와 유사
- routes에 URL과 컴포넌트를 mapping
```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import HelloView from '@/views/HelloView.vue'

Vue.use(VueRouter)
const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
]
```
```python
urlpatterns=[
    path('', views.home, name='home'),
]
```

### src/views
- views/
    - router-view에 들어갈 컴포넌트 작성
    - < router-view >의 위치에 렌더링 되는 컴포넌트를 모아두는 폴더
    - Views에 들어가는 컴포넌트는 router과 mapping되는 컴포넌트들
    - 다른 컴포넌트와 구분하기 위해 이름에 View로 끝나도록 만들기
        - e.g.) AboutView.vue, HomeView.vue,...
- components/ 
    - 나머지는 기존 컴포넌트를 작성하던 곳(src/components)으로 감
    - router와 매핑되지 않는, 하위 컴포넌트들이 들어감
        - e.g. ) HomeView 컴포넌트 내부의 HelloWorld 컴포넌트

### Vue Router 실습
- 주소를 이동하는 2가지 방법
    1. 선언적 방식 내비게이션
    2. 프로그래밍 방식 내비게이션   

동작 원리는 동일

---
1. 선언적 방식 내비게이션
- router-link의 `to` 속성으로 주소 전달
- routes에 등록된 주소와 매핑된 컴포넌트로 이동
    - router/index.js에서 정한 각 컴포넌트의 name
    - router를 연결하고자 하는 상위 컴포넌트
    ```js
    <router-link :to="{ name: 'home'}">Home</router-link>
    ```
2. `프로그래밍 방식 내비게이션`
- Vue 인스턴스 내부에서 라우터 인스턴스에 `$router`로 접근할 수 있음
- 다른 URL로 이동하려면 `this.$router.push`를 사용
    - history stack에 이동할 URL을 넣는(push)하는 방식
    - history stack에 기록이 남기 때문에 사용자가 브라우저의 뒤로가기 버튼을 클릭하면 이전 URL로 이동할 수 있음
```html
// AboutView.vue
<template>
  <div class="about">
    <h1>This is an about page</h1>
    <!-- 선언적 방식 -->
    <router-link :to="{ name : 'home' }">to Home!</router-link>
    <!-- 프로그래밍적 방식 -->
    <button @click="toHome">to Home</button>
  </div>
</template>

<script>
  export default {
    name: 'AboutView',
    methods: {
      toHome(){
        this.$router.push({ name : 'home' })
      }
    }
  }
</script>
```
#### Dynamic Route Matching
- 동적 인자 전달
    - URL의 특정 값을 변수처럼 사용할 수 있음
- Django의 variable routing
- `params`를 이용하여 동적 인자 전달 가능
```html
<template>
  <div>
    <h1>hello, {{ userName }}</h1>
  </div>
</template>

<script>
export default {
    name: 'HelloView',
    data() {
        return {
            userName : this.$route.params.userName
        }
    }
}
</script>

<style>
</style>
```
- AboutView에서 데이터를 입력받아 HelloView로 이동하여 입력받은 데이터를 보여주기
```html
<template>
  <div class="about">
    <div>
        <!-- enter 누르면 methods:goToHello로 이동 -->
      <input type="text" @keyup.enter="goToHello" v-model="inputData">
    </div>
  </div>
</template>

<script>
  export default {
    name: 'AboutView',
    data() {
      return {
        // 사용자가 입력한 데이터 inputData
        inputData: null,
      }
    },
    methods: {
      goToHello() {
        // 이름: hello , 파라미터 - userName 으로 사용자가 입력한 inputData 보내줌
        this.$router.push({ name : 'hello', params: { userName : this.inputData }})
      }
    }
  }
</script>
```
```js
// router/index.js
  const routes = [
    {
        path: '/hello/:userName', // :~~  params들어갈 자리
        name: 'hello',
        component: HelloView,
    }
  ]

```
- 위 parameter를 HelloView에서 data로 받아서 (this.$route.params.userName) 화면에 보여줌

#### route에 컴포넌트를 등록하는 또 다른 방법
- router/index.js 에 컴포넌트를 등록하는 2가지 방법
    1. 기본
    2. lazy-loading(지연 로딩)
```js
const routes = [
// basic
  {      
    path: '/',
    name: 'home',
    component: HomeView
  },
// lazy-loading
  {
    path: '/about',
    name: 'about',
    component: () => import('../views/AboutView.vue')
  },
]
```
##### lazy-loading
- 모든 파일을 한 번에 로드하려고 하면 모든 걸 다 읽는 데 시간이 매우 오래 소요됨
- 미리 로드를 하지 않고 특정 route에 방문할 때 mapping된 컴포넌트의 코드를 로드하는 방식으로 활용할 수 있음
    - 모든 파일을 한 번에 로드하지 않아도 되기 때문에 최초에 로드하는 시간이 빨라짐
    - 당장 사용하지 않을 컴포넌트는 미리 로드하지 않는 것!  

`component: () => import('../views/AboutView.vue')`

## Navigation Guard
- Vue router를 통해 특정 URL에 접근할 때 `다른 url로 redirect`를 하거나 `해당 URL로의 접근을 막는` 방법
    - e.g.) 사용자의 인증 정보가 없으면 특정 페이지에 접근하지 못하게 함
https://v3.router.vuejs.org/guide/advanced/navigation-guards.html

### Navigation Guard 종류
#### 1. 전역 가드 (Global Before Guard)
- `다른 url 주소로 이동할 때` 항상 실행
- router/index.js에 `router.beforeEach()`를 사용하여 설정
- 콜백 함수의 값으로 다음 3개의 인자를 받음
    - `to`: `이동할` URL 정보가 담긴 Route 객체
    - `from`: `현재` URL 정보가 담긴 Route 객체
    - `next`: 지정한 URL로 이동하기 위해 호출하는 `함수`
        - 콜백 함수 내부에서 반드시 한 번만 호출되어야 함
        - 기본적으로 to에 해당하는 URL로 이동
- URL이 변경되어 화면이 전환되기 직전 router.beforeEach()가 호출됨
    - 화면이 전환되지 않고 `대기상태`가 됨
- 변경된 URL로 라우팅 하기 위해서는 `next()`를 호출하여 주어야 함
    - `next()가 호출되기 전까지 화면이 전환된지 않음`

```js
const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

router.beforeEach((to, from, next) => {
  console.log(to)
  console.log(from)
  console.log(next)
  // next() : next()를 호출하지 않으면 화면이 전환되지 않고 대기상태에서 멈춰있음
  next()
})

export default router
```
- 로그인 된 사용자의 경우 hello 페이지로 넘어가고, 로그인 되어있지 않은 경우 hello 페이지를 렌더링하지 않고 login 페이지로 이동됨
```js
// router / index.js
router.beforeEach((to, from, next) => {
  // 로그인 여부(임의값 : true)
  const isLoggedIn = true
//const isLoggedIn = false

  // 로그인이 필요한 페이지
  const authPages = ['hello', 'about']

  // isAuthRequired 의 값에 따라 로그인이 되어있지 않다면 Login 페이지로 이동
  const isAuthRequired = authPages.includes(to.name)

  if(isAuthRequired && !isLoggedIn) {
    next({ name: 'login' })
  } else {
    next() // next에 인자가 없을 경우  to 로 이동
  }
})
```
- 로그인이 필요한 페이지가 너무 많으면 반대로 로그인이 필요하지 않은 페이지 list를 만들 수도 있음
```js
// router / index.js
router.beforeEach((to, from, next) => {
  // 로그인 여부(임의값 : true)
  const isLoggedIn = true
  // const isLoggedIn = false

  // 로그인이 필요하지 않은 페이지
  const allowedPage = ['home', 'login']
 
  // isAuthRequired 의 값에 따라 로그인이 되어있지 않다면 Login 페이지로 이동
  const isAuthRequired = !allowedPage.includes(to.name)

  if(isAuthRequired && !isLoggedIn) {
    next({ name: 'login' })
  } else {
    next() // next에 인자가 없을 경우  to 로 이동
  }
})
```
#### 2. 라우터 가드
- 전체 route가 아닌 특정 route에 대해서만 가드를 설정하고 싶을 때 사용
- `beforeEnter()`
    - route에 진입했을 때 실행됨
    - 라우터를 등록한 위치에 추가
    - 매개변수, 쿼리, 해시 값이 변경될 때는 실행되지 않고, 다른 경로에서 탐색 될 때만 실행됨
    - 콜백 함수는 `to, from, next`를 인자로 받음

- 이미 로그인 되어있는 경우 HomeView로 이동하기
```js
const isLoggedIn = true   // 로그인 여부를 알려주는 변수 선언

const routes = [
  ...,
  {
    path: '/login',
    name: 'login',
    component: LoginView,
    // 라우터 가드는 라우터 안에서 작성해줌
    beforeEnter(to, from, next) {
      if( isLoggedIn === true ) {
        console.log('already logged in')
        next({ name: 'home' })
      }else {
        next()
      }
    }
  }
]
```
#### 3. 컴포넌트 가드
- 특정 컴포넌트 내에서 가드를 지정하고 싶을 때 사용
- `beforeRouteUpdate()`
    - 해당 컴포넌트를 렌더링하는 경로가 변경될 때 실행
- about에서 jun에게 인사하는 페이지로 이동
```html
// views/HelloView.vue
<script>
export default {
    name: 'HelloView',
    data() {
        return {
            userName : this.$route.params.userName
        }
    },
    // 해당 컴포넌트를 렌더링하는 경로가 변경될 때 실행
    beforeRouteUpdate(to, from, next){
        this.userName = to.params.userName
        next()
    }
}
</script>

```
### 404 NOT FOUND
- 사용자가 요청한 리소스가 존재하지 않을 때 응답 
```html
<!-- views/NotFound404.vue -->
<template>
  <div>
    <h1>404 NOT FOUND</h1>
  </div>
</template>

<script>
export default {
    name:'NotFound404',
}
</script>
```
```js
// router/index.js
import NotFound404 from '@/views/NotFound404'
  ...,
  {
    path: '/404',
    name: 'NotFound404',
    component: NotFound404,
  },
```
- 요청한 리소스가 존재하지 않을 때 404로 이동
    - 모든 경로에 대해서 404 page로 redirect
    - 기존에 명시한 경로가 아닌 경우 모든 경로가 404 page로 redirect됨
    - `routes에 최하단부에 작성하여야 함`
```js  
  {
    path: '*', // 현재 주소중에서 없는 주소는 모두 404로 redirect
    redirect: '/404'
  }
```
- 형식은 유효하지만 특정 리소스를 찾을 수 없는 경우 
    - e.g.) Django에게 articles/1으로 요청을 보냈지만, 1번 게시글이 삭제된 상태라면? 
    - 이때는 404page로 렌더링되는 것이 아니라 기존에 명시한 articles/:id/에 대한 component가 렌더링 됨
    - 하지만 데이터가 존재하지 않기 때문에 정상적으로 렌더링되지 않음
- then? 
    - 데이터가 없음을 명시
    - 404 페이지로 이동

- Dog API를 활용하여 동적 인자로 강아지 품종을 전달하여 품종에 대한 랜덤 이미지를 출력하는 페이지를 만들어보기
    - Axios 설치
    - DogView 컴포넌트 작성, routes에 작성
        - `*` router보다 상단에 등록하여야 함
```html
<template>
  <div>
    <h1>Dog</h1>
  </div>
</template>

<script>
export default {
    name:'DogView',
    
}
</script>
```
```js
// router/index.js
import DogView from '@/components/DogView'

  {
    path: '/dog/:breed',  // breed를 파라미터로 받아올 것임
    name: 'dog',
    component: DogView,
  },
```
```html
// view/DogView.vue
<template>
  <div>
    <h1>Dog</h1>
    <!-- 이미지가 아직 없다면 (v-if="!imgSrc") '로딩중'문구 출력 -->
    <h2 v-if="!imgSrc">{{ loadingMsg }}</h2>
    <!-- 이미지가 있다면 (v-if="imgSrc") img(v-bind:src) 출력 -->
    <img v-if="imgSrc" :src="imgSrc" alt="">
  </div>
</template>

<script>
import axios from 'axios';

export default {
    name:'DogView',
    data(){
        return {
            imgSrc:null,
            loadingMsg:'로딩중...',
        }
    },
    methods: {
        getDogImg() {
            const breed = this.$route.params.breed // 사용자가 파라미터에 입력한 breed 값을 가져옴
            const dogUrl = `https://dog.ceo/api/breed/${breed}/images/random`
            axios({
                method: 'get',
                url: dogUrl,
            })
            .then((response) => {
                // 이미지 Src를 응답받아온 데이터로 변경
                this.imgSrc = response.data.message
            })
            .catch((error) => { // 이미지를 받아오지 못했다면?
                // this.message = `${this.$route.params.breed}는 없는 품종입니다.` // 메시지를 출력하는 방법
                this.$router.push('/404')  // 404 not found페이지로 리다이렉팅
                // params는 route에, push는 router에
                console.log(error)
            })
        }
    },
    created(){
        // 컴포넌트 생성시 바로 이미지 보여줄 수 있도록 crated에서 method를 호출함
        this.getDogImg()
    }
}
</script>
```