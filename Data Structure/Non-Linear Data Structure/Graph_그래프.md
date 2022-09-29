# 그래프
아이템(사물 혹은 추상적 개념)들과 이들 사이의 연결 관계를 표현  
**그래프** : 정점(Vertex)들의 집합과 이들을 연결하는 간선(Edge)들의 집합으로 구성된 자료구조   
선형 자료구조나 트리 자료구조로 표현하기 어려운 N:N 관계를 가지는 원소들을 표현하기에 용이  
- |V|: 정점의 개수
- |E|: 그래프에 포함된 간선의 개수
- |V|개의 정점을 가지는 그래프는 최대 `|V|(|V|-1)/2` 간선이 가능 (e.g. 5개의 정점을 가지는 그래프는 최대 10 = 5*4/2개의 간선을 가질 수 있다.)

### 그래프 유형
- 무향 그래프 Undirected Graph
- 유향 그래프 Directed Graph
- 가중치 그래프 Weighted Graph
- 사이클 없는 방향 그래프 DAG, Directed Acyclic Graph
- 완전 그래프 : 정점들에 대해 가능한 모든 간선들을 가진 그래프
- 부분 그래프 : 원래 그래프에서 일부의 정점이나 간선을 제외한 그래프  
- 인접 Adjacency
    - 두 개의 정점에 간선이 존재(연결됨)하면 서로 인접해 있다고 한다  
    - 완전 그래프에 속한 임의의 두 정점들은 모두 인접해 있다  

### 그래프 경로
경로 : 간선들을 순서대로 나열한 것 
- 간선들 (0, 2), (2, 4), (4, 6)
- 정점들 : 0, 2, 4, 6  

단순경로 : 경로 중 한 정점을 최대한 한번만 지나는 경로
- 0-2-4-6, 0-1-6

사이클Cycle : 시작한 정점에서 끝나는 경로 
- 1-3-5-1

### 그래프 표현 
간선의 정보를 저장하는 방식, 메모리나 성능을 고려해서 결정  
- 인접 행렬 Adjacent matrix
    - |V| X |V| 크기의 2차원 배열을 이용해서 간선 정보를 저장 
    - 배열의 배열(포인터 배열)
- 인접 리스트 Adjacent List
    - 각 정점마다 해당 정점으로 나가는 간선의 정보를 저장 
- 간선의 배열 
    - 간선(시작 정점, 끝 정점)을 배열에 연속적으로 저장  

#### 인접 행렬
  두 정점을 연결하는 간선의 유무를 행렬로 표현 
- |V| X |V| 정방 행렬
- 행 번호와 열 번호는 그래프의 정점에 대응
- 두 정점이 인접되어 있으면 1, 그렇지 않으면 0
- 무향 그래프
    - i번쨰 행의 합 = i번째 열의 합 = Vi의 차수
- 유향 그래프
    - 행 i의 합 = Vi의 진출 차수 
    - 열 i의 합 = Vi의 진입 차수 

#### 인접 리스트
각 정점에 대한 인접 정점들을 순차적으로 표현  
하나의 정점에 대한 인접 정점들을 각각 노드로 하는 연결 리스트로 저장  

```python
# 6 8  (마지막 정점번호 0부터 시작), E 간선 수
# 0 1 0 2 0 5 0 6 3 4 3 5 6 4 5 4
V, E = map(int, input().split())
# 인접 행렬
adjM = [[0]* (V+1) for _ in range(V+1)]
adjList = [[] for _ in range(V+1)]
for i in range(E):
    n1, n2 = arr[i*2], arr[i*2+1]
    adjM[n1][n2] = 1
    adjM[n2][n1] = 1   # 방향이 없는 경우에만 

    adjList[n1].append(n2)
    adjList[n2].append(n1)

print()
```

### 그래프 순회(탐색)
비선형구조인 그래프로 표현된 모든 자료(정점)를 빠짐없이 탐색하는 것  
- 깊이 우선 탐색(Depth First Search, DFS)
- 너비 우선 탐색(Breadth First Search, BFS)

#### 깊이 우선 탐색(Depth First Search, DFS)
- 시작 정점이 한 방향으로 `갈 수 있는 경로가 있는 곳까지` 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 방문하는 순회방법 
- 가장 마지막에 만났던 갈림길의 정점으로 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 후입선출 구조의 STACK 사용  

##### DFS 알고리즘 - 재귀
```python
DFS_Recursive(G, v):
    visited[v] = True               # v 방문했다고 설정
    
    for each all w in adjacency(G,v):
        if visited[w] == False:     # w 방문 안했으면
            DFS_Recursive(G, w)
```
##### DFS 알고리즘 - 반복 
1. 지나간 길을 stack에 저장하는 방법
2. 정점에 연결되어 있는 앞으로 갈 길을 stack에 저장해놓고 하나씩 pop해서 이동하는 방법
```python
s = [] # stack
visited = []
def DFS(v):
    push(s, v)   # 시작하는 정점, 
    while not isEmpty(s):
        v = s.pop(0)
        if not visited[v]:
            visited[v] = True
            for each w in adjacency(v): # v랑 인접인 아이들을 방문을 안했으면 stack에 push
                if not visited[w]:
                    push(s, w)
```
#### 너비 우선 탐색(Breadth First Search, BFS)
- 탐색 시작점의 인접한 정점들을 먼저 모두 차례로 방문한 후에, 방문했던 정점을 시작점으로 하여 다시 인접한 정점들을 차례로 방문하는 방식
- 인정잡 정점들에 대해 탐색을 한 후, 차례로 다시 너비우선탐색을 진행하여야 하므로, 선입선출 형태의 자료 구조인 queue를 활용

##### BFS 알고리즘 
```python
def BFS(G, v):   # graph G, 탐색 시작점 v
    # queue = deque() # deque import 및 삽입
    queue = [] # 큐 생성 
    queue.append(v)                # 시작점 v를 큐에 삽입
    visited[v] = True              # 점 v를 방문한 것으로 표시
    while queue:                   # 큐가 비어있지 않은 경우
        t = queue.pop(0)           # 큐의 첫번째 원소 소환 
        for i in range(1, N+1):    # t와 연결된 모든 선에 대해 
            if adj[t][i] == 1 and visited[i] == False: # t의 인접 정점이고 i가 방문되지 않은 곳이면, 
                queue.append(i)    # i를 큐에 넣고, 
                # visited[i] = True  # i를 방문한 것으로 표시
                visited[i] = visited[t] + 1

```

## 서로소 집합 Disjoint Set
서로소 또는 상호배타 집합들은 서로 중복 포함된 원소가 없는 집합들   
교집합이 없음  
집합에 속한 하나의 특정 멤버`[대표자(representative)]`를 통해 각 집합들을 구분함   
- 상호배타 집합을 표현하는 방법 : 연결 리스트, 트리
- 상호배타 집합 연산
    - Make-Set(x)
    - Find-Set(x)
    - Union(x, y)
#### 상호배타집합 표현 - 연결 리스트
같은 집합의 원소들은 하나의 연결리스트로 관리  
연결리스트의 맨 앞의 원소를 집합의 대표 원소로 삼음  
각 원소는 집합의 대표원소를 가리키는 링크를 가짐  
#### 상호배타집합 표현 - 트리
하나의 집합(a disjoint set)을 하나의 트리로 표현  
자식 노드가 부모 노드를 가리키며 루트 노드가 대표자가 됨  
루트 노드는 자기 자신을 가리킴

### 상호배타집합에 대한 연산
- Make_Set(x): 유일한 멤버x를 포함하는 새로운 집합을 생성하는 연산
```python
def Make_Set(x):
    p[x] = x
```
- Find_Set(x) : x를 포함하는 집합을 찾는 연산
```python
def Find_Set(x):
    while p[x] != x:
        x = p[x]
    return x    
```
- Union(x, y) : x와 y를 포함하는 두 집합을 통합하는 연산
```python
def Union(x, y):
    p[Find_Set(y)] = Find_Set(x)
```

#### 상호배타집합에 대한 연산의 효율을 높이는 방법 
1. Rank를 이용한 Union
    - 각 노드는 자신을 루트로 하는 subtree의 높이를 Rank라는 이름으로 저장 
    - 두 집합을 합칠 때 Rank가 낮은 집합을 Rank가 높은 집합에 붙임  
2. Path compression
    - Find-Set을 행하는 과정에서 만나는 모든 노드들이 직접 root를 가리키도록 포인터를 바꾸어줌

##### Rank를 이용한 Union
- Make_Set()
```python
def Make_Set(x):
    p[x] = x
    rank[x] = 0
```
- Find_Set(x) : x를 포함하는 집합을 찾는 연산
```python
def Find_Set(x):
    if x != p[x]:               # x가 root가 아닌 경우
        p[x] = Find_Set(p[x])
    return p[x]
```
- Union(x, y) : x와 y를 포함하는 두 집합을 통합하는 연산
```python
def Union(x, y):
    Link(Find_Set(x), Find_Set(y))

def Link(x, y): 
    if rank[x] > rank[y]:       # rank는 tree의 높이
        p[y] = x
    else:
        p[x] = y
        if rank[x] == rank[y]:
            rank[y] += 1
```

## MST Minimum Spanning Tree 최소 신장 트리
- 그래프에서 최소 비용 문제 
    1. 모든 정점을 연결하는 간선들의 가중치의 합이 최소가 되는 트리
    2. 두 정점 사이의 최소 비용의 경로 찾기 
- 신장 트리
    - n개의 정점으로 이루어진 `무방향 그래프`에서 n개의 정점과 n-1개의 간선으로 이루어진 트리
- 최소 신장 트리 Minimum Spanning Tree
    - `무방향 가중치 그래프`에서 신장 트리를 구성하는 간선들의 가중치의 합이 최소의 신장 트리

```python
V, E = map(int, input().split())
adjM = [[0] * (V+1) for _ in range(V+1)]
adjL = [[] for _ in range(V+1)]
for _ in range(E):
    u, v, w = map(int, input().split())
    # 인접 행렬로 저장
    adjM[u][v] = w
    adjM[v][u] = w  # 가중치가 있는 무방향 그래프
    # 인접 리스트로 저장 
    adjL[u].append((v, w))
    adjL[v].append((u, w))

```

### Prim Algorithm
- 하나의 정점에서 연결된 간선들 중에 하나씩 선택하면서 MST를 만들어가는 방식
    1. 임의 정점 하나를 선택해서 시작
    2. 선택한 정점과 인접하는 정점들 중의 최소 비용의 간선이 존재하는 정점을 선택
    3. 모든 정점이 선택될 때까지 1. 2. 과정을 반복 

- 서로소인 2개의 집합(2 disjoint sets) 정보를 유지
    - 트리 정점들(tree vertices) - MST를 만들기 위해 선택된 정점들
    - 비트리 정점들(nontree vertices) - 선택되지 않은 정점들 


```python
def prim1(r, V):
    mst = [0] * (V+1)  # MST 포함 여부 1 / 0
    key = [9999] * (V+1)  # 가중치를 최대값이상으로 초기화
    key[r] = 0    # 시작 정점의 key
    for _ in range(V):  # V+1 개 정점 중 V개 선택 
        u = 0         # mst에 포함되지 않은 정점
        minV = 10000  
        for i in range(V+1):
            if mst[i] == 0 and key[i] < minV: # 아직 mst가 아니면서 i번째의 키값이 minV보다 작으면 
                u = i
                minV = key[i] # minV를 최소값으로
        mst[u] = 1    # mst에 U 추가
        for v in range(V+1):
            if mst[v] == 0 and adjM[u][v] > 0: 
                key[v] = min(key[v], adjM[u][v])
    return sum(key)          # 가중치의 합

V, E = map(int,input().split())
visited = [i for i in range(V+1)]
adjM = [[0] * (V+1) for _ in range(V+1)]
for i in range(E):
    u, v, w = map(int, input().split())
    adjM[u][v] = w
    adjM[v][u] = w  
prim1(0, V)
```
```python
def prim2(r, V):
    mst = [0] * (V+1)   # mst 포함 여부
    mst[r] = 1          # 시작점 mst 포함
    s = 0               # 가중치의 합
    for _ in range(V): 
        u = 0
        minV = 10000
        for i in range(V+1):
            if mst[i] == 1:    # mst에 포함된 정점일 경우 인접 정점 확인
                for j in range(V+1): 
                    if adjM[i][j] > 0 and mst[j] == 0 and minV > adjM[i][j]:  # j는 i와 인접한 정점, j는 mst에 아직 포함 X, 인접한 정점 중에 가중치가 minimum인 경우 
                        u = j   # mst에 넣을 u로 지정
                        minV = adjM[i][j] # minimumV 지정
        s += minV
        mst[u] = 1
    return s
```

### Kruskal Algorithm
간선을 하나씩 선택해서 MST를 찾는 알고리즘  
1. 최초, 모든 간선을 가중치에 따라 오름차순으로 정렬
2. 가중치가 가장 낮은 간선부터 선택하면서 트리를 증가시킴
    - 사이클이 존재하면 다음으로 가중치가 낮은 간선 선택
3. n-1개의 간선이 선택될 때까지 2를 반복

#### 알고리즘
```python
V, E = map(int, input().split())
edge = []
for _ in range(E):
    u, v, w = map(int, input().split())
    edge.append([u, v, w])
edge.sort(key=lambda x:x[2])
rep = [i for i in range(V+1)]

def find_set(x):
    while rep[x] != x:
        x = rep[x]
    return x
def union(x, y):
    rep[find_set(y)] = find_set(x)   # y의 대표원소를 찾아서 x의 대표원소로 바꿈

count = 0   # 선택한 정점의 개수 
total = 0   # MST 가중치의 합 

for u, v, w in edge:
    if find_set(u) != find_set(v):
        union(u, v)
        count += 1
        total += w
    if count == V:
        break
print(total)
```