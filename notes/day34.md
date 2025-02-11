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
            
  
            
```

## 406.[根据身高重建队列](https://leetcode.com/problems/queue-reconstruction-by-height/)
```python
    class Solution(object):
        def reconstructQueue(self, people):
            """
            :type people: List[List[int]]
            :rtype: List[List[int]]
            """
            
```