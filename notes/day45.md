# 第九章 动态规划part08

今日任务： 121.买卖股票的最佳时机， 122.买卖股票的最佳时机II， 123.买卖股票的最佳时机III

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 121.[买卖股票的最佳时机](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
贪心解法
```python
    class Solution(object):
        def maxProfit(self, prices):
            """
            :type prices: List[int]
            :rtype: int
            """
            low = float("inf")
            result = 0
            for i in range(len(prices)):
                low = min(low, prices[i]) #取最左最小价格
                result = max(result, prices[i] - low) #直接取最大区间利润
            return result

```
dp解法
```python
    class Solution(object):
        def maxProfit(self, prices):
            """
            :type prices: List[int]
            :rtype: int
            """
            if len(prices) == 0: 
                return 0
            dp = [[0] * 2 for _ in range(len(prices))]
            dp[0][0] = -prices[0]
            dp[0][1] = 0
            for i in range(1, len(prices)):
                dp[i][0] = max(dp[i-1][0], -prices[i])
                dp[i][1] = max(dp[i-1][0]+prices[i], dp[i-1][1])
            return dp[-1][1]
 
```

## 122.[买卖股票的最佳时机II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)
```python
    class Solution(object):
        def maxProfit(self, prices):
            """
            :type prices: List[int]
            :rtype: int
            """
            if len(prices) == 0: 
                return 0
            dp = [[0] * 2 for _ in range(len(prices))]
            dp[0][0] = -prices[0]
            dp[0][1] = 0
            for i in range(1, len(prices)):
                dp[i][0] = max(dp[i-1][0], dp[i-1][1]-prices[i])
                dp[i][1] = max(dp[i-1][0]+prices[i], dp[i-1][1])
            return dp[-1][1]
            
        
```

## 123.[买卖股票的最佳时机III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)
```python
    class Solution(object):
        def maxProfit(self, prices):
            """
            :type prices: List[int]
            :rtype: int
            """
            if len(prices) == 0:
                return 0
            dp = [[0] * 5 for _ in range(len(prices))]
            dp[0][1] = -prices[0]
            dp[0][3] = -prices[0]
            for i in range(1, len(prices)):
                # dp[i][0] = dp[i-1][0]
                dp[i][1] = max(dp[i-1][1], dp[i-1][0] - prices[i])
                dp[i][2] = max(dp[i-1][2], dp[i-1][1] + prices[i])
                dp[i][3] = max(dp[i-1][3], dp[i-1][2] - prices[i])
                dp[i][4] = max(dp[i-1][4], dp[i-1][3] + prices[i])
            return dp[-1][4]
                      
        
```