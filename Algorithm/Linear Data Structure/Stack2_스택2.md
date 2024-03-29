## 계산기
문자열로 된 계산식이 주어질 때, 스택을 이용하여 이 계산식의 값을 계산할 수 있음  
- 문자열 수식 계산의 일반적 방법
    - step1. 중위 표기법의 수식을 후위 표기법으로 변경(stack)  
    중위 표기법(infix notation): 연산자를 피연산자의 가운데 표기하는 방법   
    예) A + B
    - step2. 후위 표기법의 수식을 stack을 이용하여 계산
    후위 표기법(postfix notation): 연산자를 피연산자 뒤에 표기하는 방법  
    예) AB + 

### 중위 표기법의 수식을 후위 표기법으로 변경(stack)  
- 수식의 각 연산자에 대하여 우선순위에 따라 괄호를 사용하여 다시 표현
- 각 연산자를 그에 대응하는 오른쪽 괄호의 뒤로 이동시킴
- 괄호를 제거한다 
```
A*B-C/D
step1.((A * B) - (C / D))
step2. ((A B)* (C D)/)-
step3. AB * CD /-
```

- ISP : 스택 안에서의 우선순위
- ICP : 대조 대상과의 우선순위
- '(' : 여는 괄호는 무조건 스택에 push
- +, -, *, / : 우선순위 주의
- ')' : 닫는 괄호를 만나면 그 전 여는 괄호가 나올 때까지 pop

### 후위 표기법의 수식을 stack을 이용하여 계산
- 피연산자를 만나면 스택에 push
- 연산자를 만나면 필요한 만큼의 피연산자를 스택에서 pop하여 연산하고, 연산결과를 다시 스택에 push
- 수식이 끝나면 마지막으로 스택을 pop하여 출력

```python
str1 = '(6+5*(2-8)/2)'

stack = []
result = ''

def my_eval(word, stack):
    # word : 연산할 계산식(후위표기법)
    # stack : 결과
    # return stack
    for char in word:
        # 피연산자를 stack에 append
        if char not in '+-/*':
            stack.append(int(char))
        else: 
            x = stack.pop()
            y = stack.pop()

            if char == '+':
                stack.append(y + x)
            if char == '-':
                stack.append(y - x)
            if char == '*':
                stack.append(y * x)
            if char == '/':
                stack.append(y / x)
    return stack[-1]

for char in str1:
    # 연산자가 들어올 때
    if char in '*/+-()':
        if not stack:
            stack.append(char)
        
        elif char == '(':
            stack.append(char)
        elif char in '*/':
            while stack and stack[-1] in '*/':
                result += stack.pop()
            stack.append(char)
        elif char in '+-':
            while stack and stack[-1] != '(':
                result += stack.pop()
            stack.append(char)
        elif char == ')':
            while stack and stack[-1] != '(':
                result += stack.pop()
            stack.pop()
    # 피연산자가 들어올 때
    else:
        result += char
while stack: 
    result += stack.pop()
res = my_eval(result, [])
print(f'result: {result}')
print(f'res: {res}')
```


## 백 트랙킹(Back Tracking)
해를 찾는 도중에 막히면 (해가 아닌 경우) 되돌아가서 다시 해를 찾는 기법  
**최적화(optimization) 문제**와 **결정(decision) 문제**를 해결할 수 있는 기법  
- 결정 문제: 문제의 조건을 만족하는 해가 존재하는지 여부를 yes or no로 답하는 문제  
    - 미로찾기  
    - n-Queen 문제
    - Map coloring
    - 부분집합의 합 문제 등

> **백트랙킹과 깊이우선탐색의 차이**
> - 어떤 노드에서 출발하는 경로가 해결책으로 이어질 것 같지 않으면 더이상 해당 경로를 따라가지 않음으로써 시도 횟수를 줄임(가지치기, Pruning) 
> - 깊이우선탐색은 모든 경로를 추적하는 데 비해 백트랙킹은 불필요한 경로를 조기에 차단할 수 있음
> - 깊이우선탐색을 하기에는 너무 경우의 수가 많음.
> - 백트랙킹 알고리즘을 적용하면 일반적으로 경우의 수가 줄어들지만, 역시 최악의 경우 여전히 지수함수 시간(Exponential Time)을 요하므로 처리 불가능할 수 있음

### 백 트랙킹 기법
- 어떤 노드의 유망성을 점검한 후 유망하지 않다고 결정되면 부모 노드로 돌아가 다음 자식 노드로 감  
- 절차
    - 상태 공간 트리의 깊이 우선 검색을 실시
    - 각 노드가 유망한지 점검
    - 만약 해당 노드가 유망하지 않다면, 부모 노드로 돌아가 그 다음 자식 노드로 가면서 검색을 계속함  

- 일반 백트랙킹 알고리즘
```python
def checknode(v):
    if promising(v):
        if there is a solution at v:
            write the solution
        else:
            for u in each child of v:
                checknode(u)
```

- 부분집합 구하기
어떤 집합의 공집합과 자기자신을 포함한 모든 부분집합을 powerset이라고 하며, 구하고자 하는 어떤 집합의 원소 개수가 n일 경우, 부분집합의 개수는 2^n이다.
    - n개의 원소가 들어있는 집합의 2^n개의 부분집합을 만들 때에는, true / false값을 가지는 항목들로 구성된 n개의 배열들을 만드는 방법을 이용 
    - 배열의 i번째항목은 i번째원소가 부분집합의 값인지 아닌지를 확인하는 값  
    
```python
# 부분집합 구하기
# 집합의 원소에 대해 각 부분집합에서의 포함 여부를 트리로 표현

def f(i, N):
    global answer
    global cnt
    cnt += 1
    if i == N:
        sum = 0
        # print(bit)
        for i in range(N):
            if bit[i]:
                # print(arr[i], end=' ')
                sum += arr[i]
        # print()
        if sum == 10:
            answer += 1
            for i in range(N):
                if bit[i]:
                    print(arr[i], end=' ')
            print()
    else:
        # bit[i] = 1  # A[i]가 부분집합에 포함
        # f(i+1, N)
        # bit[i] = 0
        # f(i+1, N)
        candidate = [0, 1]
        for x in candidate:
            bit[i] = x
            f(i+1, N)

arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
bit = [0] * 10
answer = 0
cnt = 0
f(0, 10)
print(answer, cnt)
```

부분집합 > 백트랙킹
```python
# i원소의 포함여부를 결정하면 i까지의 부분집합의 합s를 결정할 수 있음
# s가 원하는 값보다 크면 남은 원소를 고려할 필요가 없음 

def f(i, N, s, t):
    global answer
    global cnt
    cnt += 1
    if i == N:   # 모든 원소가 고려된 경우
        if s== t:  # 부분집합의 합이 t이면
            answer += 1
        return   
    elif s > t:   # 가지치기 ( 남은 원소를 고려할 필요가 없는 경우 )
        return 
    else:         # 남은 원소가 있고 s < t인 경우
        f(i+1, N, s+arr[i], t)   # arr[i]가 포함된 경우
        f(i+1, N, s, t)          # arr[i]가 포함되지 않은 경우
    return 

arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
bit = [0] * 10
answer = 0
cnt = 0
f(0, 10, 0, 10)
print(answer, cnt)
```

## 순열
- A[1, 2, 3]의 모든 원소를 사용한 순열
  - 123, 132, 213, 312, 321
```python
def f(1, N):
    if i == N :       # 순열 완성
        print(p)
    else:
        for j in range(i, N):       # P[i]에 들어갈 숫자 결정
            P[i], P[j] = P[j], P[i]
            f(i+1, N)
            P[i], P[j] = P[j], P[i]  # 원상복귀

P = [1, 2, 3]
f(0, 3)
```