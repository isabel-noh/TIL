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
    - createQueue() : 공백 상태의 큐를 생성
        - front = rear = -1
    - isEmpty() : 큐가 공백상태인지를 확인
    - isFull() : 큐가 포화상태인지를 확인
    - Qpeek() : 큐의 앞쪽(Front)에서 원소를 삭제없이 반환