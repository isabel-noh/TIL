### Data in components
- MyChild에도 똑같은 data를 정의해야하나?
    - MyComponent의 data와 MyChild의 데이터가 동일한 데이터가 맞나?
    - MyComponent의 data가 변경된다면 MyChild도 같이 변경되나?
    - No. 각 Component는 독립적이므로 서로 다른 data를 갖게 될 것
    - 완전히 동일한 data를 서로 다른 Component에서 보여주려면? 

- 컴포넌트는 부모-자식 관계를 가지고 있으므로, `부모-자식 관계끼리만 데이터를 주고 받자!` 
    - 데이터의 흐름을 파악하기에 용이
    - 유지 보수 용이

# pass props & emit event
- 부모 => 자식으로의 데이터 흐름
    - pass props의 방식
- 자식 => 부모로의 데이터 흐름
    - emit event 방식


## Pass props 
- 요소의 속성(property)을 사용하여 데이터 전달
- props는 부모(상위)컴포넌트의 정보를 전달하기 위한 `사용자 지정 특성`
- 자식(하위) 컴포넌트는 props옵션을 사용하여 수신하는 `props를 명시적으로 선언`하여야 함
    - App.vue의 <HelloWorld/>요소에 msg="~"라는 property를 설정하였고, 하위 컴포넌트인 HelloWorld는 자신에게 부여된 msg property를 template에서 {{ msgTitle }}의 형태로 사용한 것
```vue
<!-- App.vue -->
<template>
  <div id="app">
    <!-- 3. 보여주기 -->
    <MyComponent />
    <HelloWorld msg-title ="Welcome to Your Vue.js App"/>
  </div>
</template>
<!-- HelloWorld.vue -->
<template>
  <div class="hello">
    <h1>{{ msgTitle }}</h1>
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  props: {
    msgTitle: String
  }
}
</script>   
```
- 부모 => 자식으로의 data 전달 방식을 pass props라고 함
- 정적인 데이터를 전달하는 경우, static props라고 명시하기도 함
- 요소에 속성을 작성하듯이 사용 가능하여, `prop-data-name="value"`의 형태로 데이터를 전달  
  - 속성은 kebab-case
- props 명시하여야 함
- 데이터를 받는 쪽, 하위 컴포넌트에서도 props에 대해 명시적으로 작성해주어야 함
- 전달받은 props를 type과 함께 명시
- 컴포넌트를 문서화할 뿐만 아니라, 잘못된 타입이 전달하는 경우, 브라우저의 자바스크립트 콘솔에서 사용자에게 경고를 뿌림

### Pass Props convention  
부모 템플릿에서 kebab-case로 넘긴 변수를 자식의 스크립트에서 자동으로 camelCase로 변환하여 인식
- 부모에서 넘겨주는 props
  - kebab-case
- 자식에서 받는 props
  - camelCase

 
## Emit event