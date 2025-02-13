# 第八章 贪心算法 part03

今日任务： 134.加油站， 135.分发糖果， 860.柠檬水找零， 406.根据身高重建队列

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 134.[加油站](https://leetcode.com/problems/gas-station/)
```python
    class Solution(object):
        def canCompleteCircuit(self, gas, cost):
            """
            :type gas: List[int]
            :type cost: List[int]
            :rtype: int
            """
            curSum = 0  # 当前累计的剩余油量
            totalSum = 0  # 总剩余油量
            position = 0  
            
            for i in range(len(gas)):
                curSum += gas[i] - cost[i]
                totalSum += gas[i] - cost[i]
                
                if curSum < 0:  # 当前累计剩余油量curSum小于0
                    position = i + 1  # 起始位置更新为i+1
                    curSum = 0  # curSum重新从0开始累计
            
            if totalSum < 0:
                return -1  # 总剩余油量totalSum小于0，说明无法环绕一圈
            return position
            
```

## 135.[分发糖果](https://leetcode.com/problems/candy/)
```python
    class Solution(object):
        def candy(self, ratings):
            """
            :type ratings: List[int]
            :rtype: int
            """
            n = len(ratings)
            candies = [1] * n  
            
            # Forward pass: compare with left neighbor
            for i in range(1, n):
                if ratings[i] > ratings[i-1]:
                    candies[i] = candies[i-1] + 1
            
            # Backward pass: compare with right neighbor
            for i in range(n-2, -1, -1):
                if ratings[i] > ratings[i+1]:
                    candies[i] = max(candies[i], candies[i+1] + 1)
            
            return sum(candies)
    
            
```

## 860.[柠檬水找零](https://leetcode.com/problems/lemonade-change/)
```python
    class Solution(object):
        def lemonadeChange(self, bills):
            """
            :type bills: List[int]
            :rtype: bool
            """
            n_5 = 0 
            n_10 = 0
            for i in range(len(bills)):
                if bills[i] == 5:
                    n_5 += 1
                elif bills[i] == 10 and n_5 < 1:
                    return False
                elif bills[i] == 10:
                    n_10 += 1
                    n_5 -= 1
                elif bills[i] == 20:
                    if (n_10 < 1 and n_5<3) or n_5<1:
                        return False
                    if n_10 != 0:
                        n_10 -= 1
                        n_5 -= 1
                    else:
                        n_5 -=3
            return True

            
```

## 406.[根据身高重建队列](https://leetcode.com/problems/queue-reconstruction-by-height/)
```python
    class Solution(object):
        def reconstructQueue(self, people):
            """
            :type people: List[List[int]]
            :rtype: List[List[int]]
            """
            # 先按照h维度的身高顺序从高到低排序。确定第一个维度
            # lambda返回的是一个元组：当-x[0](维度h）相同时，再根据x[1]（维度k）从小到大排序
            people.sort(key=lambda x: (-x[0], x[1]))
            que = []
        
            # 根据每个元素的第二个维度k，贪心算法，进行插入
            # people已经排序过了：同一高度时k值小的排前面。
            for p in people:
                que.insert(p[1], p)
            return que
            
```