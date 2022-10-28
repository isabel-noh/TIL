# 비동기와 프로미스

### Javascript Runtime
- javascript engine의 `Call Stack`
- `Web API`
- `Task queue`
- `Event loop`

### 비동기 처리 방식

- setTimeOut의 3000ms는 Web API에서 Task Queue로 3000ms뒤에 들어간다는 의미임. 
- 최소 지연 시간을 의미함.
- 꼭 3000ms 뒤에 실행된다는 의미는 아니다.
- Call Stack이 비어야 Task Queue에 있는 업무들이 call Stack으로 들어갈 수 있는 것이다. 
- 또한 Call Stack에 이미 다른 업무들이 미리 있어서 그 일을 처리하는 데에도 대기시간이 더 있을 수도 있다. 



## Axios
Javascript HTTP 웹 통신 라이브러리  
https://axios-http.com/kr/docs/intro  
https://github.com/kr/axios/axios  


## Callback & Promise
- 비동기 처리의 핵심은 Web API에 들어오는 순서가 아니라 작업이 완료되는 순서대로 처리됨

### Callback 함수

# Promise
비동기 처리를 위한 객체  
