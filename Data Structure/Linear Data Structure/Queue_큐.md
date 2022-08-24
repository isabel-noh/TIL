# Queue(큐)
## Queue의 특성
- 삽입과 삭제의 위치가 제한적인 자료구조
- 선입선출 구조(FIFO: First In First Out)
    - 큐에서 삽입한 순서대로 원소가 저장되어, 가장 먼저 삽입(First In)된 원소는 가장 먼저 삭제(First Out)됨
    - Front(머리) : 저장된 원소 중 첫번째 원소(혹은 삭제된 위치)
    - Rear(꼬리) : 저장된 원소 중 마지막 원소
- 주요 연산
    - `enQueue(item)` : 큐의 뒤쪽(rear 다음)에 원소를 삽입
        - rear += 1
        - Q[rear] = 'A' 삽입
    - `deQueue()` : 큐의 앞쪽(front)에서 원소를 삭제하고 반환
        - 마지막으로 꺼낸 자리
        - front += 1
    - `createQueue()` : 공백 상태의 큐를 생성
        - q = []   /  q = [0] * N  (N 크기의 큐 생성)
        - front = rear = -1
    - `isEmpty()` : 큐가 공백상태인지를 확인
        - if front == rear : 큐가 비어있는 상태
    - `isFull()` : 큐가 포화상태인지를 확인
    - `Qpeek()` : 큐의 앞쪽(Front)에서 원소를 삭제없이 반환

## Queue의 구현
### 선형큐
- 1차원 배열을 이용한 큐
    - 큐의 크기 = 배열의 크기
    - front: 저장된 첫번째 원소의 인덱스
    - rear: 저장된 마지막 원소의 인덱스
- 상태 표현
    - 초기 상태: front = rear = -1
    - 공백 상태: front == rear
    - 포화 상태 : rear == n-1 (n: 배열의 크기, n-1: 배열의 마지막 인덱스)

#### 삽입: enQueue(item)
마지막 원소 뒤에 새로운 원소를 삽입하기 위해  
- rear값을 하나 증가시켜 새로운 원소를 삽입할 자리 마련
- 그 인덱스에 해당한느 배열 원소 Q[rear]에 item 저장
```python
def enQueue(item):
    global rear
    if isFull():
        print("Queue Full")
    else:
        rear += 1
        Q[rear] = item
```

#### 삭제: deQueue()
가장 앞에 있는 원소를 삭제하기 위해  
- front 값을 하나 증가시켜 큐에 남아있게 될 첫번째 원소 이동
- 새로운 첫번째 원소를 return함으로써 삭제와 동일한 기능
```python
def deQueue():
    global front
    if isEmpty():   # front == rear 
        print('queue_empty')
    else: 
        front += 1
        return Q[front]
```
#### 공백상태 및 포화상태 검사
- 공백상태: front == rear
- 포화상태: rear == n-1
```python
def isEmpty():
    return front == rear
def isFull():
    return rear == len(Q)-1
```

#### 검색: Qpeek()
- 가장 앞에 있는 원소를 검색하여 반환
- 현재 front의 한자리 뒤 (front+1)에 있는 원소
- 즉 큐의 첫 번째 자리의 원소 반환
```python
def Qpeek():
    if isEmpty():
        print('queue_empty')
    else:
        return Q[front+1]
```

### 선형 큐 이용시의 문제점 
    - 잘못된 포화상태 인식  
    선형 큐를 이용하여 원소의 삽입과 삭제를 계속할 경우, 배열의 앞부분에 활용할 수 있는 공간이 있음에도, rear=n-1 즉 포화상태로 인식하여 더 이상의 삽입을 수행하지 않게 됨  
    - 해결방법 : 원형 큐

### 원형 큐  
일차원 배열을 사용하되, 논리적으로는 배열의 처음과 끝이 연결되어 원형 형태의 큐를 이룬다고 가정하고 사용
-  초기 공백상태
    - front = rear = 0
-  index의 순환
    - front와 rear의 위치가 배열의 마지막 인덱스인 n-1을 가리킨 후, 그 다음에는 논리적 순환을 이루어 배열의 처음 인덱스인 0으로 이동하여야 함
    - 이를 위해 나머지 연산자 mod`(%)`를 사용
-  front 변수
    - 공백상태와 포화상태 구분을 쉽게 하기 위하여 front자리는 사용하지 않고 항상 빈자리로 둠
-  삽입위치와 삭제위치
    - 삽입위치: rear = (rear+1) mod n
    - 삭제위치: front = (front+1) mod n

#### 공백상태와 포화상태: isEmpty(), isFull()
- 공백상태: rear == front
- 포화상태: front == (rear+1) % N
```python
def isEmpty():
    return front == rear
def isFull():
    return (rear+1) % len(cQ) == front
```

#### enQueue(item)
마지막 원소 뒤에 새로운 원소를 삽입하기 이해
- rear값을 조정하여 새로운 원소를 삽입할 자리 마련
    - rear = (rear+1) mod n
- 그 인덱스에 해당하는 배열원소 cQ[rear]에 item저장
```python
def enQueue(item):
    global rear
    if isFull():
        print('queue_full')
    else:
        rear = (rear + 1) & len(cQ)
        cQ[rear] = item
```
#### deQueue(), delete()
가장 앞에 있는 원소 삭제  
- front값을 조정하여 삭제할 자리 준비
- 새로운 front 원소를 return하여 삭제와 동일한 기능을 수행
```python
def deQueue():
    global front
    if isEmpty():
        print('queue_empty')
    else:
        front = (front + 1) % len(cQ)
        return cQ[front]
```
## 우선순위 큐(Priority Queue)
- 우선순위를 가진 항목들을 저장하는 큐
- FIFO순서가 아니라 우선순위가 높은 순서대로 나가게 됨

> [적용분야]
> - 시뮬레이션 시스템
> - 네트워크 트래픽 제어
> - 운영체제의 테스크 스케줄링

- 우선순위 큐의 구현
    - 배열 활용
    - 리스트 활용
- 우선순위 큐의 기본 연산
    - 삽입: enQueue
    - 삭제: deQueue

### 배열을 이용하여 우선순위 큐 구현
    - 원소를 삽입하는 과정에서 우선순위를 비교하여 적절한 위치에 삽입
    - 가장 앞에 있고 최고 우선순위의 원소가 위치하게 됨

    - 문제점 
    배열을 사용하므로, 삽입이나 삭제연산이 일어날 때 원소의 재배치 발생 > 소요되는 시간 및 메모리 낭비가 큼

