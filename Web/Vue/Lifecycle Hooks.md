# Lifecycle Hooks
- 각 Vue 인스턴스는 생성과 소멸의 과정 중 단계별 초기화 과정을 거침
    - Vue 인스턴스가 생성된 경우, 인스턴스를 DOM에 마운트하는 경우, 데이터가 변경되어 DOM을 업데이트 하는 경우 등
- Lifecycle Hooks : 각 단계가 트리거가 되어 특정 로직을 실행할 수 있음

![vue LifeCycle](https://wormwlrm.github.io/static/1d3dae65499d59846dfbfaaa7daae963/a6d36/1.png)

### created
- Vue instance가 생성된 후 호출됨
- data, computed 등의 설정이 완료된 상태
- 서버에서 받은 데이터를 vue instance의 data에 할당하는 로직을 구현하기에 적합
- 단, mount되지 않아 요소에 접근할 수는 없음(DOM과는 연결되지 않은 상태)
> - 버튼을 클릭하지 않아도 첫 실행시 기본 사진이 출력되도록 하고싶다면? 
>     - created 함수에 강아지 사진을 가져온느 함수를 추가  
```js
// App.vue
<template>
  <div id="app">
    <button @click="toggle">toggle</button>
    <DogComponent/>
  </div>
</template>

<script>
import DogComponent from '@/components/DogComponent'

export default {
  name: 'App',
  data() {
    return {
      flag: true
    }
  },
  methods: {
    toggle() {
      this.flag = !this.flag
    }
  },
  components: {
    DogComponent,
  },
  created() {
    console.log('App created!')
  },
  mounted() {
    console.log('App mounted!')
  },
}
</script>
```
```html
// DogComponent.vue
<template>
  <div>
    <button @click="getDogImage">멍멍아 이리온</button><br><br>
    <img v-if="imgSrc" :src="imgSrc" alt="#"><br>
  </div>
</template>


<script>
import axios from 'axios'

export default {
  name:'DogComponent',
  data() {
    return {
      imgSrc: null,
    }
  },
  methods:{
    getDogImage() {
      const dogImageSearchURL = 'https://dog.ceo/api/breeds/image/random'
      
      axios({
        method: 'get',
        url: dogImageSearchURL
      })
        .then((response) => {
          const imgSrc = response.data.message
          this.imgSrc = imgSrc
        })
        .catch((error) => {
          console.log(error)
        })
    }
  },
  created(){  // 페이지가 처음에 렌더링될 때 버튼을 클릭하지 않아도 바로 api에 사진을 요청하여 보여줄 수 있게 함
    this.getDogImage()
  },
}
</script>

<style>
</style>

```
### mounted
- Vue instance가 요소에 mount된 후 호출됨
- mount된 요소를 조작할 수 있음
```js
...,
mounted(){  // Vue instance가 생성되고 DOM에 연결된 이후에 시점에 실행되기 때문에 DOM에 대한 접근 및 수정이 가능
    const button = document.querySelector('button')
    button.innerText = 'woof, woof!'
},
```
- 위 내용의 코드를 created시점에 적용하려고 하면 에러 발생 -> 'null 값에 innerText를 시행할 수 없다.'
    - created 시점에는 DOM에 연결되지 않았기 때문에 동작할 수 없음

### updated
- 데이터가 변경되어 DOM에 영향을 줄 때 시행됨
```js
updated(){
    console.log('new doggies')
},
```

## Lifecycle Hooks의 특징
- instance마다 각각의 lifecycle을 가지고 있음
- Lifecycle Hooks는 컴포넌트 별로 정의할 수 있음
- 위 project의 경우,  
`App.vue created -> ChildComponent created -> ChildComponent mounted -> App.vue mounted -> ChildComponent updated` 순으로 동작
- 부모 컴포넌트의 mounted hook이 실행되었다고 해서 자식이 mounted 되는 것이 아니고, 부모 컴포넌트가 updated hook이 실행되었다고 해서 자식이 updated되는 것도 아님
    - 부착 여부가 부모-자식 관계에 따라 순서를 가지지 않음
- `instance마다 각각의 lifecycle을 가지고 있기 때문`


### Todo with Vuex
#### 개요
- Vuex를 사용한 Todo project 만들기
- 구현 기능
    - Todo CRUD
    - Todo 개수 계산
        - 전체 Todo
        - 완료된 Todo
        - 미완료된 Todo

