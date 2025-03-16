# 第十一章 图论part05

今日任务： 并查集理论基础， 107.寻找存在的路径

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## [并查集理论基础](https://www.programmercarl.com/kamacoder/%E5%9B%BE%E8%AE%BA%E5%B9%B6%E6%9F%A5%E9%9B%86%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html#%E8%83%8C%E6%99%AF)
并查集通常来解决连通性问题 
并查集的两个功能：
1. 将两个元素添加到一个集合中
2. 判断两个元素在不在同一个集合中

## 卡码网107.[寻找存在的路径](https://kamacoder.com/problempage.php?pid=1179)
```python

class UnionFind:
    def __init__(self, size):
        self.parent = list(range(size + 1))  # 初始化并查集

    def find(self, u):
        if self.parent[u] != u:
            self.parent[u] = self.find(self.parent[u])  # 路径压缩
        return self.parent[u]

    def union(self, u, v):
        root_u = self.find(u)
        root_v = self.find(v)
        if root_u != root_v:
            self.parent[root_v] = root_u

    def is_same(self, u, v):
        return self.find(u) == self.find(v)


def main():
    import sys
    input = sys.stdin.read
    data = input().split()
    
    index = 0
    n = int(data[index])
    index += 1
    m = int(data[index])
    index += 1
    
    uf = UnionFind(n)
    
    for _ in range(m):
        s = int(data[index])
        index += 1
        t = int(data[index])
        index += 1
        uf.union(s, t)
    
    source = int(data[index])
    index += 1
    destination = int(data[index])
    
    if uf.is_same(source, destination):
        print(1)
    else:
        print(0)

if __name__ == "__main__":
    main()

   
```