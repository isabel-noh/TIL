# Heap

힙은 일종의 완전 이진 트리이다.  
주로 우선순위 큐를 구현하는데 밑받침이 되는 자료구조로 쓰인다.  
트리 구조이기 때문에 삽입과 삭제에 `O(logN)`의 시간이 소요된다.

최소 힙, 최대 힙  
빠른 시간 안에 최대값과 최소값을 찾아낼 수 있다.

> 파이선 -> heapq heapify 등 라이브러리에서 함수와 구조를 제공

### 힙에서의 부모-자식 관계

힙은 완전 이진 트리 base 이기 때문에, 노드들 간의 부모-자식 관계가 성립하게 된다. 힙의 경우엔 보통의 완전 이진 트리와는 다르게 반정렬 상태(느슨한 정렬 상태)를 유지한다. `최대힙이라면 큰 값이 부모 노드쪽에, 최소힙이라면 작은 값이 부모 노드 쪽에 배치되는 것만 유지`하고 왼쪽 자식과 오른쪽 자식은 부모 노드보다 작은 값을 유지하기만 하면 된다.

### 구현 - Max Heap

```js
// 기본 세팅
class Heap {
  constructor() {
    this.heap = [null]; // 첫 원소는 사용 X
  }
}
```

배열의 첫 원소는 사용하지 않으므로 부모와 자식 간 다음의 관계가 성립한다.

> 완전 이진 트리의 일종이기 때문에 Binary Search tree에서의 부모-자식 간 관계와 유사하다.

- 왼쪽 자식의 index = `부모 index * 2`;
- 오른쪽 자식의 index = `(부모 index * 2) + 1`;
- 부모의 index = `Math.floor(자식의 인덱스 / 2)`;

```js
getParentIndex(i){
    return Math.floor(i / 2);
}

getLeftChildIndex(i){
    return i * 2;
}

getRightChildIndex(i){
    return i * 2 + 1;
}
```

## 삽입

마지막 노드에 들어온 값을 `push()`하여 배열의 맨 마지막에 삽입한다. 이 때 부모노드를 확인하면서 들어온 값이 부모노드보다 작은지 큰지를 확인하면서 위치를 교환 `swap()`해주며 정렬 `heapifyUp()`한다.

```js
swap(idx1, idx2){
    const temp = this.heap[idx1];
    this.heap[idx1] = this.heap[idx2];
    this.heap[idx2] = temp;
}

push(value){
    this.heap[this.heap.length] = value; // 배열의 맨 마지막에 값 넣기
    this.heapifyUp();
}

// 최대 힙에 맞게 제일 큰 노드를 최상단으로 맞춰주기 위해 가장 마지막에 들어온 노드의 인덱스를 변수로 둔다.
heapifyUp(){
    let curIndex = this.heap.length - 1;
    // 확인 중의 인덱스의 값이 부모 인덱스의 값보다 크면, swap하고, 현재 인덱스에 부모 인덱스를 재할당하여 while문에서 부모 인덱스를 확인
    while(this.heap[curIndex] > this.heap[this.getParentIndex(curIndex)]){
        this.swap(curIndex, this.getParentIndex(curIndex));
        curIndex = this.getParentIndex(curIndex);
    }
}
```

## 삭제/추출

힙에서 루트 노드가 가장 먼저 추출된다. 그 빈 자리는 트리의 맨 마지막에 있는 값을 가져와 채우고, 맨 마지막 노드를 삭제한다. 그리고 다시 트리를 정렬한다. 힙의 원칙에 맞게 정렬이 다 끝나면 처음에 추출했던 루트노드값을 리턴한다.

1. maxVal: 배열의 최상위 노드를 꺼낸다.
2. 루트 노드와 맨 끝에 있는 값을 교체한다.
3. 맨 마지막 노드를 삭제한다.
4. 변경된 노드와 자식 노드들을 비교하면서 정렬한다.
5. 자식 노드 둘보다 부모 노드가 크거나 가장 마지막 바닥까지 도달하지 않을 때까지 과정을 반복한다.
6. 2에서 제거한 루트 노드 값을 return 한다.

```js
poll(){
    let maxVal = this.heap[1];
    this.heap[1] = this.heap[this.heap.length - 1];
    this.heap.length--;

    this.heapifyDown();

    return maxVal;
}

// 최소 힙에 맞게 제일 작은  노드를 최상단으로 맞춰주기 위해 가장 마지막에 들어온 노드의 인덱스를 변수로 둔다.
heapifyDown(){
    let curIndex = 1;
    // curIndex가 마지막 노드가 아닐 때까지 반복
    while(this.heap[this.getLeftChildIndex(curIndex)] !== undefined){
        let biggerChildIndex = this.getLeftChildIndex(curIndex);

        if(this.heap[this.getRightChildIndex(curIndex)] !== undefined && this.heap[this.getRightChildIndex(curIndex)] > this.heap[this.getLeftChildIndex(curIndex)]
        ){
            biggerChildIndex = this.getRightChildIndex(curIndex);
        }
        // 자식 노드가 있다면 자식 노드 중에서 제일 큰 자식 노드의 값과 현재 노드의 값을 비교
        // 자식 노드 값이 더 크다면 swap하는 식으로 전체 트리를 heap의 구조에 맞게 정렬
        if(this.heap[curIndex] < this.heap[biggerChildIndex]){
            this.swap(curIndex, biggerChildIndex);
            curIndex = biggerChildIndex;
        } else {
            return;
        }

    }
}
```

## 전체 코드

```js
class Heap {
  constructor() {
    this.heap = [];
  }

  getParentIndex(i) {
    return Math.floor(i / 2);
  }

  getLeftChildIndex(i) {
    return i * 2;
  }

  getRightChildIndex(i) {
    return i * 2 + 1;
  }

  swap(idx1, idx2) {
    const temp = this.heap[idx1];
    this.heap[idx1] = this.heap[idx2];
    this.heap[idx2] = temp;
  }

  push(val) {
    this.heap[this.heap.length] = val;
    this.heapifyUp();
  }

  heapifyUp() {
    let curIdx = this.heap.length - 1;
    while (this.heap[curIdx] > this.heap[this.getParentIndex(curIdx)]) {
      this.swap(curIdx, this.getParentIndex(curIdx));
      curIdx = this.getParentIndex(curIdx);
    }
  }

  poll() {
    let maxVal = this.heap[0];
    if (maxVal === 12 || maxVal === 10 || maxVal === 8) {
      console.log("g", this.heap);
    }
    this.heap[0] = this.heap[this.heap.length - 1];
    this.heap.length--;
    this.heapifyDown();
    return maxVal;
  }

  heapifyDown() {
    let curIdx = 0;
    while (this.heap[this.getLeftChildIndex(curIdx)] !== undefined) {
      let biggerChild = this.getLeftChildIndex(curIdx);
      if (
        this.heap[this.getLeftChildIndex(curIdx)] <
        this.heap[this.getRightChildIndex(curIdx)]
      ) {
        biggerChild = this.getRightChildIndex(curIdx);
      }
      if (this.heap[curIdx] < this.heap[biggerChild]) {
        this.swap(curIdx, biggerChild);
        curIdx = biggerChild;
      } else {
        return;
      }
    }
  }
}
```

#### 힙 사용 예제

- 우선순위 큐를 구현하는데 사용한다.
- 게임엔진에서 각 액터의 우선순위를 정한다.
- 서버에서 많은 트래픽을 처리할 때 우선 처리해야 할 트래픽을 정한다.
- 시뮬레이션 시스템
- 네트워크 트래픽 제어
- 운영 체제에서의 작업 스케쥴링 (우선 순위가 높은 일을 바로 조회)
- 수치 해석적인 계산
