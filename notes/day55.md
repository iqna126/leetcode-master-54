# 第十一章 图论part01

今日任务： 图论理论基础， 深搜理论基础， 卡码网98.所有可达路径， 广搜理论基础

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## [图论理论基础](https://programmercarl.com/kamacoder/%E5%9B%BE%E8%AE%BA%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html#%E5%9B%BE%E7%9A%84%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5)

## [深搜理论基础](https://programmercarl.com/kamacoder/%E5%9B%BE%E8%AE%BA%E6%B7%B1%E6%90%9C%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)

## 卡码网98.[所有可达路径](https://kamacoder.com/problempage.php?pid=1170)
使用邻接矩阵存储图
```python
    def dfs(graph, x, n, path, result):
        if x == n:
            result.append(path.copy())
            return
        for i in range(1, n + 1):
            if graph[x][i] == 1:
                path.append(i)
                dfs(graph, i, n, path, result)
                path.pop()

    def main():
        n, m = map(int, input().split())
        graph = [[0] * (n + 1) for _ in range(n + 1)]

        for _ in range(m):
            s, t = map(int, input().split())
            graph[s][t] = 1

        result = []
        dfs(graph, 1, n, [1], result)

        if not result:
            print(-1)
        else:
            for path in result:
                print(' '.join(map(str, path)))

    if __name__ == "__main__":
        main()
    
```
使用邻接表存储图
```python
    def dfs(graph, x, n, path, result):
        if x == n:
            result.append(path.copy())
            return
        for i in range(1, n + 1):
            if graph[x][i] == 1:
                path.append(i)
                dfs(graph, i, n, path, result)
                path.pop()

    def main():
        n, m = map(int, input().split())
        graph = [[0] * (n + 1) for _ in range(n + 1)]

        for _ in range(m):
            s, t = map(int, input().split())
            graph[s][t] = 1

        result = []
        dfs(graph, 1, n, [1], result)

        if not result:
            print(-1)
        else:
            for path in result:
                print(' '.join(map(str, path)))

    if __name__ == "__main__":
        main()
    
```

## [广搜理论基础](https://programmercarl.com/kamacoder/%E5%9B%BE%E8%AE%BA%E5%B9%BF%E6%90%9C%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)