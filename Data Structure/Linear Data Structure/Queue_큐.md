# Queue(큐)
## Queue의 특성
- 삽입과 삭제의 위치가 제한적인 자료구조
- 선입선출 구조(FIFO: First In First Out)
    - 큐에서 삽입한 순서대로 원소가 저장되어, 가장 먼저 삽입(First In)된 원소는 가장 먼저 삭제(First Out)됨
    - Front(머리) : 저장된 원소 중 첫번째 원소(혹은 삭제된 위치)
    - Rear(꼬리) : 저장된 원소 중 마지막 원소
- 주요 연산
    - enQueue(item) : 큐의 뒤쪽(rear 다음)에 원소를 삽입
        - rear += 1
        - Q[rear] = 'A' 삽입
    - deQueue() : 큐의 앞쪽(front)에서 원소를 삭제하고 반환
        - 마지막으로 꺼낸 자리
        - front += 1
    - createQueue() : 공백 상태의 큐를 생성
        - q = []   /  q = [0] * N  (N 크기의 큐 생성)
        - front = rear = -1
    - isEmpty() : 큐가 공백상태인지를 확인
        - if front == rear : 큐가 비어있는 상태
    - isFull() : 큐가 포화상태인지를 확인
    - Qpeek() : 큐의 앞쪽(Front)에서 원소를 삭제없이 반환

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
    if isEmpty(): 
        Queue_Empty()
    else: 
        front += 1
        return Q[front]
```