# 第十一章 图论part07

今日任务： prim算法精讲， kruskal算法精讲

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## [prim算法精讲](https://www.programmercarl.com/kamacoder/0053.%E5%AF%BB%E5%AE%9D-prim.html)
[卡码网53.寻宝](https://kamacoder.com/problempage.php?pid=1053)
最小生成树(以最小的成本将图中所有的节点连接到一起)模版题  
当有n个节点，那么一定可以用n-1条边把整个图连接起来，最小生成树算法解决悬着这n-1条边的问题  
prim三部曲：
1. 选择距离生成树最近节点
2. 将最近节点加入生成树
3. 更新非生成树节点到生成树的距离
```python
# 接收输入
v, e = list(map(int, input().strip().split()))
# 按照常规的邻接矩阵存储图信息，不可达的初始化为10001
graph = [[10001] * (v+1) for _ in range(v+1)]
for _ in range(e):
    x, y, w = list(map(int, input().strip().split()))
    graph[x][y] = w
    graph[y][x] = w

# 定义加入生成树的标记数组和未加入生成树的最近距离
visited = [False] * (v + 1)
minDist = [10001] * (v + 1)

# 循环 n - 1 次，建立 n - 1 条边
# 从节点视角来看：每次选中一个节点加入树，更新剩余的节点到树的最短距离，
# 这一步其实蕴含了确定下一条选取的边，计入总路程 ans 的计算
for _ in range(1, v + 1):
    min_val = 10002
    cur = -1
    for j in range(1, v + 1):
        if visited[j] == False and minDist[j] < min_val:
            cur = j
            min_val = minDist[j]
    visited[cur] = True
    for j in range(1, v + 1):
        if visited[j] == False and minDist[j] > graph[cur][j]:
            minDist[j] = graph[cur][j]

ans = 0
for i in range(2, v + 1):
    ans += minDist[i]
print(ans)
```

## [kruskal算法精讲](https://www.programmercarl.com/kamacoder/0053.%E5%AF%BB%E5%AE%9D-Kruskal.html)
[卡码网53.寻宝](https://kamacoder.com/problempage.php?pid=1053)
最小生成树模版题
并查集
```python
class Edge:
    def __init__(self, l, r, val):
        self.l = l
        self.r = r
        self.val = val

n = 10001
father = list(range(n))

def init():
    global father
    father = list(range(n))

def find(u):
    if u != father[u]:
        father[u] = find(father[u])
    return father[u]

def join(u, v):
    u = find(u)
    v = find(v)
    if u != v:
        father[v] = u

def kruskal(v, edges):
    edges.sort(key=lambda edge: edge.val)
    init()
    result_val = 0

    for edge in edges:
        x = find(edge.l)
        y = find(edge.r)
        if x != y:
            result_val += edge.val
            join(x, y)

    return result_val

if __name__ == "__main__":
    import sys
    input = sys.stdin.read
    data = input().split()

    v = int(data[0])
    e = int(data[1])

    edges = []
    index = 2
    for _ in range(e):
        v1 = int(data[index])
        v2 = int(data[index + 1])
        val = int(data[index + 2])
        edges.append(Edge(v1, v2, val))
        index += 3

    result_val = kruskal(v, edges)
    print(result_val)
   
```