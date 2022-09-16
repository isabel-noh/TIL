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
: 모든 노드들이 2개의 서브트리를 갖는 특별한 형태의 트리  
: 각 노드가 자식 노드를 최대한 2개까지만 가질 수 있는 트리  
    - 왼쪽 자식 노드 left child node  
    - 오른쪽 자식 노드 right child node
##### 특성
-  레벨 i에서의 노드의 최대 개수는 `2^i`개 
- 높이가 h인 이진트리가 가질 수 있는 노드의 최소 개수는 (`h+1`)개가 되며, 최대 개수는 (`2^(h+1) - 1`)개가 된다.

#### 포화 이진 트리 Full Binary Tree
: 모든 레벨에 노드가 포화상태로 차 있는 이진 트리  
: 높이가 h일 때, 최대의 노드 개수인 (2^(h+1) - 1)의 노드를 가진 이진 트리  
> 높이가 3일 때, 2^(3+1) - 1 = 15개의 노드  

: 루트를 1번으로 하여 2^(h+1) - 1까지 정해진 위치에 대한 노드 번호를 가짐  

#### 완전 이진 트리 Complete Binary Tree
: 높이가 h이고 노드 수가 n개 일 때, (단, h+1 <= n < 2^(h+1) - 1),   
: 포화 이진 트리의 노드 번호 1부터 n까지 빈 자리가 없는 이진 트리  

#### 편향 이진 트리 Skewed Binary Tree
: 높이 h에 대한 최소 개수의 노드를 가지면서 한쪽 방향의 자식 노드만을 가진 이진 트리    
    - 왼쪽 편향 이진 트리  
    - 오른쪽 편향 이진 트리

### 순회 traversal
: 트리의 각 노드를 중복되지 않게 전부 방문(visit)하는 것을 말함  
: 트리는 비선형구조이기 때문에 선형구조에서와 같이 선후연결 관계를 알 수 없음  
: 트리의 노드들을 체계적으로 방문하는 것  
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

### 이진트리의 표현  
- `배열`을 이용한 이진트리의 표현 (`포화이진트리, 완전이진트리`)
    - 이진 트리에 각 노드 번호를 다음과 같이 부여
    - 루트의 번호 = 1
    - 레벨 n에 있는 노드에 대하여 왼쪽부터 오른쪽으로 2^n 부터 2^(n+1) - 1 까지 번호를 차례로 부여  
        > tree = [0, A, B, C, D, E, F, G, H, I, J, K, L, M]  
        > - 0번째는 채우지 않음  
    - 노드 번호의 성질
        - 노드번호가 i인 노드의 부모노드 번호: i // 2
        - 노드번호가 i인 노드의 왼쪽 자식 노드 번호: 2 * i
        - 노드번호가 i인 노드의 오른쪽 자식 노드 번호: 2 * i + 1
        - 레벨 n의 노드번호 시작 번호: 2^n  
        - 노드 번호를 배열의 인덱스로 사용
        - 높이가 h인 이진트리를 위한 배열의 크기는?
            - 레벨 i의 최대 노드 수 : 2^i
            - 1 + 2 + 4 + 8 + ... + 2^i = 2^(h+1) - 1    

    ![배열 이진트리](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAoHCBQUEhgSFBQYGBgYGBgYGBkYGBsaGRkbGBgaGRobGBgbIS0kGx0qHxgaJTkmLC4xNDQ5GyM6PzozPi0zNDEBCwsLEA8QGhISHTwhISEzMzMzMzM0MzMzMTMxMzQxMTMxMTMzMzMzMzEzMzMxMzEzMzM+MzM1MzMxMzMzMTMzPv/AABEIALABHgMBIgACEQEDEQH/xAAbAAEAAgMBAQAAAAAAAAAAAAAABAUBAgMGB//EAEAQAAIBAgQCCAIGCQMFAQAAAAECAAMRBBIhMUFRBRMiMmFxgZEUUgZCYnKhsRcjM1OCosHR0pKy8AdUY5PiNP/EABgBAQEBAQEAAAAAAAAAAAAAAAABAwIE/8QAIBEBAQEBAQACAwADAAAAAAAAAAECEhEDURMhMUFhsf/aAAwDAQACEQMRAD8A+zREQEREBERAREQEREBERA1JtMgzhjKKvTdGUMGUgqRcG42I4zn0WhWhTVhYimgIO4IUAgwJkREBERAREQEREBERARMRAzExEDMREBExEDMTEzAREQEREBERAREQEREBERAREQI+JxCouZj4AAXJPIKNSfASL8TXbVKKgf8AkqZGP8KK9vUg+EzgxnqPUP1WamngFsGPmXB9FWa4vpMJWp0cpObvPewp5jlp5hxztdR4iBsMcym1amaY+cEPT9W0K+bKBLCasLix1B3kLo45WejwQrl5hGFwp8jmA8AIFhERAREQEREDE819IPpbTwlUUnpuxKhrrltYki2p8J6Uz5h9PKqJ0jSeouZFRCy/MA7XHjNfhzNa8rP5NXOfYt/0kUP3NX+T/KP0kUP3NX+T/KeVxmIp2qI5/WLhnRndBTZ3NZGRQm4ZUuOe/KTujzTd3enTBRkCoFoWKsFQMCypdyWBO5no/Djz3xh+TX2u/wBJFD9zV/k/ymf0j0P3NX+T/KeTw9CmalWsaT1VepVVERLKqsxGfMwtmAJyrbcakSmx2G6uoU7VtCCy5GIPNbm2txvwnefg+O3zxzfl3P8AL6S3/UGiEWp1VSzO6W7F7oqMfrfbHtOX6SKH7mr/ACf5T55W/wDypb97X/2UZ67AJSOKqBFpFMyZMholcnxFAarTXPfUi7HwtOdfDiT+LPl1f8rb9I9D9xV/k/yj9I9D9zV/k/ynk8SMOKL/ALO+StfbrRW639Xl45Mltuz3r62krHrSWpiRlp5uvTKGaghCdWc1uuVhlzW0Gu0n4sfVX8mvt6L9I9D9zV/k/wApc/Rz6S08aXCI65ACc2XXNfaxPKfLelUUUcNlFr06l9QxJFdwTmAFxpp4Wnq/+lner+Sfm0nyfDiYupFx8mrqSvo8RE8b1EREBERAREQEREBERATEzECtoHq6jI2iuxdCdrsLun3swLeIY8jOWL6Ep1GdmL5nyaq5XLk1SyjsnK12GYHUnykzGNTyWqWyngeJ3AUbluVteUrRg651p1qlJPqq4WoT/qBYDwLE+W0qermpUCqWYgAC5J0AHjInRyE56rAjrCCqncKoAW/idW8M1uEjYWipcCqzvUGoFQjLpxRVCo1ueXML62luJBmIiFIiICIiBrPGfS36OJia4d6xTsBcoTNcXOt7jnPaSi6a/aD7o/MzT4rZr9M/kkuf28viPo2tQsXxeYt3m+Gphj45x2r+N5wofQ+mjq6YtgykFT1QuCNiLtL6UvWE5Q9RlV69dWOcronWBFDfVAyg2Hy631np61J57/xhzn6Rz9CqO/xTf+r/AOoH0Ko/903/AKv/AKkzoau7kF2JzYeg5v8AMxqBmA4XyjbTSW0s1r7LnP0pG+h9PqlT4lrB3a/V7llQWtm+wPeML9FVpnNTxjqTYEikODK43PzKp9JfnuD7zfks5yS6+znP08830LpEknFMSbk/que/1p0r/RFKjl3xbMzG7E0tztwaXsS9a+05n0oX+iKMqqcWxCAhB1WwZixHe5kn1nofod0GmGaoUqmpnC3uuW1ifE33mkteg928h/WZ/Jdc2eu8ZnUXURE8r0kREBERATlVqBVLMQAASSdAANSSeAtOs412IViq5iASFuBmNtBc6C50uYGmGxSVAWRgwBsbHY2BseRsQfUSTKzohHCMaiMrs2Z82SxOUDshGYBAAFAJv2dd7mzgImJEq4oA5VBZ/lXhyLHZR5+l4EpmtIRxTPpSAI+du4Pujd/Sw8YGEZ9apDckHcHnfVz56eAk4CVEWhhApzElm+Ztx4KNlHlJVpmJFca1FXFmFx+R5g8D4iRg70+9d0+YC7L94DvDxGvMcZPiBzp1AwDAgg7Eag+U6SDUwxBL0yFY6kHusftAbH7Q9bzehigTlIKtvlPLmp2ZfHxF7QiXINTHBXVCj2YgB7DLma5C3vcnTcAjmQZNlXisAXrU6hyWpkMpyHrBowZQ17ZTccNgfMFWgmZgTMDEqek8NncG4GlvxMtpAxve9J1i/tzr+Kz4E/MPYzinQ6KGAIszFyDmYZibkgE2GuunOWMp6mJqfD1qgqWZKlXLdVIVabsoUCw3C7m51PhNrqs+Ykr0WA5cMMzBVJ7Wy3sANgO0duZnT4E/MPYxSrN8Q9Mm6ilScCw0LtUU6gX2Rd78ZLjqnMRjgzlAzDvNwPJf7TX4E/MPYyb9UeZ/ITWJqnkRPgT8w9jHwJ+YexmnTWM6qkWDKrMyojNbKGchQxubWUHMfBZv0VixVpLUurHVWKm6lkJRip4rmBI8CI6pzD4E/MPYyf0Vh8hbUG9pzkvA7n0nO9Xx1mT1NiImLQiIgIiICIiBi8g4jpWil81RbruoOZh/CtzfwmtX9a7U7kIlg9jYuxF8lxqFAIJtvcDa4OzYqhSPV3VbBTlC2CqxIBNhZRcHflA40MT8RfI4VBuEYFzf5iO56XPiJPoUVQZVAA5D+vM+M5YrCK9iRZh3WGjKfst/TY8Zrga7NmV+8jZWtsdAysBwBUj1uOEqJsREikREBERAwZV4ioavZpoGAPfYlVBGl0KjMxHMWH2p16WJyBQSM7olxuAzANY8DlvrJLWRDYABVNgNBYDQDltAg0qeLRRepRqEcCj0yfNw76/w6+Ek0MXmJVlKuNSpIOnNSNGH5cbSLgcdUY086KBUTMpVibGynKQQODbjlOvTHZp9aO9SIqDyHeHqpYesIsBMzAmYViVuOqqGsTY25GWUoumv2g+6PzM7+Oe1xu+Rt8RT+b8D/aR6SUlV0zZldnYqwuO2SzAabEkmxvvIkrBXc03c1GW1WogyohayuyIiAjUkgb3J120tvcRn1XoF6sVGqZzmZVQ6GwVCxAAtzdj6zt8RT+b8D/aeewlWoahSoRcUqTkAaB2NQOFO+W6Dfxk6OYnVWprplHa4ngeQ8PGa/EU/m/A/2kA9wfeb/ak5xMQuli1SmSGJBKklTlNwSCDbTTQkesLUpi5BAzHM1lOpsBc6amwAv4Sh6TquoQJmuzhTkCFrZWJy9Z2fqjfxm/R1V3p3e+YO662zWVyBmy9nNYDbTlHM9Xqr34hPm/A/2kzo+qrFspvtwMoJa9B7t5D+s5+TMkq417V1ERPO2IiICIiAmDMzBgQMCbVKynfOHHirooB8rqw/hlX0v0a9SpUKq3bpU0VhVKIGVqhPWIGs62caWa4uJcYnDZiGDZXXuta/mrD6yniNPCx1kKt0jVp3DUQ+UZmZHFgL2zMHtl4m1zYAy/1FuDIGE7VerUHdslPzKZ2Yj1qBfNDMHr30IFJeJDZ38hYZV8+15cRMoUgqhVFgOH53PE31vxkV2iIgIiICIiBEx9AuhVSAwKspOwZGDLfwuLHwM1oYhaikbMNGQ6MpPAj8jsd5NkXFYKnUsXXUbMCVZfuupDL6GBGwfRoplSajvkXImfJZF0vYKq3PZGpudPOMW4qnqV1AZTUI1AVTfJfizEAW4Akm2l4+D6PVwXZ6rIWOQNVqWKjQEjN2gbE68CJbUqSooVVCqNgoAA8gJUdBMxEisSn6Vw7M4It3QNT4mXEgY3vek6xfK51/FT8E32feRB0CuzWcZ3dcxHYZ75spABHebe/eIlzKs42p1T1LoMlSootTqVCER2Qdim2aoxIG1rX20m11WfMKfRJVy4IuVRLX0CpmIA0vux3J3nb4Jua+816Pxz1HswUA0KNUZdbGp1gZc17MBk0IA3lhHVTmIhwbZQLr3m4+Cj+k0+CbmvvLD6o8z+QmsTVXmK2t0ZnADhWANxc7EcR4zNHo7IuVQqjXQHmbk+8kY6s6hFTLndwilrlR2WckgEE9lDpca2nXDh8v6wqWudUBAI4HKSSD4XMdU5iL8E3NfeWPRGHKlr21A2M0kvA7n0nO9Wx1nM9TYiJi0IiICIiAmDMzhiKwRbnXWwA3JOwHjA54msVsqi7tsOGm7N9kf2HGbUcOFXKdb3LE7sTuT/zwmuGokXdtWbfkBwUeAv66njJcqIXR7EKabboct+a2uh/02B8QZNkDFdh0qcDam/kx7BPkxt/GZOikZiIkUiIgIiICQukGOTKujOQgPLN3iPJQx9JMkFO3WZuFMZR95rFj6DKL/eHOWJUukoVQoFgAAByA0E6TEzIpERAxK/HOA2rAacTaWEoumv2g+6PzM7+Oe1xu+R06xfnX3kKnhKYVlNTQ1HcFXZGXOzMRmVtdWP8AzWR5Wt0g4pu1lZw9VUQXFxTZlu5udOzckAbgAX334jOaXuHw9NKhdXUDq6dNVGyrTLka8e+fYSV1qfOvvPOYHGNUazBbGjSqC196mcEbnTsXHnJ0cQ6W5qLlHaXc8fATXrU+dfeVx7g+83+1JziYLpPxVOnUXK7C1wwIcqQQbgqwIIP9zNqC00XKHG5PacsbnxYkykxdVwyIhUFywJZSwAVS2wZeXOdMJVZl7QAYMynLexyki4vsDa9vxMnEOl31qfOvvJmAcEmxB22M89LXoPdvIf1k3nzLrGvauoiJ52pK09JD4lcMFJJR3LfVBQ07r4m1RT6+1lKqh0JTSstZC4KrVXK1R3U9cyOxs7GxunDmYFpMxMEwNKlQKCzGwAuSdhI2Hplm6xhY2sin6oPE/aPHltzvqh61g31FN0+2R9b7o4e/KTgJUJmIkVxr0gylDswIPrynHAVCUs3eUlW8SvH1Fj6yZID9isG+q/ZbwYXKk+Yut/BRLEqfMXgGVHTGLq0yGUN1ao71HCo2XKUI0ZgT2c50B7vleKt5maibQERECPiqwRGe17DQczsAPEmw9ZjBUciBSbtux5sxJY+5M44g56qJwT9Y3uQgPqGb+CZ6Rxq0UDsVF2VVzMFBJPEnYAXPkDKidE5owIBBuCLgjYg8ROkikREDEpulaDM4IF+yOI5mXMgY3vek6xf251PYp/hX5fiP7yAOgAwZalNHBeoy5lW6io2ZgCSePEW2HK8v5Uv0hVIuiX/W1U7KM+VaZYXYBxqSm9xuBYmbXVZ8ueG6Ham5ZR2ciU1XTsrTzW1vqe2eWw85K+Ef5fxH95vg8YXqFLqy9VSqKygi/WFxsSdOxcfe9TNlm6coRwr5ALfWbiOS+PhNPhH+X8R/eWR7o8z+Qmsk1TmKnEdGM+UkMCpJUq9iLgg7HlNsP0cyLlVTa5OrXJJNySSbkkkyR0pi2pqhUau4TuPUtdWNwidpu7w534TvhnLICxuTr3Gp+V0cllPnHVOYifCP8v4j+8suh6LKWzC1wP6zWS8DufSc71bFzn9psRExakRIuOxHV02cC5A0HMnRR6kiBricYiEKbliLhUUsxHOyjQeJ0kLEYqo9lOGrKh75vSJI+XKrk2PG1zwtrJ2Ew/Vqbm7HtO1tWa2pP9BwAAmuCxy1QGVWCsoYMy2BBta3oZUb4TEo47B20KkFWXkGQgFfUSVK7pJSqmsg7dNSw+0q6sh5gi9uRsZNpuGAYaggEHwIuJFdIiIGJVY7FK4anTV6jc0UEKw453KpmBG2a+m07Y5iaiUQSA4ZmI+RMoYA8CS6jyvax1m9fEJRCLlPaYIiot9QrNYAaABVb2gcKXSLAA1aNSloLkhXW/HWmzWHiQJ2xGFpVgpYBltoQxsytYkHKbOpsLqbg6SRRqZlDWZfBhY721Hp+MhkdVWULolUsCOAqBS+Ycsyq9/EA7k3CyiIgJAfpKmCVBZyNCEVnsRuCVBAPgTMYti7iiCQCpZyNDlBsFB4Zid+SnncdKtanRVQbKuiqqqTc8FVVBJNhsBwgQsDj0GZ6gemzuT+sRkAA7KDORl7oGl9yZNxuF6zKQ7KyNmVlykglWQ6MCNmPCb0K61VzKQVN+HoQQdiDcEGRqB6uqKQ7jKWQfKUIDKPCzAgcLNwtKJeFoBKaU1vZFVRfeyiwv7TvESBERAxIGM73DbmJPlF01+0H3R+Znfxz2uN3yO3qPcSDT6PsrKapANR3Uo2RhnZmKscxD2LHgOHEXkaVzdJWQswGtV6aABm0RmDFgAToqM2g5ec2uP9s+l7hsEtNy6lQvV06aKLdlaecjtE6988thJdxzHuJ5+jic1VkFioRHVgdw5qD17m/jJMcHS5PdGo3PEchNbjmPcSsP7Mfeb8lnOJj/Z0scThlqBQWtlYOpVgCCARf2Yj1nSkmUWz5vFmBO9+Fuc8/wBIYo01UqLlnCd1mtdWN8qanu8Oc7YdyUBO55Ky/wAr9oac44/f9Ol5ccx7iS8DufTjPOy16D3byH9ZzvPmXWNe1dRETBqSH0lQNSkyL3rArfbMpDLf1AkyIEajWFRMy31B0OhB2KkcCDoR4SB0JgWooENKklkRS1NiS5UWuylFtxO53kqvgrsXpsUc7kWKtbbMh0PnofGczSxJ062kBzFJ7+gNSwPvA36TqEU2Ve+4KIPtMLX8h3j4AyVRpBVVBsoCjyAsJww2DCdoszsdC7WvbkAAAo8ABJkBERArsb2KtOse6A9Nj8ocoQT4XpgfxTPSOAFY0wwUqlTOysLgjq6iWtzu4PpJroDoQCDoQdj5yAcFUT9lUyj5HUuo+6QysPK5HhAnU6YVQqgAAWAGgA5CQa5z16ajakS7HgCyMiL5kOx9BzEfDV20esqj/wASZWPhmZmsPIX8ZKw9BUXKosNzuSSdySdSSeJ1hEiIiFVtXsYhXPddervwDA5kB8wW15gDiJnpKi7FGQAlGJIuAbMrJdSQQGGa+otoZNq0wylWFwdCJCWjWTRHV14CoDmHhnXcea38TA6dHq4pgVTmftE7HckgXAANgQL2F7X4zm4z4hANqSsWP23ACr/pzE+a84NLENozog49WCzejPoP9J9JJw9BUXKo033JJJ3JJ1JPMwO8zEQEREDEpOlqTM4IUnsjYeJl3IGN73pO/jvlcbnsUvwz/I3tINPohwCCXBzvUQoCjLnLEqTchu8dbctL6z0EgHpB+reoEWyPUU5nK9mmSrNoh4qdPLXhNrtxyhYbop6dQsFOXIlNVynsrTLkXJJv3/w4yV8M/wAje074bFl3NNkyMKdOoe1e2cuMp03BQj2kuJunKCcO+UDKe83DwWc/hn+RvaWh7o8z+QmsTdOYqquBZspKN2GzDTjYj8mM3+Gf5G9pLxeJ6sLZSzOwRVva5IJ1J2AVST5aX2m+HdmW7rlNyLBgw04qw3B8h5R3TlB+Gf5G9pZ9DUmUtmBGg39ZiS8Dx9JzvVsXOZ6mxETBqREQEREBERAREQEREBERAREQEREBERAREQEREDEg4tSW0HCT5iWXxLPVVkPI+0r6HRz5GR9FNZ6gy3OZWqF8rAgZdSARc3A8SJ6WJe05igp4VxXeqQLNTpoAL37DVGJItp37eklZDyPtLWJfyHMVhU5Rodzw8BNch5H2lrEnZzFFjMGaigdpSrBlIF7GxU3BFiCrMpHiYwGB6pMij6zMbKFF3YsbKoAA12l7EdnKqyHkfaSsEDrccpLiLv2Ez4zEROXT/9k=)

### 이진트리의 저장 
- 부모 번호를 인덱스로 자식 번호를 저장
> 4 <- 간선의 개수 N  
> 1 2 1 3 3 4 3 5 <- 부모 자식 순  
> e.g.   
> p > 0, 1, 2, 3, 4, 5   
> c1 = [0, 2, 0, 4, 0, 0]   
> c2 = [0, 3, 0, 5, 0, 0]
```python
for i : 1 -> N
    read p, c  # p: parent c: child
    if(c1[p] == 0): # c1이 비어있으면 c1에 child 넣기
        c1[p] = c
    else:           # c1이 비어있지 않으면 c2에 child 넣기
        c2[p] = c
```
- 자식 번호를 인덱스로 부모 번호를 저장
> c > 0, 1, 2, 3, 4, 5   
> parent = [0, 0, 1, 1, 3, 3]
```python
for i : 1 -> N
    read p, c # p: parent c: child
    parent[c] = p
```

- root 찾기, 조상 찾기  
> 자식 c  - 0, 1, 2, 3, 4, 5  
> 부모 p = [0, 0, 1, 1, 3, 3]
> e.g. 5번 노드의 조상찾기
```python
# 이 경우 부모가 0이면 root node 임
c = 5
while(a[c] !=  0):  # root인지 확인
    c = a[c]
    anc.append(c)   # 조상 목록
root = c
```

> [참고] 배열을 이용한 이진 트리의 표현의 단점  
>- 편향 이진 트리의 경우에 사용하지 않는 배열 원소에 대한 메모리 공간 낭비 발생 
>- 트리의 중간에 새로운 노드를 삽입하거나 기존 노드를 삭제할 경우, 배열의 크기 변경 어려워 비효율적  

```python
# 정점 번호 V = 1(E+1)
# 간선 수
# 부모 자식 순
# 4
# 1 2 1 3 3 4 3 5 
def find_root(V): # V : 마지막 정점의 번호
    for i in range(1, V + 1):
        if parent[i] == 0: # parent[i]에 부모가 없으면 
        return i  # i가 root

def preorder(n):   # 전위순휘
    if n:
        print(n) # 현재 노드 n 처리
        preorder(ch1[n]) # 왼쪽 자식 노드 순회
        preorder(ch2[n]) # 오른쪽 자식 노드 순회

def inorder(n):    # 중위순회
    if n:
        inorder(ch1[n]) # 왼쪽 자식 노드 순회
        print(n) # 현재 노드 n 처리
        inorder(ch2[n]) # 오른쪽 자식 노드 순회

def postorder(n):    # 후위순회
    if n:
        postorder(ch1[n]) # 왼쪽 자식 노드 순회
        postorder(ch2[n]) # 오른쪽 자식 노드 순회  
        print(n) # 현재 노드 n 처리  

E = int(input())   # 간선의 수
arr = list(map(int, input().split()) 
root = 1
V = E + 1  # 노드의 수
# 부모를 인덱스로 자식 번호 저장 
ch1 = [0] * (V + 1) # 인덱스 0, 1, 2, 3, 4까지 있는 ch1배열 선언
ch2 = [0] * (V + 1) 

for i in range(E):
    p = arr[i*2]
    c = arr[i*2+1]
# for j in range(0, E*2, 2):  
#     p, c = arr[j], arr[j+1]
    if ch1[p] == 0:
        ch1[p] = c
    else:
        ch2[p] = c

preorder(root)
inorder(root)
postorder(root)

# 자식을 인덱스로 부모 번호 저장 
parent = [0] * (V + 1)
for i in range(E):
    p = arr[i*2]
    c = arr[i*2+1]
    parent[c] = p

```
### 트리의 표현 - 연결 리스트 (Linked List)
배열을 이용한 이진 트리의 표현의 단점을 보안하기 위하여 연결리스트를 이용하여 트리를 표혀할 수 있다. 
- 연결리스트를 이용한 이진트리의 표현  
이진 트리의 모든 노드는 최대 2개의 자식 노드를 가지므로 일정한 구조의 단순 연결 리스트 노드를 사용하여 구현  

### 수식 트리(Expression Binary Tree)
= 수식 이진 트리  
연산자는 루트 노드이거나 가지 노드(리프 노드 위 노드)  
피연산자는 모두 리프 노드  

#### 수식 트리 순회
- 중위 순회
    - A / B * C * D + E (식의 중위표기법)
- 후위 순회
    - A B / C * D * E + (식의 후위표기법)
- 전위 순회
    - / * * + A B C D E (식의 전위표기법)

### 이진 탐색 트리
- 탐색 작업을 효율적으로 하기 위한 자료구조
- 모든 원소는 서로 다른 유일한 키를 가짐
- key(왼쪽 서브트리) < key(루트 노드) < key(오른쪽 서브트리)   
왼쪽 서브트리 : 루트 노드보다 작은 값  
오른쪽 서브트리 : 루트 노드보다 큰 값  
> **중위 순회 하면 오름차순으로 정렬된 값을 얻을 수 있다**
#### 탐색 연산
1. 루트에서 시작 
2. 탐색할 키 값 x를 루트노드의 키 값과 비교 
    - (x == 루트노드의 키 값)인 경우: 탐색 연산 성공
    - (x > 루트노드의 키 값)인 경우: 루트노드의 왼쪽 서브트리에 대해서 탐색 연산 수행
    - (x < 루트노드의 키 값)인 경우: 루트노드의 오른쪽 서브트리에 대해서 탐색 연산 수행
3. 서브트리에 대해서 순환적으로 탐색 연산 반복

#### 삽입 연산
1. 먼저 탐색 연산을 수행
    - 삽입할 원소와 값이 같은 원소가 트리에 있으면 삽입할 수 없으므로, 같은 원소가 트리에 있는지 탐색하여 확인
    - 탐색에서 탐색실패가 되는 위치가 삽입 위치
2. 탐색 실패한 위치에 원소 삽입

>##### 이진 탐색 트리 - 성능
> 탐색(searching), 삽입(insertion), 삭제(deletion) 시간은 트리의 높이만큼 시간이 걸림  
> O(h) , h : BST의 깊이(height)  
> - 평균의 경우
>   - 이진트리가 균형적으로 생성되어 있는 경우
>   - O(log n)
> - 최악의 경우
>   - 한 쪽으로 치우친 경사의 이진트리 
>   - O(n)
>   - 순차탐색과 시간복잡도가 같음   

> - **검색 알고리즘 비교**  
>   - 배열에서의 순차 검색 : O(n)
>   - 정렬된 배열에서의 순차 검색 : O(n)
>   - 정렬된 배열에서의 이진 탐색 : O(log n)
>       - 고정 배열 크기와 삽입, 삭제 시 추가 연산 필요
>   - 이진 탐색 트리에서의 평균: O(log n)
>       - 최약의 경위 O(n)  
>       - 완전 이진 트리 혹은 균형트리로 만들 수 있다면 최악의 경우를 없앨 수 있다.  
>           - 새로운 원소를 삽입할 때 삽입 시간을 줄임
>           - 평균과 최악의 시간이 같음 : O(log n)
>   - 해쉬 검색: O(1)
>       - 단, 추가 저장 공간이 필요

### 힙 Heap
**완전 이진 트리**에 있는 노드 중에서 키 값이 가장 큰 노드나 키 값이 가장 작은 노드를 찾기 위해 만든 자료 구조   
1. **최대 힙 max heap**  
키 값이 가장 큰 노드를 찾기 위한 완전 이진 트리  
부모 노드 키 값 > 자식 노드 키 값  
루트 노드 : 키 값이 가장 큰 노드   
2. **최소 힙 min heap**   
키 값이 작은 큰 노드를 찾기 위한 완전 이진 트리  
부모 노드 키 값 < 자식 노드 키 값  
루트 노드 : 키 값이 가장 작은 노드   

```python
# 최대힙
def enq(n):
    global last
    last += 1       # 마지막 정점 추가
    heap[last] = n  # 마지막 정점에 key 추가

    # 부모가 없거나 부모 > 자식 조건을 만족할 때까지 
    # 부모 <-> 자식 자리 교환
    c = last
    p = c // 2      # 완전 이진 트리에서 부모 정점 번호

    while p and heap[p] < heap[c]:
        # 부모가 없다면 넘어갈 것 while p 
        heap[p], heap[c] = heap[c], heap[p]
        c = p       # 부모를 새로운 자식으로 
        p = c // 2  # 조상까지 다 확인
heap = [0] * 100
last = 0
```
#### 힙 연산 - 삭제(deletion)
힙에서는 루트 노드 원소만을 삭제할 수 있다  
루트노드의 원소를 삭제하여 반환한다  
힙의 종류에 따라 최대값 혹은 최소값을 구할 수 있다  

```python
def deq(n):
    global last
    tmp = heap[1]               # 루트 백업
    heap[1] = heal[last]        # 삭제할 노드의 키를 루트에 복사
    last -= 1                   # 마지막 노드 삭제
    # 루트에 옮긴 값과 자식 비교
    p = 1
    c = p * 2                   # 왼쪽 자식
    while c <= last:            # 자식이 하나라도 있으면
        if c + 1 <= last and heap[c] < heap[c+1]: # 오른쪽 자식도 있고, 왼쪽 자식보다 오른쪽 자식이 더 크면
        c += 1                  # 오른쪽 자식을 비교대상으로 정함
        # 아니면 왼쪽 자식을 비교대상으로 정함
        if heap[p] < heap[c]:   # 자식이 부모보다 크면 규칙에 어긋나므로
            heap[p], heap[c] = heap[c], heap[p]
            p = c               # 자식을 새로운 부모로 교체
            c = p * 2           # 왼쪽 자식 번호를 확인
        else:                   # 부모가 더 크면 비교 중단
            break

heap = [0] * 100
last = 0 
```
> 힙의 키를 우선순위로 활용하여 우선순위 큐를 구현할 수 있다  