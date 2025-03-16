# 第十一章 图论part04

今日任务： 110.字符串接龙， 105.有向图的完全可达性， 106.岛屿的周长

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 卡码网110.[字符串接龙](https://kamacoder.com/problempage.php?pid=1183)
```python
def judge(s1,s2):
    count=0
    for i in range(len(s1)):
        if s1[i]!=s2[i]:
            count+=1
    return count==1

if __name__=='__main__':
    n=int(input())
    beginstr,endstr=map(str,input().split())
    if beginstr==endstr:
        print(0)
        exit()
    strlist=[]
    for i in range(n):
        strlist.append(input())
    
    # use bfs
    visit=[False for i in range(n)]
    queue=[[beginstr,1]]
    while queue:
        str,step=queue.pop(0)
        if judge(str,endstr):
            print(step+1)
            exit()
        for i in range(n):
            if visit[i]==False and judge(strlist[i],str):
                visit[i]=True
                queue.append([strlist[i],step+1])
    print(0)
   
```

## 卡码网105.[有向图的完全可达性](https://kamacoder.com/problempage.php?pid=1177)
DFS
```python
def dfs(graph, key, visited):
    for neighbor in graph[key]:
        if not visited[neighbor]:  # Check if the next node is not visited
            visited[neighbor] = True
            dfs(graph, neighbor, visited)

def main():
    import sys
    input = sys.stdin.read
    data = input().split()

    n = int(data[0])
    m = int(data[1])
    
    graph = [[] for _ in range(n + 1)]
    index = 2
    for _ in range(m):
        s = int(data[index])
        t = int(data[index + 1])
        graph[s].append(t)
        index += 2

    visited = [False] * (n + 1)
    visited[1] = True  # Process node 1 beforehand
    dfs(graph, 1, visited)

    for i in range(1, n + 1):
        if not visited[i]:
            print(-1)
            return
    
    print(1)

if __name__ == "__main__":
    main()

   
```

## 卡码网106.[岛屿的周长](https://kamacoder.com/problempage.php?pid=1178)
```python
def main():
    import sys
    input = sys.stdin.read
    data = input().split()
    
    # 读取 n 和 m
    n = int(data[0])
    m = int(data[1])
    
    # 初始化 grid
    grid = []
    index = 2
    for i in range(n):
        grid.append([int(data[index + j]) for j in range(m)])
        index += m
    
    sum_land = 0    # 陆地数量
    cover = 0       # 相邻数量

    for i in range(n):
        for j in range(m):
            if grid[i][j] == 1:
                sum_land += 1
                # 统计上边相邻陆地
                if i - 1 >= 0 and grid[i - 1][j] == 1:
                    cover += 1
                # 统计左边相邻陆地
                if j - 1 >= 0 and grid[i][j - 1] == 1:
                    cover += 1
                # 不统计下边和右边，避免重复计算
    
    result = sum_land * 4 - cover * 2
    print(result)

if __name__ == "__main__":
    main()

   
```