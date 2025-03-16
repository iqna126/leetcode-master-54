# 第十一章 图论part06

今日任务： 108.冗余连接， 109.冗余连接II  

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 卡码网108.[冗余连接](https://kamacoder.com/problempage.php?pid=1181)
```python
father = list()

def find(u):
    if u == father[u]:
        return u
    else:
        father[u] = find(father[u])
        return father[u]
        
def is_same(u, v):
    u = find(u)
    v = find(v)
    return u == v
    
def join(u, v):
    u = find(u)
    v = find(v)
    if u != v:
        father[u] = v
        
if __name__ == "__main__":
    n = int(input())
    for i in range(n + 1):
        father.append(i)
  
    result = None
    for i in range(n):
        s, t = map(int, input().split())
        if is_same(s, t):
            result = str(s) + ' ' + str(t)
        else:
            join(s, t)
 
    print(result)
   
```

## 卡码网109.[冗余连接II](https://kamacoder.com/problempage.php?pid=1182)
```python
from collections import defaultdict

father = list()


def find(u):
    if u == father[u]:
        return u
    else:
        father[u] = find(father[u])
        return father[u]
        
        
def is_same(u, v):
    u = find(u)
    v = find(v)
    return u == v
    
    
def join(u, v):
    u = find(u)
    v = find(v)
    if u != v:
        father[u] = v
    
    
def is_tree_after_remove_edge(edges, edge, n):
    global father 
    father = [i for i in range(n + 1)]
    
    for i in range(len(edges)):
        if i == edge:
            continue
        s, t = edges[i]
        if is_same(s, t): 
            return False
        else: 
            join(s, t)
    return True
    

def get_remove_edge(edges):
    global father
    father = [i for i in range(n + 1)]
    
    for s, t in edges:
        if is_same(s, t):
            print(s, t)
            return
        else:
            join(s, t)
        

if __name__ == "__main__":
    n = int(input())
    edges = list()
    in_degree = defaultdict(int)
    
    for i in range(n):
        s, t = map(int, input().split())
        in_degree[t] += 1
        edges.append([s, t])
        
    vec = list()
    for i in range(n - 1, -1, -1):
        if in_degree[edges[i][1]] == 2:
            vec.append(i)
            
    if len(vec) > 0:
        # 情況一
        if is_tree_after_remove_edge(edges, vec[0], n):
            print(edges[vec[0]][0], edges[vec[0]][1])
        # 情況二
        else:
            print(edges[vec[1]][0], edges[vec[1]][1])
    else:
        # 情況三
        get_remove_edge(edges)
   
```