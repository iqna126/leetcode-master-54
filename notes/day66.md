# 第十一章 图论part11

今日任务： Floyd 算法精讲， A * 算法精讲 （A star算法）， 最短路算法总结篇， 图论总结

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## [Floyd 算法精讲](https://www.programmercarl.com/kamacoder/0097.%E5%B0%8F%E6%98%8E%E9%80%9B%E5%85%AC%E5%9B%AD.html#%E6%80%9D%E8%B7%AF)
```python
if __name__ == '__main__':
    max_int = 10005  # 设置最大路径，因为边最大距离为10^4

    n, m = map(int, input().split())

    grid = [[max_int]*(n+1) for _ in range(n+1)]  # 初始化二维dp数组

    for _ in range(m):
        p1, p2, val = map(int, input().split())
        grid[p1][p2] = val
        grid[p2][p1] = val

    # 开始floyd
    for k in range(1, n+1):
        for i in range(1, n+1):
            for j in range(1, n+1):
                grid[i][j] = min(grid[i][j], grid[i][k] + grid[k][j])

    # 输出结果
    z = int(input())
    for _ in range(z):
        start, end = map(int, input().split())
        if grid[start][end] == max_int:
            print(-1)
        else:
            print(grid[start][end])
```

## [A * 算法精讲 （A star算法）](https://www.programmercarl.com/kamacoder/0126.%E9%AA%91%E5%A3%AB%E7%9A%84%E6%94%BB%E5%87%BBastar.html#%E6%80%9D%E8%B7%AF)
```python
import heapq
 
n = int(input())
 
moves = [(1, 2), (2, 1), (-1, 2), (2, -1), (1, -2), (-2, 1), (-1, -2), (-2, -1)]
 
def distance(a, b):
    return ((a[0] - b[0]) ** 2 + (a[1] - b[1]) ** 2) ** 0.5
 
def bfs(start, end):
    q = [(distance(start, end), start)]
    step = {start: 0}
     
    while q:
        d, cur = heapq.heappop(q)
        if cur == end:
            return step[cur]
        for move in moves:
            new = (move[0] + cur[0], move[1] + cur[1])
            if 1 <= new[0] <= 1000 and 1 <= new[1] <= 1000:
                step_new = step[cur] + 1
                if step_new < step.get(new, float('inf')):
                    step[new] = step_new
                    heapq.heappush(q, (distance(new, end) + step_new, new))
    return False
                     
for _ in range(n):
    a1, a2, b1, b2 = map(int, input().split())
    print(bfs((a1, a2), (b1, b2)))
```

## [最短路算法总结篇](https://www.programmercarl.com/kamacoder/%E6%9C%80%E7%9F%AD%E8%B7%AF%E9%97%AE%E9%A2%98%E6%80%BB%E7%BB%93%E7%AF%87.html)

## [图论总结](https://www.programmercarl.com/kamacoder/%E5%9B%BE%E8%AE%BA%E6%80%BB%E7%BB%93%E7%AF%87.html#%E6%8B%93%E6%89%91%E6%8E%92%E5%BA%8F)
