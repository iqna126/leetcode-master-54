# 第十一章 图论part10

今日任务： Bellman_ford 队列优化算法（又名SPFA）， Bellman_ford之判断负权回路， Bellman_ford之单源有限最短路

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## [Bellman_ford 队列优化算法（又名SPFA）](https://www.programmercarl.com/kamacoder/0094.%E5%9F%8E%E5%B8%82%E9%97%B4%E8%B4%A7%E7%89%A9%E8%BF%90%E8%BE%93I-SPFA.html#%E8%83%8C%E6%99%AF)
```python
import collections


n, m = map(int, input().strip().split())
edges = [[] for _ in range(n + 1)]
for _ in range(m):
    src, dest, weight = map(int, input().strip().split())
    edges[src].append([dest, weight])

minDist = [float("inf")] * (n + 1)
minDist[1] = 0
que = collections.deque([1])
visited = [False] * (n + 1)
visited[1] = True

while que:
    cur = que.popleft()
    visited[cur] = False
    for dest, weight in edges[cur]:
        if minDist[cur] != float("inf") and minDist[cur] + weight < minDist[dest]:
            minDist[dest] = minDist[cur] + weight
            if visited[dest] == False:
                que.append(dest)
                visited[dest] = True

if minDist[-1] == float("inf"):
    return "unconnected"
print(minDist[-1])
   
```

## [Bellman_ford之判断负权回路](https://www.programmercarl.com/kamacoder/0095.%E5%9F%8E%E5%B8%82%E9%97%B4%E8%B4%A7%E7%89%A9%E8%BF%90%E8%BE%93II.html)
```python
import sys

def main():
    input = sys.stdin.read
    data = input().split()
    index = 0
    
    n = int(data[index])
    index += 1
    m = int(data[index])
    index += 1
    
    grid = []
    for i in range(m):
        p1 = int(data[index])
        index += 1
        p2 = int(data[index])
        index += 1
        val = int(data[index])
        index += 1
        # p1 指向 p2，权值为 val
        grid.append([p1, p2, val])

    start = 1  # 起点
    end = n    # 终点

    minDist = [float('inf')] * (n + 1)
    minDist[start] = 0
    flag = False

    for i in range(1, n + 1):  # 这里我们松弛n次，最后一次判断负权回路
        for side in grid:
            from_node = side[0]
            to = side[1]
            price = side[2]
            if i < n:
                if minDist[from_node] != float('inf') and minDist[to] > minDist[from_node] + price:
                    minDist[to] = minDist[from_node] + price
            else:  # 多加一次松弛判断负权回路
                if minDist[from_node] != float('inf') and minDist[to] > minDist[from_node] + price:
                    flag = True

    if flag:
        print("circle")
    elif minDist[end] == float('inf'):
        print("unconnected")
    else:
        print(minDist[end])

if __name__ == "__main__":
    main()

   
```

## [Bellman_ford之单源有限最短路](https://www.programmercarl.com/kamacoder/0096.%E5%9F%8E%E5%B8%82%E9%97%B4%E8%B4%A7%E7%89%A9%E8%BF%90%E8%BE%93III.html#%E6%80%9D%E8%B7%AF)
```python
def main():
    # 輸入
    n, m = map(int, input().split())
    edges = list()
    for _ in range(m):
        edges.append(list(map(int, input().split() )))
    
    start, end, k = map(int, input().split())
    min_dist = [float('inf') for _ in range(n + 1)]
    min_dist[start] = 0
    
    # 只能經過k個城市，所以從起始點到中間有(k + 1)個邊連接
    # 需要鬆弛(k + 1)次
    
    for _ in range(k + 1):
        update = False
        min_dist_copy = min_dist.copy()
        for src, desc, w in edges:
            if (min_dist_copy[src] != float('inf') and 
            min_dist_copy[src] + w < min_dist[desc]):
                min_dist[desc] = min_dist_copy[src] + w
                update = True
        if not update:
            break
    # 輸出
    if min_dist[end] == float('inf'):
        print('unreachable')
    else:
        print(min_dist[end])
            
            

if __name__ == "__main__":
    main()
```