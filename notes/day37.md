# 第九章 动态规划part01

今日任务： 理论基础， 509.斐波那契数， 70.爬楼梯， 746.使用最小花费爬楼梯
 
文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## [理论基础](https://programmercarl.com/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html#%E4%BB%80%E4%B9%88%E6%98%AF%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)
动态规划，英文：Dynamic Programming，简称DP，如果某一问题有很多重叠子问题，使用动态规划是最有效的。

所以动态规划中每一个状态一定是由上一个状态推导出来的，这一点就区分于贪心，贪心没有状态推导，而是从局部直接选最优的
对于动态规划问题，我将拆解为如下五步曲，这五步都搞清楚了，才能说把动态规划真的掌握了！

1. 确定dp数组（dp table）以及下标的含义
2. 确定递推公式
3. dp数组如何初始化
4. 确定遍历顺序
5. 举例推导dp数组

## 509.[斐波那契数](https://leetcode.com/problems/fibonacci-number/)
```python
    class Solution(object):
        def fib(self, n):
            """
            :type n: int
            :rtype: int
            """
            if n == 0:
                return 0
            # 确定 dp 数组
            dp = [0] * (n + 1)

            # 初始化 dp 数组
            dp[0] = 0
            dp[1] = 1

            # 确定遍历顺序: 由前向后。因为后面要用到前面的状态
            for i in range(2, n + 1):

                # 确定递归公式/状态转移公式
                dp[i] = dp[i - 1] + dp[i - 2]
            
            # 返回答案
            return dp[n]
    
```

## 70.[爬楼梯](https://leetcode.com/problems/climbing-stairs/)
```python
    class Solution(object):
        def climbStairs(self, n):
            """
            :type n: int
            :rtype: int
            """
            dp = [0] * (n+1)
            if n <= 1:
                return n
            else:
                dp[1] = 1
                dp[2] = 2
                for i in range(3,n+1):
                    dp[i] = dp[i-1]+dp[i-2]
                return dp[n]
                
   
```

## 746.[使用最小花费爬楼梯](https://leetcode.com/problems/min-cost-climbing-stairs/)
```python
    class Solution(object):
        def minCostClimbingStairs(self, cost):
            """
            :type cost: List[int]
            :rtype: int
            """
            dp = [0] * (len(cost) + 1)
            dp[0] = 0  
            dp[1] = 0 
            
            for i in range(2, len(cost) + 1):
                dp[i] = min(dp[i - 1] + cost[i - 1], dp[i - 2] + cost[i - 2])
            
            return dp[len(cost)] 
        
   
```