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
##### init project
- project 생성 및 vuex plugin 추가
```shell
vue create todo-vuex-app
cd todo-vuex-app
vue add vuex
```
#### READ / CREATE
- Vue 컴포넌트의 method에서 `dispatch()`를 사용하여 actions 메서드를 호출
- Actions에 정의된 함수는 `commit()`을 사용하여 mutations를 호출
- Mutations에 정의된 함수가 최종적으로 state 변경

```js
// App.vue
<template>
  <div id="app">
    <h1>TodoList</h1>
    <TodoList />
    <TodoForm />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import TodoForm from '@/components/TodoForm';
export default {
  name: 'App',
  components: {
    TodoList,
    TodoForm, 
  },
}
</script>
```
```js
// TodoForm.vue
<template>
  <div>
    <input 
        type="text" 
        v-model.trim="todoTitle"
        @keyup.enter="createTodo">
    <!-- v-model: 양방향 바인딩-->
  </div>
</template>

<script>
export default {
    name:'TodoForm',
    data(){
        return{
            todoTitle: null,
        }
    },
    methods:{
        createTodo(){
            // console.log(this.todoTitle)
            if(this.todoTitle){  // todoTitle이 공백이 아니라면 아래 시행
                this.$store.dispatch('createTodo', this.todoTitle)
                this.todoTitle = null
            }
        },
    }
}
</script>
```
```js
// src/store/index.js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    todos:[],
  },
  getters: {
  },
  mutations: {
    CREATE_TODO(state, todoItem){
      state.todos.push(todoItem)
    }
  },
  actions: { 
    createTodo(context, todoTitle){
      const todoItem = {
        title: todoTitle,
        isCompleted: false,
      }
      context.commit('CREATE_TODO', todoItem) // mutations 호출
    }
  },
  modules: {
  }
})

```
#### DELETE
- TodoListItem 컴포넌트에 삭제 버튼 및 deleteTodo 메서드 작성
```js
<template>
  <div>
    <div>{{ todo.title }}</div>
    <button
        @click="deleteTodo">DELETE</button>
  </div>
</template>

<script>
export default {
    name:'TodoListItem',
    props: {
        todo: Object, 
    },
    methods: {
        deleteTodo(){
            this.$store.dispatch('deleteTodo', this.todo)
            // this.$store.commit('DELETE_TODO', this.todo)
        }
    }
}
</script>
```
- deleteTodo 메서드에서 deleteTodo actions메서드 호출(dispatch)
- 삭제되는 todo 전달
- deleteTodo actions 메서드에서 DELETE_TODO mutations 메서드 호출(commit)
```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    todos:[
    ],
  },
  mutations: {
    DELETE_TODO(state, todoItem){
      const index = state.todos.indexOf(todoItem)
      state.todos.splice(index, 1)
    },
  },
  actions: { 
    // 딱히 작업이 없기 때문에 여기서는 생략하고 component의 method에서 mutation 호출하여도 됨
    deleteTodo(context, todoItem){
      context.commit('DELETE_TODO', todoItem)
    }
  },
})
```
- 전달된 todoItem에 해당하는 todo 삭제

### update
```js
<template>
  <div>
    <span
        @click="updateTodo">{{ todo.title }}</span>
  </div>
</template>

<script>
export default {
    name:'TodoListItem',
    props: {
        todo: Object, 
    },
    methods: {
        updateTodo(){
            this.$store.dispatch('updateTodo', this.todo)
        },
    }
}
</script>
```
```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    todos:[],
  },
  getters: {
  },
  mutations: {
    UPDATE_TODO(state, todoItem){
      // const index = state.todos.indexOf(todoItem)
      // state.todos[index].isCompleted = !state.todos[index].isCompleted 

      // map은 새로운 배열을 return함
      state.todos = state.todos.map((todo) => {
        if (todo === todoItem) {
          todo.isCompleted = !todo.isCompleted
        }
        return todo
      })
    }
  },
  actions: { 
    updateTodo(context, todoItem){
      context.commit('UPDATE_TODO', todoItem)
    }
  },
})

```
- css 스타일 적용하기
  - v-bind를 활용하여 isCompleted값에 따라 css class가 toggle 방식으로 적용되게하기
```js
<template>
  <div>
    <span
        @click="updateTodo"
        :class="{'is-completed': todo.isCompleted}" 
        >{{ todo.title }}</span>  <!--v-bind-->
  </div>
</template>
<style>
.is-completed {
    text-decoration: line-through;
}
</style>
```

#### 전체 todo 개수
- allTodosCount getters 
- state에 있는 todos 배열의 길이 계산
```js
// index.js
  getters: {
    allTodosCount(state){
      return state.todos.length
    }
  },
```
```js
// TodoList.vue
<template>
  <div>
    <h3>모든 todo 개수 : {{ todoCounts }}</h3>
    ...
  </div>
</template>

<script>
export default {
    ...,
    computed: {
        todoCounts(){
            return this.$store.getters.allTodosCount
        }
    }
}
</script>

<style>

</style>
```

### completed/uncompleted todo 개수
```js
getters: {
    // 1. 전체 todolist에서 isCompleted가 true인 것들만 filter해서 새로운 array를 만들어주고 그것의 길이를 구해주기
    completedTodoCount(state){
      // 새로운 배열 return
      const completedTodos = state.todos.filter((todo) => {
        return todo.isCompleted === true
      })
      return completedTodos.length
    },
    // 2. 전체 todoList길이에서 completedTodo의 개수를 빼주면 됨! 
    uncompletedTodoCount(state, getters){
      return state.todos.length - getters.completedTodoCount
    }
  },
```
```html
<template>
  <div>
    <h3>완료된 todo 개수 : {{ completedCounts }}</h3>
    <h3>미완료된 todo 개수 : {{ uncompletedCounts }}</h3>
  </div>
</template>

<script>
import TodoListItem from '@/components/TodoListItem'
export default {
    name:'TodoList',
    components:{
        TodoListItem,
    },
    computed: {
        completedCounts(){ 
            return this.$store.getters.completedTodoCount
        },
        uncompletedCounts(){
            return this.$store.getters.uncompletedTodoCount
        },
    }
}
</script>
```

## Local Storage  
- 브라우저의 local storage에 todo 데이터를 저장하여, 브라우저를 종료 후 다시 실행해도 데이터가 보존될 수 있도록 하기
### Window.localStorage
- Window가 제공하는 로컬 스토리지
- 브라우저에서 제공하는 저장공간 중 하나인 Local Storage에 관련된 속성
- 만료되지 않고 브라우저를 종료하고 다시 실행해도 데이터가 보존됨
- 데이터가 문자열 형태로 저장됨 (JSON처럼 {key:value}형태인데 문자열)
#### 관련 메서드
- setItem(key, value) - key, value 형태로 데이터 저장
- getItem(key) - key에 해당하는 데이터 조회
![localStorage](https://developer.mozilla.org/ko/docs/Web/API/Window/localstorage)

### local storage 실습
- todos 배열을 local storage에 저장하기
- 데이터가 문자열 형태로 저장되어야 하기 때문에 JSON.stringfy를 사용하여 문자열로 변환
- state를 변경하는 작업이 아니기 때문에 mutations가 아닌 actions에서 작성
```js
// index.js
  mutations:{ 

    LOAD_TODO(state) {
      const localStorageTodos = localStorage.getItem('todos')
      const parsedTodos = JSON.parse(localStorageTodos)
      state.todos = parsedTodos
    },
  },
  actions: { 
    createTodo(context, todoTitle){
      const todoItem = {
        title: todoTitle,
        isCompleted: false,
      }
      // console.log(todoItem)
      context.commit('CREATE_TODO', todoItem) // mutations 호출
      context.dispatch('saveTodosToLocalStorage')  // local storage에 저장하기 위하여 actions 호출. actions에서 actions 호출 가능함
    },
    // 딱히 작업이 없기 때문에 여기서는 생략하고 component의 method에서 mutation 호출하여도 됨
    deleteTodo(context, todoItem){
      context.commit('DELETE_TODO', todoItem)
      context.dispatch('saveTodosToLocalStorage')
    },
    updateTodo(context, todoItem){
      context.commit('UPDATE_TODO', todoItem)
      context.dispatch('saveTodosToLocalStorage')
    },
    saveTodosToLocalStorage(context){
      const jsonTodo = JSON.stringify(context.state.todos)
      localStorage.setItem('todos', jsonTodo)
    }
  },
```
```js
// App.vue
// created에서 localStorage에 넣은 todos를 불러오면 페이지 시작되면서 동시에 화면에서 보여줄 수 있음
  created(){
    this.$store.dispatch('loadTodo')
  }
```

#### vuex-persistedstate
- vuex state를 자동으로 브라우저의 Local Storage에 저장해주는 라이브러리 중 하나
- 페이지가 새로고침 되어도 Vuex state를 유지시킴
- Local Storage에 저장된 data를 자동으로 state로 불러옴
- https://github.com/robinvdvleuten/vuex-persistedstate

```shell
npm install veux-persistedstate
```
```js
// App.vue
import createPersistedState from 'vuex-persistedstate'

Vue.use(Vuex)

export default new Vuex.Store({
  plugins: [
    createPersistedState(),
  ],
  ...,
})
```
- 일전에 만들었던 LOAD TODOS 관련 methods를 모두 삭제하여도 자동으로 데이터를 local Storage에 저장하고, 불러옴

##### mutations로만 state를 변경하면 안되나?(가능은 함)
- 저장소의 각 concept(state, getters, mutations, actions)은 각자의 역할이 존재하도록 설계되어 있기 때문에 각 목적에 맞게 사용하는 것이 좋음