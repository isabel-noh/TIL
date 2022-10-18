# 알고리즘  
유한한 단계를 통해 문제를 해결하기 위한 절차나 방법  
컴퓨터가 어떤 일을 수행하기 위한 단계적 방법  

#### 컴퓨터 분야에서 알고리즘을 표현하는 방법 2가지
- 의사코드(Pseudo Code)
- 순서도  
> **보다 좋은 알고리즘을 이해하고 활용하는 것**  
주어진 문제를 해결하기 위해 여러 개의 다양한 알고리즘이 가능함  
-> 어떤 알고리즘을 사용하여야 하는가 ? 

#### 좋은 알고리즘 ?
- 정확성 : 얼마나 정확하게 동작하는가
- 작업량 : 얼마나 적은 연산으로 원하는 결과를 얻어내는가
- 메모리 사용량 : 얼마나 적은 메모리를 사용하는가
- 단순성 : 얼마나 단순한가
- 최적성 : 더이상 개선할 여지가 없이 최적화 되었는가

## 시간 복잡도(Time Complexity)  
실행되는 명령문의 개수를 계산 -> 실제 걸리는 시간을 대략적으로 측정  
### = 빅오(O) 표기법  
시간 복잡도 함수 중에서 가장 큰 영향력을 주는 n에 대한 항만을 표시  
계수(Coefficient)는 생략  
```
O(3n + 2) = O(3n) = O(n)
O(2n^2 + 10n + 100) = O(n^2)
O(4) = O(1)
```
빅오(O, big-O) : 입력값이 무한대로 향할 때, 함수의 상한을 설명하는 수학적 표기방법 (실행 시간)  
Amortized Insertion Time: 조회하는 데에는 O(1)의 비용 발생  
(크기가 용량만큼 차게 되면, 새로운 메모리 공간에 더 큰 크기의 배열을 할당하고 기존 데이터를 복사하는 작업으로 O(n)의 비용이 발생)

## 배열 
> 포인터(Pointer) : 메모리 영역을 1바이트 단위로 가리키는 주소

배열  
: 일정한 자료형의 변수들을 하나의 이름으로 열거하여 사용하는 자료구조   
: 값 또는 변수 엘리먼트의 집합으로 구성된 구조  
: 하나 이상의 인덱스 또는 키로 식별됨  
: 고정된 크기만큼의 연속된 메모리 할당 (-> 미리 크기를 지정하지 않고 자동으로 re-sizing하는 배열인 동적 배열이 생김)   

파이썬의 동적 배열 자료형 : List
초깃값을 작게 잡아 배열을 생성하고, 데이터를 추가하면서 꽉 채워지면 배열을 늘리고 모두 복사하는 방식
(정적 배열 자료형은 없음)

### 1차원 배열
별도의 선언 방법이 없다면 변수에 처음 값을 할당할 때 생성  
이름: 프로그램에서 사용할 배열의 이름  
```python
arr = [] 
arr = list()
arr = [1,2,3]
arr = [0] * 10
```

```python
arr = [i for i in range(2,9) if i%2==0]
# [2, 4, 6, 8]
```

## 정렬
2개 이상의 자료를 특정 기준에 의해 오름차순 혹은 내림차순으로 재배열하는 것  
> #### 대표적인 정렬 방식의 종류
> - 버블정렬
> - 카운팅 정렬
> - 선택 정렬
> - 퀵 정렬
> - 삽입 정렬
> - 병합 정렬

### 버블 정렬
인접한 두 원소를 비교하며 자리를 계속 교환하는 방식  
시간 복잡도: **O(n^2)**
```python
def BubbleSort(arr, n):
    for i in range(n-1, -1, -1):
        for j in range(i, n-1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
```
### 카운팅 정렬
항목들의 순서를 결정하기 위하여 집합에 각 항목이 몇개씩 있는지 세는 작업을 하여, 선형 시간에 정렬을 하는 효율적인 알고리즘  
> 정수나 정수로 표현할 수 있는 자료에 대해서만 적용 가능   

시간 복잡도: **O(n + k)**  # n은 리스트의 길이, k는 정수의 최대값
```python
def CountingSort(arr, sorted_arr, n):
    # arr = 입력배열(1~n)
    # sorted_arr = 정렬된 배열
    # count_arr = 카운트 배열
    sorted_arr = [0] * (n + 1)
    count_arr = [0] * (n + 1)
    for i in range(len(arr)):
        count_arr[arr[i]] += 1
    
    for i in range(1, len(count_arr)):
        count_arr[i] += count_arr[i-1]

    for i in range(len(sorted_arr)-1, -1, -1):
        count_arr[arr[i]] -= 1
        sorted_arr[count_arr[arr[i]]] = arr[i]
```
### 완전 검색 
문제의 해법이라고 생각할 수 있는 모든 경우의 수를 나열, 확인하는 방법  
= 브루트 포스/generate-and-test 기법  

> 자격평가시험 등에서 주어진 문제를 풀 때, 우선 완전 검색 기법으로 접근하여 해답을 도출한 후, 성능 개선을 위해 다른 알고리즘을 사용하고 해답을 확인할 것!

### 순열
서로 다른 것들 중에서 몇 개를 뽑아 한줄로 나열하는 것  
- 서로 다른 n개 중에서 r개를 나열하는 것 
    - nPr = n * (n-1) * (n-2) * ... * (n-r+1)
- n개 중에서 n개를 뽑는 것
    - nPn = n! 
    - = n * (n-1) * (n-2) * ... * 2 * 1

### 탐욕 알고리즘 
- 최적해를 구하는 데 사용되는 근시안적 방법  
- 여러 경우 중 하나를 결정해야 할 때 마다 그 순간에 최적이라고 생각돠는 것을 선택해 나가는 방식으로 진행하여 최종적인 해답에 도달  
- 각 선택의 시점에서 이루어지는 결정은 지역적으로는 최적이지만 그 선택들을 계속 수집하여 최종적인 해답을 만들었다고 해서 그것이 최적이라는 보장은 없음  
>1) 해 선택 : 현재 상태에서 부분 문제의 최적 해를 구한 뒤, 부분 해 집합에 추가(solution set)
>2) 실행 가능성 검사 : 새로운 부분해 집합이 실행가능한지를 확인  
>3) 해 검사 : 새로운 부분해 집합이 문제의 해가 되는지를 확인

- baby-gin
```python
num = 456789
c = [0] * 12 #6자리 수로부터 각 자리수를 추출하여 개수를 누적할 리스트
# 왜 0~9까지가 아니라 0~11까지의 list를 만들었을까? 
# run을 조사할 때 굳이 7까지만 조사하라는 조건을 붙여 연산을 더 하게 하지 않고 메모리만 더 쓰는 방법으로 연산을 간소화함   

for i in range(6):
    c[num%10] += 1
    num //= 10

triplet = run = 0

i = 0  # 0부터 9번까지 확인
while i < 10:

    if c[i] >= 3: # triplet 조사 (i가 몇 개 있는지 확인) 후 데이터 삭제
        c[i] -= 3
        triplet += 1
        continue

    if c[i] >= 1 and c[i+1] >= c[i+2] >= 1: # run조사 후 데이터 삭제
        c[i] -= 1
        c[i+1] -= 1
        c[i+2] -= 1
        run += 1
        continue
    i += 1

if triplet + run == 2 :
    print("baby gin")
else : 
    print("Lose")
```


## 2차원 배열
1차원 List를 묶어놓은 List  
2차원 이상의 다차원 list는 차원에 따라 index를 선언함  
2차원 리스트 선언 : 세로길이(행의 개수), 가로길이(열의 개수)가 필요  
파이썬에서는 데이터 초기화를 통해 변수 선언과 초기화가 가능함  

```python
# [참고]
# 3
# 1 2 3
# 4 5 6
# 7 8 9
N = int(input())
arr = [list(map(int, input().split())) for _ in range(N)]

N, M = map(int, input().split())
for i in range(N):
    for j in range(M):
        print(arr[i][j], end=' ')
    print()

```

### 리스트 순회
- 행의 우선 순회
```python
# i행 좌표
# j행 좌표
for i in range(N):
    for j in range(M):
        # 모든 원소에 대해 
        arr[i][j] #필요한 연산 수행
```
- 열 우선 순회
```python
for j in range(M):
    for i in range(N):
        arr[i][j]
```

- 지그재그 순회  
List의 행을 좌우로 순회하며 조사하는 방법
    - i가 짝수일 때 홀수일 때를 나눠서 if문 시행(i%2 == 1 or == 0)
    - 아래는 위 두가지 경우를 하나로 합친 경우
```python
n = len(arr)
m = len(arr[0])

for i in range(len(arr)):
    for j in range(len(arr[0])):
        arr[i][j + (m - 1 - 2*j) * (i % 2)]
```
### 델타를 이용한 2차 배열 탐색  
2차 배열의 한 좌표에서 4방향의 인접 배열 요소를 탐색하는 방법  
```python
arr[0...N-1][0...N-1] # NxN 배열
di = [0, 0, -1, 1] #상하좌우
dj = [-1, 1, 0, 0]
for i in range(N):
    for j in range(N):
        # for d in range(1, 3): # 처음엔 한칸 사방, 그다음엔 두칸 사방
        for k in range(4): #4방향이니까
            ni = i + di[k] 
            nj = j + dj[k] 
            # ni = i + di[k] * d 
            # nj = j + dj[k] * d
            if 0 <= ni < N and 0 <= nj < N: #유효한 index이면  
            # 예를 들어 0,0 을 기준으로 시작하면 오른쪽, 위는 없으니까 
                test(arr[ni][nj])
```

```python
for i in range(N):
    for j in range(M):
        for di, dj in [[0, 1], [1, 0], [0, -1], [-1, 0]]:
            ni, nj = i + di, j + dj
            if 0 <= ni < N and 0 <= nj < M:
                print(ni, nj)
```

### 전치 행렬
```python
# i : 행의 좌표 len(arr)
# j : 열의 좌표 len(arr[0])

for i in range(3):
    for j in range(3):
        if i < j:
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]

# 1 2 3        1 4 7 
# 4 5 6    >   2 5 8
# 7 8 9        3 6 9

```

### 부분집합  
- 부분 집합의 수 
    - 집합의 원소 : n개
    - 공집합을 포함한 부분집합의 개수 : 2^n
    - 각 원소를 부분집합에 포함시키거나 or 포함시키지 않는 2가지 경우를 모든 원소에 적용한 경우의 수 (2 * 2 * 2 * ... * 2를 n번 곱함)

### 비트 연산자
#### 비트 연산자
- `&` : 비트 단위로 AND 연산
- `|` : 비트 단위로 OR 연산
- `<<` : 피연산자의 비트 열을 왼쪽으로 이동시킴
- `>>` : 피연산자의 비트 열을 오른쪽으로 이동시킴  
>이진법에서 왼쪽으로 옮긴다는 것의 의미는 `2를 곱한다`는 것  
반대로 생각하면 오른쪽으로 옮기는 것은 `2로 나눈다`는 것을 의미

#### << 연산자 
- `1 << n` = 2^n   
원소가 n개일 경우의 모든 부분집합의 수  
= n번 비트  
= 비트 n 

#### & 연산자
- `i & (1 << j)`  
i의 j번째 비트가 1인지 아닌지 검사   

```python
arr = [3, 6, 7, 1, 5, 4]
n = len(arr) # n : 원소의 개수
for i in range(1<<n): # 부분집합의 개수만큼 반복
    for j in range(n): # 원소의 수만큼 비트를 비교
        if i & (i<<j): # i의 j번 비트가 1인 경우
            print(arr[j], end=", ") # j번 원소 출력
    print()
print()
```

## 검색 (Search)
저장되어있는 자료 중에서 원하는 항목을 찾는 작업  
목적하는 탐색 키를 가진 항목을 찾는 것  
- 탐색 키(search key) : 자료를 구별하여 인식할 수 있는 키

>#### 검색의 종류
>- 순차 검색(sequential search)
>- 이진 검색(binary search)
>- 해쉬

### 순차 검색(Sequential Search)
일렬로 되어있는 자료를 순서대로 검색하는 방법  
- 배열이나 연결리스트 등 순차구조로 구현된 자료구조에서 원하는 항목을 찾을 때 유용함
- 알고리즘이 단순하여 구현이 쉽지만, 검색 대상의 수가 많은 경우 수행시간이 급격히 증가하여 비효율적임  

#### 정렬되어 있지 않은 경우
첫번째 원소부터 순서대로 검색대상과 키값이 같은 원소가 있는지 비교 검색  
키 값이 동일한 원소를 찾으면 그 원소의 `인덱스`를 반환    
마지막에 이를 때까지 검색 대상을 찾지 못하면 검색 실패  

- 찾고자하는 원소의 순서에 따라 비교 회수가 결정됨  
- 정렬되지 않은 자료에서 순차검색의 평균 비교 횟수
    - = (1/n) * (1 + 2 + 3 + ... + n) = (n+1) / 2
- 시간 복잡도: `O(n)`
```python
#pseudo code
def sequentialSearch(a, n, key):
    i <- 0
    while i<n and a[i]!=key:
        i <- i+1
    if i<n :
        return i
    else:
        return -1
```
#### 정렬되어 있는 경우
자료가 오름차순으로 정렬된 상태에서 검색을 실시한다고 가정  
순차적으로 검색하면서 키 값을 비교하여, 원소의 키 값이 검색 대상의 키 값보다 크면 찾는 원소가 없다는 뜻이므로 더이상 검색하지않고 종료  
- 정렬되어 있으므로, 검색 실패를 반환하는 경우 평균 비교 회수가 반으로 줄어듦  
- 시간 복잠도 : `O(n)`
```python
#pseudo code
def sequentialSearch_sorted(a, n, key):
    i <- 0
    while i<n and a[i]<key:
        i <- i+1
    if i<n and a[i] == key:
        return i
    else:
        return -1
```

### 이진 검색(Binary Search)
자료의 `가운데`에 있는 항목의 키 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속 진행하는 방법  
목적 키를 찾을 때까지 이진 검색을 순환적으로 반복 수행함으로써 검색 범위를 반으로 줄여가면서 보다 빠르게 검색을 수행함    
이진 검색을 하기 위해서는 자료가 `정렬된 상태`여야 함  
- 검색 범위의 시작점(start)와 종료점(end)을 이용하여 검색을 반복 수행  
- 이진 검색의 경우, 자료에 삽입이나 삭제가 발생하였을 때 배열의 상태를 항상 정렬 상태로 유지하는 추가 작업 필요  

```python
def binarySearch(a, N, key):
    start = 0
    end = N - 1
    while start <= end: # start가 end 왼쪽 혹은 같을 때까지만 반복(뒤집어지면 종료) 
        middle = (start + end) // 2
        if a[middle] == key: #검색 성공 
            return true
        elif a[middle] > key: 
            end = middle - 1
        elif a[middle] < key:
            start = middle + 1 

    return false #검색 실패
```
```python
#[ 재귀 버전 ]
def binarySearch2(a, low, hight, key) : 
    if low > high: # 검색 실패
        return False
    else:
        middle = (low + high) // 2
        if key == a[middle]: # 검색 성공
            return True
        elif key < a[middle]:
            return binarySearch2(a, low, middle-1, key)
        elif key > a[middle]:
            return binarySearch2(a, middle+1, high, key)
```

### 인덱스(Index)
database에서 유래한 용어로 테이블에 대한 동작 속도를 높여주는 자료 구조를 말함  
database분야가 아닌 곳에서는 Look up table 등의 용어를 사용하기도 한다  
- 배열을 사용한 인덱스  
대량의 데이터를 매번 정렬하면, 프로그램의 반응은 느려질 수 밖에 없음.  이런 대량 데이터의 성능저하 문제를 해결하기 위해 배열 인덱스를 사용할 수 있음    
- 원본데이터에 데이터가 삽입될 경우, 상대적으로 크기가 작은 인덱스 배열을 정렬하기 때문에 속도가 빠름  

### 선택 정렬(Selection Sort)
주어진 자료들 중에서 가장 작은 값의 원소부터 차례대로 선택하여 위치를 교환하는 방식  
- 주어진 list에서 최소값을 찾음(해당 인덱스도!)
- 그 값을 list의 맨 앞의 값과 교환 
- 맨 처음 위치를 제외한 나머지 list를 대상으로 위의 과정 반복  
- 시간 복잡도 : `O(n^2)`
```python
def selectionSort(arr, n):
    for i in range(n-1): #어차피 마지막에 남은 1개는 정렬해도 그자리니까 아예 for문에서 제외시킴 
        minIdx = i
        for j in range(i+1, n): # i랑 배열에서의 그 뒤 값들 비교 
            if arr[minIdx] > arr[j]:
                minIdx = j # arr[j]이 arr[minIdx]보다 작으면 minIdx를 j로 변경 
        arr[i], arr[minIdx] = arr[minIdx], arr[i] # 최소값을 구간 맨 앞으로!
    return arr
```
#### 셀렉션 알고리즘(Selection Algorithm)
자료로부터 k번째로 큰 혹은 작은 원소를 찾는 방법  
최소값, 최대값 혹은 중간값을 찾는 알고리즘을 의미하기도 함 

- k번째로 작은 원소를 찾는 알고리즘
    - 1번째부터 k번째까지 작은 원소들을 찾아 배열의 앞쪽으로 이동시키고, 배열의 k번째를 반환한다  
    - k가 비교적 작을 때 유용
- 시간 복잡도: `O(kn)`
```python
def select(arr, k):
    for i in range(0, k):
        minIdx = i
        for j in range(i+1, len(arr)):
            if arr[minIdx] > arr[j]:
                minIdx = j
        arr[i], arr[minIdx] = arr[minIdx], arr[i]
    return arr[k-1]
```
- 교환의 회수가 버블정렬, 삽입정렬보다 작음   

[참고]
```python
N = 3 # 행
M = 4 # 열

# N개의 원소를 갖는 0으로 초기화된 1차원 배열
arr1 = [0] * N
# 크기가 NxM이고 0으로 초기화된 2차원 배열
arr2 = [[0] * M for _ in range(N)]
```

