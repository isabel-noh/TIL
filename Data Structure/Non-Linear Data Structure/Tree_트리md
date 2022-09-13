# Tree 트리 
##### 개념
비선형 구조  
원소들 간에 1:n 관계를 가지는 자료구조  
원소들 간에 계층관계를 가지는 계층형 자료구조  
상위 원소에서 하위 원소로 내려가면서 확장되는 트리(나무)모양의 구조   

![트리구조](https://i0.wp.com/hanamon.kr/wp-content/uploads/2021/07/%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9-%E1%84%90%E1%85%B3%E1%84%85%E1%85%B5-%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%8B%E1%85%A5.png?resize=975%2C551&ssl=1)  

##### 정의 
- 한 개 이상의 노드로 이루어진 `유한 집합`
    - root : 노드 중 최상위 노드
    - 나머지 노드들은 n(>=0)개의 분리집합 T1, ... , TN으로 분리될 수 있다. 
- T1, ... , TN은 각각 하나의 트리가 되며 (재귀적 정의) 루트의 부 트리(subtree)라 함

##### 용어
- 노드 node : 트리의 원소
- 간선 edge : 노드를 연결하는 선. 부모 노드와 자식 노드를 연결  
- 루트 노드 root node : 트리의 시작 노드 (최상단 노드)  
- 형제 노드 sibling node : 같은 부모 노드의 자식 노드들
- 조상 노드 : 간선을 따라 루트 노드까지 이르는 경로에 있는 모든 노드들 (부모, 부모의 부모, 부모의 부모의 부모, ..., 루트 노드)
- 서브 트리 subtree : 부모 노드와 연결된 간선을 끊었을 때 생성되는 트리 
- 자손 노드 : 서브 트리에 있는 하위 레벨의 노드들
- 차수 degree 
    - 노드의 차수 : 노트에 연결된 자식 노드의 수(자손X 자식O)
    - 트리의 차수 : 트리에 있는 노드의 차수 중에서 가장 큰 값 
    - 단말 노드 leaf node : 차수가 0인 노드. 자식노드가 없는 노드
- 높이 level
    - 노드의 높이 : 루트에서 노드에 이르는 간선의 수. 노드의 레벨
    - 트리의 높이 : 트리에 있는 노드의 높이 중에서 가장 큰 값. 최대 레벨  
    > 레벨의 높이는 0부터 시작한다는 의견과 1부터 시작한다는 의견으로 나뉘어 상대적인 개념임

## 이진트리
모든 노드들이 2개의 서브트리를 갖는 특별한 형태의 트리  
각 노드가 자식 노드를 최대한 2개까지만 가질 수 있는 트리  
    - 왼쪽 자식 노드 left child node  
    - 오른쪽 자식 노드 right child node
##### 특성
-  레벨 i에서의 노드의 최대 개수는 `2^i`개 
- 높이가 h인 이진트리가 가질 수 있는 노드의 최소 개수는 (`h+1`)개가 되며, 최대 개수는 (`2^(h+1) - 1`)개가 된다.

#### 포화 이진 트리 Full Binary Tree
모든 레벨에 노드가 포화상태로 차 있는 이진 트리  
높이가 h일 때, 최대의 노드 개수인 (2^(h+1) - 1)의 노드를 가진 이진 트리  
- 높이가 3일 때, 2^(3+1) - 1 = 15개의 노드  

루트를 1번으로 하여 2^(h+1) - 1까지 정해진 위치에 대한 노드 번호를 가짐  

#### 완전 이진 트리 Complete Binary Tree
높이가 h이고 노드 수가 n개 일 때, (단, h+1 <= n < 2^(h+1) - 1),   
포화 이진 트리의 노드 번호 1부터 n까지 빈 자리가 없는 이진 트리  

#### 편향 이진 트리 Skewed Binary Tree
높이 h에 대한 최소 개수의 노드를 가지면서 한쪽 방향의 자식 노드만을 가진 이진 트리  
- 왼쪽 편향 이진 트리
- 오른쪽 편향 이진 트리

### 순회 traversal
트리의 각 노드를 중복되지 않게 전부 방문(visit)하는 것을 말함  
트리는 비선형구조이기 때문에 선형구조에서와 같이 선후연결 관계를 알 수 없음  
- 트리의 노드들을 체계적으로 방문하는 것  
- 순회 방법
    - 전위 순회 preorder traversal : VLR
        - 부모 노드 방문 후, 좌식노드를 좌, 우 순서로 방문
    - 중위 순회 inorder traversal : LVR 
        - 왼쪽 자식노드, 부모노드, 오른쪽 자식노드 순으로 방문
    - 후위 순회 postorder traversal : LRV
        - 자식노드를 좌우 순서로 방문한 뒤, 부모노드로 방문 

#### 전위 순회 preorder traversal
- 수행 방법 
    1. 현재 노드 n을 방문하여 처리 -> V
    2. 현재 노드 n의 왼쪽 서브트리로 이동 -> L
    3. 현재 노드 n의 오른쪽 서브트리로 이동 -> R
- 알고리즘  
```python
def preorder_traverse(T):                # 전위순회
    if T :                               # T is not None
        visit(T)                         # print(T.item)
        preorder_traverse(T.left)
        preorder_traverse(T.right)
```
#### 중위 순회 inorder traversal
- 수행 방법 
    1. 현재 노드 n의 왼쪽 서브트리로 이동 -> L
    2. 현재 노드 n을 방문하여 처리 -> V
    3. 현재 노드 n의 오른쪽 서브트리로 이동 -> R
- 알고리즘  
```python
def inorder_traverse(T):                # 중위순회
    if T :                               # T is not None
        inorder_traverse(T.left)
        visit(T)                         # print(T.item)
        inorder_traverse(T.right)
```
#### 후위 순회 postorder traversal
- 수행 방법 
    1. 현재 노드 n의 왼쪽 서브트리로 이동 -> L
    2. 현재 노드 n의 오른쪽 서브트리로 이동 -> R
    3. 현재 노드 n을 방문하여 처리 -> V
- 알고리즘  
```python
def postorder_traverse(T):                # 후위 순회
    if T :                               # T is not None
        postorder_traverse(T.left)
        postorder_traverse(T.right)
        visit(T)                         # print(T.item)
```