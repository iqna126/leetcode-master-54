# 第十一章 图论part03

今日任务： 101.孤岛的总面积， 102.沉没孤岛， 103.水流问题， 104.建造最大岛屿

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 卡码网101.[孤岛的总面积](https://kamacoder.com/problempage.php?pid=1173)
DFS
```python
position = [[1, 0], [0, 1], [-1, 0], [0, -1]]
count = 0

def dfs(grid, x, y):
    global count
    grid[x][y] = 0
    count += 1
    for i, j in position:
        next_x = x + i
        next_y = y + j
        if next_x < 0 or next_y < 0 or next_x >= len(grid) or next_y >= len(grid[0]):
            continue
        if grid[next_x][next_y] == 1: 
            dfs(grid, next_x, next_y)
                
n, m = map(int, input().split())

# 邻接矩阵
grid = []
for i in range(n):
    grid.append(list(map(int, input().split())))

# 清除边界上的连通分量
for i in range(n):
    if grid[i][0] == 1: 
        dfs(grid, i, 0)
    if grid[i][m - 1] == 1: 
        dfs(grid, i, m - 1)

for j in range(m):
    if grid[0][j] == 1: 
        dfs(grid, 0, j)
    if grid[n - 1][j] == 1: 
        dfs(grid, n - 1, j)
    
count = 0 # 将count重置为0
# 统计内部所有剩余的连通分量
for i in range(n):
    for j in range(m):
        if grid[i][j] == 1:
            dfs(grid, i, j)
            
print(count)
   
```

## 卡码网102.[沉没孤岛](https://kamacoder.com/problempage.php?pid=1174)
DFS
```python
def dfs(grid, x, y):
    grid[x][y] = 2
    directions = [(-1, 0), (0, -1), (1, 0), (0, 1)]  # 四个方向
    for dx, dy in directions:
        nextx, nexty = x + dx, y + dy
        # 超过边界
        if nextx < 0 or nextx >= len(grid) or nexty < 0 or nexty >= len(grid[0]):
            continue
        # 不符合条件，不继续遍历
        if grid[nextx][nexty] == 0 or grid[nextx][nexty] == 2:
            continue
        dfs(grid, nextx, nexty)

def main():
    n, m = map(int, input().split())
    grid = [[int(x) for x in input().split()] for _ in range(n)]

    # 步骤一：
    # 从左侧边，和右侧边 向中间遍历
    for i in range(n):
        if grid[i][0] == 1:
            dfs(grid, i, 0)
        if grid[i][m - 1] == 1:
            dfs(grid, i, m - 1)

    # 从上边和下边 向中间遍历
    for j in range(m):
        if grid[0][j] == 1:
            dfs(grid, 0, j)
        if grid[n - 1][j] == 1:
            dfs(grid, n - 1, j)

    # 步骤二、步骤三
    for i in range(n):
        for j in range(m):
            if grid[i][j] == 1:
                grid[i][j] = 0
            if grid[i][j] == 2:
                grid[i][j] = 1

    # 打印结果
    for row in grid:
        print(' '.join(map(str, row)))

if __name__ == "__main__":
    main()
   
```

## 卡码网103.[水流问题](https://kamacoder.com/problempage.php?pid=1175)
```python
first = set()
second = set()
directions = [[-1, 0], [0, 1], [1, 0], [0, -1]]

def dfs(i, j, graph, visited, side):
    if visited[i][j]:
        return
    
    visited[i][j] = True
    side.add((i, j))
    
    for x, y in directions:
        new_x = i + x
        new_y = j + y
        if (
            0 <= new_x < len(graph)
            and 0 <= new_y < len(graph[0])
            and int(graph[new_x][new_y]) >= int(graph[i][j])
        ):
            dfs(new_x, new_y, graph, visited, side)

def main():
    global first
    global second
    
    N, M = map(int, input().strip().split())
    graph = []
    for _ in range(N):
        row = input().strip().split()
        graph.append(row)
    
    # 是否可到达第一边界
    visited = [[False] * M for _ in range(N)]
    for i in range(M):
        dfs(0, i, graph, visited, first)
    for i in range(N):
        dfs(i, 0, graph, visited, first)
    
    # 是否可到达第二边界
    visited = [[False] * M for _ in range(N)]
    for i in range(M):
        dfs(N - 1, i, graph, visited, second)
    for i in range(N):
        dfs(i, M - 1, graph, visited, second)

    # 可到达第一边界和第二边界
    res = first & second
    
    for x, y in res:
        print(f"{x} {y}")
    
    
if __name__ == "__main__":
    main()
```

## 卡码网104.[建造最大岛屿](https://kamacoder.com/problempage.php?pid=1176)
DFS
```python
import collections

directions = [[-1, 0], [0, 1], [0, -1], [1, 0]]
area = 0

def dfs(i, j, grid, visited, num):
    global area
    
    if visited[i][j]:
        return

    visited[i][j] = True
    grid[i][j] = num  # 标记岛屿号码
    area += 1
    
    for x, y in directions:
        new_x = i + x
        new_y = j + y
        if (
            0 <= new_x < len(grid)
            and 0 <= new_y < len(grid[0])
            and grid[new_x][new_y] == "1"
        ):
            dfs(new_x, new_y, grid, visited, num)
    

def main():
    global area
    
    N, M = map(int, input().strip().split())
    grid = []
    for i in range(N):
        grid.append(input().strip().split())
    visited = [[False] * M for _ in range(N)]
    rec = collections.defaultdict(int)
    
    cnt = 2
    for i in range(N):
        for j in range(M):
            if grid[i][j] == "1":
                area = 0
                dfs(i, j, grid, visited, cnt)
                rec[cnt] = area  # 纪录岛屿面积
                cnt += 1
    
    res = 0
    for i in range(N):
        for j in range(M):
            if grid[i][j] == "0":
                max_island = 1  # 将水变为陆地，故从1开始计数
                v = set()
                for x, y in directions:
                    new_x = i + x
                    new_y = j + y
                    if (
                        0 <= new_x < len(grid)
                        and 0 <= new_y < len(grid[0])
                        and grid[new_x][new_y] != "0"
                        and grid[new_x][new_y] not in v  # 岛屿不可重复
                    ):
                        max_island += rec[grid[new_x][new_y]]
                        v.add(grid[new_x][new_y])
                res = max(res, max_island)

    if res == 0:
        return max(rec.values())  # 无水的情况
    return res
    
if __name__ == "__main__":
    print(main())
```