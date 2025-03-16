# 第十一章 图论part08

今日任务： 拓扑排序精讲， dijkstra（朴素版）精讲

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## [拓扑排序精讲](https://www.programmercarl.com/kamacoder/0117.%E8%BD%AF%E4%BB%B6%E6%9E%84%E5%BB%BA.html#%E6%8B%93%E6%89%91%E6%8E%92%E5%BA%8F%E7%9A%84%E8%83%8C%E6%99%AF)
其实只要能在把 有向无环图 进行线性排序 的算法 都可以叫做 拓扑排序。
实现拓扑排序的算法有两种：卡恩算法（BFS）和DFS
```python
from collections import deque, defaultdict

def topological_sort(n, edges):
    inDegree = [0] * n # inDegree 记录每个文件的入度
    umap = defaultdict(list) # 记录文件依赖关系

    # 构建图和入度表
    for s, t in edges:
        inDegree[t] += 1
        umap[s].append(t)

    # 初始化队列，加入所有入度为0的节点
    queue = deque([i for i in range(n) if inDegree[i] == 0])
    result = []

    while queue:
        cur = queue.popleft()  # 当前选中的文件
        result.append(cur)
        for file in umap[cur]:  # 获取该文件指向的文件
            inDegree[file] -= 1  # cur的指向的文件入度-1
            if inDegree[file] == 0:
                queue.append(file)

    if len(result) == n:
        print(" ".join(map(str, result)))
    else:
        print(-1)


if __name__ == "__main__":
    n, m = map(int, input().split())
    edges = [tuple(map(int, input().split())) for _ in range(m)]
    topological_sort(n, edges)
   
```

## [dijkstra（朴素版）精讲](https://www.programmercarl.com/kamacoder/0047.%E5%8F%82%E4%BC%9Adijkstra%E6%9C%B4%E7%B4%A0.html)
dijkstra三部曲：
1. 选源点到哪个节点近且该节点未被访问过
2. 该最近节点被标记访问过
3. 更新非访问节点到源点的距离（即更新minDist数组）


```python
import sys

def dijkstra(n, m, edges, start, end):
    # 初始化邻接矩阵
    grid = [[float('inf')] * (n + 1) for _ in range(n + 1)]
    for p1, p2, val in edges:
        grid[p1][p2] = val

    # 初始化距离数组和访问数组
    minDist = [float('inf')] * (n + 1)
    visited = [False] * (n + 1)

    minDist[start] = 0  # 起始点到自身的距离为0

    for _ in range(1, n + 1):  # 遍历所有节点
        minVal = float('inf')
        cur = -1

        # 选择距离源点最近且未访问过的节点
        for v in range(1, n + 1):
            if not visited[v] and minDist[v] < minVal:
                minVal = minDist[v]
                cur = v

        if cur == -1:  # 如果找不到未访问过的节点，提前结束
            break

        visited[cur] = True  # 标记该节点已被访问

        # 更新未访问节点到源点的距离
        for v in range(1, n + 1):
            if not visited[v] and grid[cur][v] != float('inf') and minDist[cur] + grid[cur][v] < minDist[v]:
                minDist[v] = minDist[cur] + grid[cur][v]

    return -1 if minDist[end] == float('inf') else minDist[end]

if __name__ == "__main__":
    input = sys.stdin.read
    data = input().split()
    n, m = int(data[0]), int(data[1])
    edges = []
    index = 2
    for _ in range(m):
        p1 = int(data[index])
        p2 = int(data[index + 1])
        val = int(data[index + 2])
        edges.append((p1, p2, val))
        index += 3
    start = 1  # 起点
    end = n    # 终点

    result = dijkstra(n, m, edges, start, end)
    print(result)
   
```
思考： 为什么prim算法可以处理负权值，但是dijkstra不行