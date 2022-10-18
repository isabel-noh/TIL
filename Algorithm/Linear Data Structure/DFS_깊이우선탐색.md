
# DFS(Depth First Search) 깊이 우선 탐색
비선형구조인 그래프 구조는 그래프로 표현된 모든 자료를 빠짐없이 검색하는 것이 중요  
- 깊이 우선 탐색(Depth First Search, DFS)
- 너비 우선 탐색(Breadth First Search, BFS)

## DFS algorithm 
```c++
visited[], stack[] 초기화
DFS(v)
    시작점 v 방문;
    visited[v] <- true
    while{
        if(v 인접 접점 중 방문하지 않은 w가 있으면){
            push(v);
            v <- w; (w에 방문)
            visited[w] <- true;
        }
        else{
            if(stack이 비어있지 않으면){
                v <- pop(stack);
            }
            else{
                break
            }
        }
    }
end DFS()
```

```python
adjList = [[1, 2],
            [0, 3, 4],
            [0, 4],
            [1,5 ],
            [1, 2, 5],
            [3, 4, 6],
            [5]]
def dfs(v, N):
    visited = [0] * N
    stack =  [0] * N
    top = -1

    visited[v] = 1
    while True:
        for w in adjList[v]:
            if visited[w] == 0:      # v의 인접접점에 방문하지 않은 w가 있으면
                top += 1
                stack[top] = v      # push(v)
                v = w
                visited[w] = 1      # w 방문
                break
        else:                       # w가 없으면
            if stack[top] != -1:    # stack이 비어있지 않으면
                v = stack[top]
                top -= 1
            else:                   # stack이 비어있으면
                break

```