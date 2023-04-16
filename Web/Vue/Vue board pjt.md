- 프로젝트 시작
```shell
vue crate project_name
cd project_name
vue add vuex
vue add router
```

### Optional Chaining
- Optional Chaining(`?.`) 앞의 평가 대상이 undefined이거나 null이면 error가 발생하지 않고 `undefined를 반환`
```js
const userInfo = {
    name : {
        last: 'Stark',
    },
    address: {
        city: 'Seoul',
    },
    getInfo(){
        console.log(this.name)
    }
}

// Optional Chaining 미사용
const myCity = userInfo.address && userInfo.address.city

// Optional Chaining 사용
const myCity = userInfo.address?.city

// Optional Chaining 사용(메서드 호출)
userInfo.getInfo?.()
```

#### Date in Javascript
- Javascript에서 시간을 나타내는 Date 객체는 1970년 1월 1일 UTC 자정과의 시간 차이를 밀리초로 나타내는 정수 값을 담음
    - `Date().toLocaleString()`을 사용하여 반환 가능
