# Vuex
## State Management
### 상태 관리(State Management)
- 상태(State): 현재에 대한 정보(data)
- 현재 App이 가지고 있는 data
- 각 component는 독립적이기 때문에 각각의 상태(data)를 가짐
- componenet들이 모여서 하나의 App을 구성
    - 여러 개의 component가 같은 상태(data)를 유지할 필요가 있음 => `상태관리(State Management) 필요!`

#### Pass Props & Emit Event
- 지금까지 props와 event를 이용하여 상태 관리를 하고 있음
- 각 컴포넌트는 독립적으로 데이터를 관리
- 같은 데이터를 공유하고 있으므로, 각 컴포넌트가 동일한 상태를 유지하고 있음
- 데이터의 흐름을 직관적으로 파악 가능 
---
- component 중첩이 깊어지면 데이터 전달이 쉽지 않음
- 공통의 상태를 유지해야 하는 component가 많아지면 데이터 전달 구조가 복잡해짐

### Centralized Store
- `중앙 저장소(store)애 데이터를 모아서 상태 관리`
- 각 component는 중앙 저장소의 데이터를 사용
- component의 계층에 상관없이 중앙 저장소에 접근하여 데이터를 얻거나 변경할 수 있음
- 중앙 저장소의 데이터가 변경되면 각각의 component는 해당 데이터의 변화에 반응하여 새로 변경된 데이터를 반영함
- 규모가 크거나 component 중첩이 깊은 project의 관리가 매우 편리

## Vuex
### Vuex
- `State management pattern + Library` for vue.js(상태관리패턴 + 라이브러리)
- 중앙 저장소를 통해 상태 관리를 할 수 있도록하는 라이브러리
- 데이터가 예측 가능한 방식으로만 변경될 수 있도록하는 규칙을 설정하며, Vue의 반응성을 효율적으로 사용하는 상태 관리 기능을 제공 

### Vue 시작하기
```shell
vue create [project_name]
cd [project_name]
vue add vuex   // vue CLI를 통해 vuex plugin 적용
```
- src/store/index.js가 생성됨
- vuex의 핵심 컨셉 4가지
    - state
    - getters
    - mutations
    - actions

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
  },
  getters: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
})

```
![vuex](https://user-images.githubusercontent.com/89833631/200209263-6d6ea276-7e57-407c-b6af-a434dd14003a.png)

#### 1. State
- vue 인스턴스의 data에 해당
- 중앙에서 관리하는 모든 상태 정보
- 개별 component는 state에서 데이터를 가져와서 사용
    - 개별 component가 관리하던 data를 중앙 저장소(Vuex Store의 state)에서 관리하게 됨
- state의 데이터가 변화하면 해당 데이터를 사용(공유)하는 component도 자동으로 다시 렌더링됨
- `$store.state`로 state 데이터에 접근

#### 2. Mutations
- 실제로 `state를 변경하는 유일한 방법`
- vue instance의 methods에 해당하지만 Mutations에서 호출되는 핸들러(handler)함수는 반드시 `동기적`
    - 비동기 로직으로 mutations를 사용하여 state를 변경하는 경우, state의 변경 시기를 특정할 수 없기 때문
- 첫번째 인자 : state, component 혹은 Actions에서 commit()메서드로 호출됨    
> handler 함수 : mutations, action에서 호출되는 함수

#### 3. Actions
- mutations와 비슷하지만 `비동기 작업`을 포함할 수 있다는 차이가 있음
- `state를 직접 변경하지 않고 commit()메서드로 mutations를 호출하여 state를 변경함`
- context 객체를 인자로 받으며, 이 객체를 통해 store.js의 모든 요소와 메서드에 접근할 수 있음(== 즉 state를 직접 변경할 수 있지만 하지 말아야 함)
- 비동기 작업이 포함될 수 있는 (외부 API와의 소통 등) methods
- component에서 `dispatch()`메서드에 의해 호출됨
- 첫번째 인자는 context, 두번째 인자는 payload(넘겨준 데이터를 받아서 사용)

#### Mutations & Actions
- vue component의 methods역할이 vuex에서는 아래와 같이 분화됨
- Mutations 
    - state를 변경
- Actions
    - state 변경을 제외한 나머지 logic
![mutations_and_acrtions](https://user-images.githubusercontent.com/89833631/200210114-350509d0-db3c-46d4-89ef-b077655b0032.png)

#### 4. Getters
- vue instance의 computed에 해당
- `state를 활용하여 계산된 값을 얻고자 할 때 사용, state의 원본 데이터를 건들지 않고 계산된 값을 얻을 수 있음`
- computed와 마찬가지로 getters의 계산 결과는 캐시cache되며, 종속된 값이 변경된 경우에만 재계산됨
- getters에서 계산된 값은 state에 영향을 주지 않음
- 첫번째 인자로 state, 두번째 인자로 getter을 받음

> ##### 모든 데이터를 vuex에서 관리해야하나?   
> vuex를 사용한다고 하여 모든 데이터를 state에 넣어야하는 것은 아님
> - vuex에서도 여전히 pass props, emit event를 사용하여 상태를 관리할 수 있음

##### component에 관한 데이터의 흐름
- component에서 데이터를 조작하기 위한 데이터의 흐름
    - component => (actions) => mutations => state
- component에서 데이터를 사용하기 위한 데이터의 흐름
    - state => (getters) => component


### Vuex 실습
- Object method shorthand
- 객체 메서드 축약형 사용
```js
//before
const obj1 = {
    addValue : function (value) { 
        return value
    },
}

// from now
const obj2 = {
    addValue(value) {
        return value
    },
}
```

```js
// App.vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- 별도의 선언없이 바로 store에 접근 가능 -->
    <!-- <h1>{{ $store.state.message }}</h1>  -->
    <!-- but 바로 접근하기보다 computed에 정의 후 접근하는 것을 권장함 -->
    <h1>{{ message }}</h1>  
    <input type="text" name="inputValue" @keyup.enter="changeMsg" v-model="inputValue">
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data(){
    return {
      inputValue:null,
    }
  },
  computed : {
    message(){
      return this.$store.state.message
    }
  },
  methods : {
    changeMsg (message) {
      const newMsg = this.inputValue
      this.$store.dispatch('액션 메서드', newMsg)
      this.inputValue = null
    }
  }
}
</script>
```
- context는 store의 전반적인 속성을 모두 가지고 있으므로 context.state와 context.getters를 통해 mutations를 호출하는 것이 모두 가능
- dispatch()를 사용하여 다른 actions를 호출할 수도 있음
    - actions에서 state를 직접 조작하는 것은 삼가야 함
- payload : 넘겨준 데이터를 받아서 사용
```js
// src/store/index.js
...
export default new Vuex.Store({
  ...,
  actions: {
    changeMsg(context, newMsg){
      console.log(context)
      console.log(newMsg)
    }
  },
})
```
- mutations
    - actions에서 commit()을 통해 mutations 호출하기
        - component 혹은 actions에서 commit()에 의해 호출됨
    - commit (A, B)
        - A : 호출하고자하는 mutations 함수
        - B : payload(추가 data)
    - mutations 이름은 대문자로 ! 
    - mutations 함수의 1st argument: `state`, 2nd argument: `payload`
```js
// src/store/index.js
export default new Vuex.Store({
    ...,
    mutations: { // mutations : state 조작
        CHANGE_MESSAGE(state, newMsg) {
            // console.log(state)
            // console.log(newMsg)
            state.message = newMsg
        }

    },
    actions: {
        changeMsg(context, newMsg){
            // context.commit('mutation_method_name', payload)
            context.commit('CHANGE_MESSAGE', newMsg)
        }
    }
})
```
- getters
    - 1st argument: state, (2nd argument: getters)
```js
// src/store/index.js
export default new Vuex.Store({
    getters:{
        messageLength(state){
            return state.message.length
        },
        // messageLength를 이용하여 새로운 값을 계산
        doubleLength(state, getters){
            return getters.messageLength * 2
        }
    }
})
```
```js
// App.vue
<script>
export default{
    name:'App',
    ...,
    computed: {
        ...,
        messageLength(){
            return this.$store.getters.messageLength
        },
        messageDoubleLength(){
            return this.$store.getters.doubleLength
        },
    }
}
</script>
```