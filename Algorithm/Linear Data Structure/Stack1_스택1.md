# Stack
물건을 쌓아올리듯 자료를 쌓아 올린 형태의 자료구조  
스택에 자료를 삽입하거나 꺼낼 수 있음  
마지막에 넣은 자료를 가장 먼저 꺼냄`(후입선출, LIFO, Last-in First-out)` 
- stack은 선형 자료구조임 
    - 선형구조 : 자료 간의 관계가 1대1 관계
    - 비선형구조 : 자료 간의 관계가 1대N 관계(예. 트리)
- 자료를 선형으로 저장할 저장소가 필요
- top : 스택에서 마지막에 삽인된 원소의 위치
- 삽입 : 저장소에 자료 저장(push) 
- 삭제 : 저장소에서 자료 삭제(pop), 삽입한 자료의 역순으로 자료를 꺼냄  
- isEmpty : stack의 공간이 공백인지 아닌지 확인 
- peek : stack의 top에 있는 원소(item)을 반환 

#### push algorithm
```python
def push(item):
    s.append(item)
```
```python
def push(item, size):
    global top
    top += 1
    if top == size:
        print('overflow')
    else:
        stack[top] = item

size = 10
stack = [0] * size   # stack 생성
top = -1             # top 이 없는 상황

push(10, size)
top += 1             # push(20)
stack[top] = 20 
```
#### pop algorithm
```python
def pop():
    if len(s) == 0: # stack의 길이가 0인 경우
        # underflow 처리
        return
    else:
        return s.pop(-1) # 마지막에 들어간 원소를 꺼냄
```
```python
def pop():
    global top
    if top == -1:
        print('underflow')
        return 0
    else:
        top -= 1
        return stack[top+1]

print(pop())

if top > -1:          # pop()
    top -= 1
    print(stack[top])
```

#### 스택 구현시 고려사항 
- 리스트를 사용하여 스택을 구현하는 경우 
    - 구현이 용이함
    - but, 리스트의 크기를 변경하는 작업은 내부적으로 큰 overhead 발생 작업으로 소요시간이 크게 발생할 수 있음 
- 해결 방법
    - 리스트의 크기를 변동하지 않도록 배열처럼 크기를 지정해 놓고 사용
    - 동적 연결 리스트를 이용하여 저장소를 동적으로 할당하여 스택을 구현

### function call
- 프로그램에서의 함수 호출과 복귀에 따른 수행 순서를 관리
    - 후입선출 구조이므로, 후입선출 구조의 스택을 이용하여 수행순서 관리
    - 함수 호출이 발생하면 호출한 함수 수행에 필요한 지역변수, 매개변수 및 수행 후 복귀할 주소등의 정보를 스택 프레임에 저장하여 시스템 스택에 삽입
    - 함수 실행이 끝나면 시스템 스택의 top원소(스택 프레임)를 삭제(pop)하면서 프레임에 저장되어 있던 복귀 주소를 확인하고 복귀
    - 함수 호출과 복귀에 따라 이 과정을 반복하여 전체 프로그램 수행이 종료되면 시스템 스택은 공백 스택이 됨

### 재귀호출
자기 자신을 호출하여 순환 수행하는 것  
[재귀호출의 예] factorial  
n에 대한 factorial: 1부터 n까지 모든 자연수를 곱하여 구하는 연산  
```python
n! = n * (n-1)!
(n-1)! = (n-1) * (n-2)!
(n-2)! = (n-2) * (n-3)!
...
2! = 2 * 1!
1! = 1
```
[재귀호출의 예] 피보나치   
0과 1로 시작하고 이전 두 수의 합을 다음 항으로 하는 수열  
```python
# 0, 1, 1, 2, 3, 5, 8, 13, 21, ...
# F_0 = 0, F_1 = 1
# F_I = F_I-1 + F_I-2 for i >= 2

def fibo(n):
    if n < 2:
        return n
    else:
        return fibo(n-1) + fibo(n-2)
```


### Memoization
컴퓨터 프로그램을 실행할 때에 이전에 계산한 값을 메모리에 저장하여 매번 다시 계산하지 않도록 하여 전체적인 실행속도를 빠르게 하는 기술  
DP(동적계획법)의 핵심기술  

> [참고]
피보나치를 재귀함수로 구현할 경우, f(n)함수가 너무 많이 호출된다. (마지막에 가면 f(1)함수가 굉장히 여러번 호출됨) 이런 상황을 막기 위해 f(n)값을 저장하여 함수를 호출할 필요없이 값을 가져다가 쓰게함  
실행시간을 O(n)으로 줄일 수 있음
```python
# memo를 위한 리스트 생성
# memo[0]을 0으로, memo[1]을 1로 초기화

# way1
def fibo1(n):
    if n >= 2 and len(memo) <= n:
        memo.append(fibo1(n-1) + fibo1(n-2))
    return memo[n]
    
memo = [0, 1]
for i in range(101):
    print(i, fibo(i))
```
```python
# way2
def fibo(n):
    if memo[n] == -1:
        memo[n] = fibo(n-1) + fibo(n-2)
    return memo[n]

memo = [-1] * 101
memo = [0, 1]
for i in range(101):
    print(i, fibo(i))
```

### 동적 계획법(DP)
먼저 입력 크기가 작은 부분 문제들을 해결하고 그 해들을 이용하여 큰 크기의 부분 문제들을 해결  
```python
# 피보나치 수 DP 적용 알고리즘
def fibo_dp(n):
    table = [0, 1]

    for i in range(2, n+1):
        # table.append(table[i-1]+table[i-2])
        table[i] = table[i-1] + table[i-2]

    return table[n] 

table = [0] * 101
fibo_dp(100)
print(table[20])
``` 
- DP 구현 방식
    - recursive 방식(재귀): fib1()
    - iterative 방식(반복구조): fib2()
