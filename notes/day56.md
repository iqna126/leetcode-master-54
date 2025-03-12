# 第十一章 图论part02

今日任务：99.岛屿数量 深搜， 99.岛屿数量 广搜， 100.岛屿的最大面积 

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)


## 卡码网99.[岛屿数量 深搜](https://kamacoder.com/problempage.php?pid=1171)
方法一
```python
direction =[[1,0],[0,1],[-1,0],[0,-1]]
def dfs(graph, visited, x, y):
    for i, j in direction:
        next_x = x+i
        next_y = y+j
        if next_x< 0 or next_x>=len(graph) or next_y < 0 or next_y>=len(graph[0]):
            continue
        if graph[next_x][next_y] == 1 and visited[next_x][next_y] is False:
            visited[next_x][next_y] = True
            dfs(graph,visited,next_x,next_y)   

def main():
    n, m = map(int,input().split())
    graph = []
    for i in range(n):
        graph.append(list(map(int,input().split())))
        
    visited = [[False] * m for _ in range(n)]

    res = 0
    for i in range(n):
        for j in range(m):
            if graph[i][j] == 1 and visited[i][j] is False:
                res += 1
                visited[i][j] = True
                dfs(graph, visited, i, j)
    print(res)

if __name__ == "__main__":
    main()
   
```

方法二
```python
direction =[[1,0],[0,1],[-1,0],[0,-1]]
def dfs(graph, visited, x, y):
    if visited[x][y] or graph[x][y] == 0:
        return
    visited[x][y] = True

    for i, j in direction:
        next_x = x+i
        next_y = y+j
        if next_x< 0 or next_x>=len(graph) or next_y < 0 or next_y>=len(graph[0]):
            continue
        dfs(graph,visited,next_x,next_y)

def main():
    n, m = map(int,input().split())
    graph = []
    for i in range(n):
        graph.append(list(map(int,input().split())))
        
    visited = [[False] * m for _ in range(n)]

    res = 0
    for i in range(n):
        for j in range(m):
            if graph[i][j] == 1 and visited[i][j] is False:
                res += 1
                dfs(graph, visited, i, j)
    print(res)

if __name__ == "__main__":
    main()
```

## 卡码网99.[岛屿数量 广搜](https://kamacoder.com/problempage.php?pid=1171)
```python
from collections import deque
directions = [[0, 1], [1, 0], [0, -1], [-1, 0]]
def bfs(grid, visited, x, y):
    que = deque([])
    que.append([x,y])
    visited[x][y] = True
    while que:
        cur_x, cur_y = que.popleft()
        for i, j in directions:
            next_x = cur_x + i
            next_y = cur_y + j
            if next_y < 0 or next_x < 0 or next_x >= len(grid) or next_y >= len(grid[0]):
                continue
            if not visited[next_x][next_y] and grid[next_x][next_y] == 1: 
                visited[next_x][next_y] = True
                que.append([next_x, next_y])


def main():
    n, m = map(int, input().split())
    grid = []
    for i in range(n):
        grid.append(list(map(int, input().split())))
    visited = [[False] * m for _ in range(n)]
    res = 0
    for i in range(n):
        for j in range(m):
            if grid[i][j] == 1 and not visited[i][j]:
                res += 1
                bfs(grid, visited, i, j)
    print(res)

if __name__ == "__main__":
    main()
   
```

## 卡码网100.[岛屿的最大面积](https://kamacoder.com/problempage.php?pid=1172)
```python
direction =[[1,0],[0,1],[-1,0],[0,-1]]
def dfs(graph, visited, x, y):
    if visited[x][y] or graph[x][y] == 0:
        return 0
    visited[x][y] = True
    cur = 1
    for i, j in direction:
        next_x = x+i
        next_y = y+j
        if next_x< 0 or next_x>=len(graph) or next_y < 0 or next_y>=len(graph[0]):
            continue
        cur += dfs(graph,visited,next_x,next_y)
    return cur

def main():
    n, m = map(int,input().split())
    graph = []
    for i in range(n):
        graph.append(list(map(int,input().split())))
        
    visited = [[False] * m for _ in range(n)]

    res = 0
    for i in range(n):
        for j in range(m):
            if graph[i][j] == 1 and visited[i][j] is False:
                size = dfs(graph, visited, i, j)
                res = max(res, size)
    print(res)

if __name__ == "__main__":
    main()
```
