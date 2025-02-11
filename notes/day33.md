# 第八章 贪心算法 part02

今日任务： 122.买卖股票的最佳时机II， 55.跳跃游戏， 45.跳跃游戏II， 1005.K次取反后最大化的数组和

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 122.[买卖股票的最佳时机II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)
```python
    class Solution(object):
        def maxProfit(self, prices):
            """
            :type prices: List[int]
            :rtype: int
            """
            res = 0 
            cur = 0
            for i in range(len(prices)-1):
                cur = prices[i+1] - prices[i]
                if cur >=0:
                    res += cur
                i +=1
            return res
            
            
```

## 55.[跳跃游戏](https://leetcode.com/problems/jump-game/)
```python
    class Solution(object):
        def canJump(self, nums):
            """
            :type nums: List[int]
            :rtype: bool
            """
            cover = 0
            if len(nums) == 1: return True
            i = 0
            while i <= cover: # 才能往前移动
                cover = max(i + nums[i], cover)
                if cover >= len(nums) - 1: return True
                i += 1
            return False
            
                
```

## 45.[跳跃游戏II](https://leetcode.com/problems/jump-game-ii/)
```python
    class Solution(object):
        def jump(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            if len(nums) == 1: 
                return 0
            
            cur_distance = 0   
            next_distance = 0 
            res = 0
            
            for i in range(len(nums)):
                next_distance = max(nums[i] + i, next_distance)  # 记录已经走过的可以达到最长的next_distance
                if i == cur_distance: # 走到当前可以达到的最长距离但依旧没有到达终点时才一定需要下一步
                    res += 1  
                    cur_distance = next_distance  
                    if next_distance >= len(nums) - 1:
                        break
            
            return res
            
            
```

## 1005.[K次取反后最大化的数组和](https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/)
```python
    class Solution(object):
        def largestSumAfterKNegations(self, nums, k):
            """
            :type nums: List[int]
            :type k: int
            :rtype: int
            """
            nums.sort(key=lambda x: abs(x), reverse=True)

            for i in range(len(nums)):  
                if nums[i] < 0 and k > 0:
                    nums[i] *= -1
                    k -= 1

            if k % 2 == 1: 
                nums[-1] *= -1

            return sum(nums)
                
            
```