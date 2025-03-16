# 第十一章 图论part09

今日任务： dijkstra（堆优化版）精讲， Bellman_ford 算法精讲

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## [dijkstra（堆优化版）精讲](https://www.programmercarl.com/kamacoder/0047.%E5%8F%82%E4%BC%9Adijkstra%E5%A0%86.html)
```python
import heapq

class Edge:
    def __init__(self, to, val):
        self.to = to
        self.val = val

def dijkstra(n, m, edges, start, end):
    grid = [[] for _ in range(n + 1)]

    for p1, p2, val in edges:
        grid[p1].append(Edge(p2, val))

    minDist = [float('inf')] * (n + 1)
    visited = [False] * (n + 1)

    pq = []
    heapq.heappush(pq, (0, start))
    minDist[start] = 0

    while pq:
        cur_dist, cur_node = heapq.heappop(pq)

        if visited[cur_node]:
            continue

        visited[cur_node] = True

        for edge in grid[cur_node]:
            if not visited[edge.to] and cur_dist + edge.val < minDist[edge.to]:
                minDist[edge.to] = cur_dist + edge.val
                heapq.heappush(pq, (minDist[edge.to], edge.to))

    return -1 if minDist[end] == float('inf') else minDist[end]

# 输入
n, m = map(int, input().split())
edges = [tuple(map(int, input().split())) for _ in range(m)]
start = 1  # 起点
end = n    # 终点

# 运行算法并输出结果
result = dijkstra(n, m, edges, start, end)
print(result)

   
```

## [Bellman_ford 算法精讲](https://www.programmercarl.com/kamacoder/0094.%E5%9F%8E%E5%B8%82%E9%97%B4%E8%B4%A7%E7%89%A9%E8%BF%90%E8%BE%93I.html)
```python
def main():
    n, m = map(int, input().strip().split())
    edges = []
    for _ in range(m):
        src, dest, weight = map(int, input().strip().split())
        edges.append([src, dest, weight])
    
    minDist = [float("inf")] * (n + 1)
    minDist[1] = 0  # 起点处距离为0
    
    for i in range(1, n):
        updated = False
        for src, dest, weight in edges:
            if minDist[src] != float("inf") and minDist[src] + weight < minDist[dest]:
                minDist[dest] = minDist[src] + weight
                updated = True
        if not updated:  # 若边不再更新，即停止回圈
            break
    
    if minDist[-1] == float("inf"):  # 返还终点权重
        return "unconnected"
    return minDist[-1]
    
if __name__ == "__main__":
    print(main())
```