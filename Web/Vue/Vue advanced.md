### computed
- Vue instance가 가진 options 중의 하나
- computed 객체에 정의한 함수를 페이지가 최초로 렌더링될 때 호출하여 계산
    - 계산 결과가 변하기 전까지 함수를 재호출하는 것이 아닌 계산된 값을 반환

#### method vs computed
- method 
    - 호출 될 때마다 함수를 실행
    - 같은 결과여도 매번 새롭게 계산함
- computed
    - 함수의 종속 대상의 변화에 다라 계산 여부가 결정됨
    - 종속 대상이 변하지 않으면 항상 캐싱(저장)된 값을 반환

### watch
- 특정 데이터의 변화를 감지하는 기능
    1. watch 객체를 정의
    2. 감시할 대상 data를 지정
    3. data가 변하면 시행할 함수를 정의
- 첫번째 인자는 변동 전 data (val)
- 두번째 인자는 변동 후 data (oldVal)
```html

  <div id="app">
    <h3>Increase number</h3>
    <p>{{ number }}</p>
    <button @click="number++">+</button>
    <hr>

    <h3>Change name</h3>
    <p>{{ name }}</p>
    <input type="text" v-model="name">
    <hr>

    <h3>push myObj</h3>
    <p>{{ myObj }}</p>
    <button @click="itemChange">change Item</button>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        number: 0,
        name: '',
        myObj: {completed: true}
      },
      methods: {
        nameChange: function () {
          console.log('name is changed')
        },

        itemChange: function () {
          this.myObj.completed = !this.myObj.completed
        }
      },
      watch: {
        number: function (val, oldVal) {
          console.log(val, oldVal)
        },

        name: {
          handler: 'nameChange' //method를 호출할 때는 handler라는 key값을 사용하여야 함. 
          // 여기서 'nameChange'는 함수 이름
        },

        myObj: {
          handler: function (val) {
            console.log(val)
          },
          deep: true // 한 겹 아래(배열이나 객체.. 둥)에 있는 값을 감시하려면 deep:true라는 옵션을 넣어줘야 watch할 수 있음 (depth가 하나 더 깊기 때문)
        },
      }
    })
  </script>
```
- 실행 함수를 Vue method로 대체 가능
    1. 감시 대상 data의 이름으로 객체 생성
    2. 실행하고자 하는 method를 handler에 문자열 형태로 할당
- Array, Object의 내부요소변경을 감지하기 위해서는 `deep`속성 추가 필요

### filter 
- 텍스트 형식화를 적용할 수 있는 필터
- interpolation 혹은 v-bind를 이용할 때 사용 가능
- 필터는 자바스크립트 표현식 마지막에 `|`와 함께 추가되어야
- filter함수는 chaining 가능

```html
<body>
  <div id="app">
    <p>{{ numbers | getOddNums |getUnderTenNums }}</p> <!--filter함수 chaining가능-->
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15],
      },
      filters: {
        getOddNums: function (nums) {  // 위의 p태그의 numbers가 여기 filter 함수의 nums인자로 들어옴
          const oddNums = nums.filter((num) => {
            return num % 2
          })
          return oddNums
        },
        
        getUnderTenNums: function (nums) {
          const underTen = nums.filter((num) => {
            return num < 10
          })
          return underTen
        }
      }
    })
  </script>
</body>
```