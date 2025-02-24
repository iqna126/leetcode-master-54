# 第九章 动态规划part09

今日任务： 188.买卖股票的最佳时机IV， 309.最佳买卖股票时机含冷冻期， 714.买卖股票的最佳时机含手续费， 股票总结

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 188.[买卖股票的最佳时机IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)
```python
    class Solution(object):
        def maxProfit(self, k, prices):
            """
            :type k: int
            :type prices: List[int]
            :rtype: int
            """
            if len(prices) == 0:
                return 0
            dp = [[0] * (2*k+1) for _ in range(len(prices))]
            for j in range(1, 2*k, 2):
                dp[0][j] = -prices[0]
            for i in range(1, len(prices)):
                for j in range(0, 2*k-1, 2):
                    dp[i][j+1] = max(dp[i-1][j+1], dp[i-1][j] - prices[i])
                    dp[i][j+2] = max(dp[i-1][j+2], dp[i-1][j+1] + prices[i])
            return dp[-1][2*k]
            
            
        
```

## 309.[最佳买卖股票时机含冷冻期](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)
```python
    class Solution(object):
        def maxProfit(self, prices):
            """
            :type prices: List[int]
            :rtype: int
            """
            n = len(prices)
            if n == 0:
                return 0
            dp = [[0] * 4 for _ in range(n)]  # 创建动态规划数组，4个状态分别表示持有股票、不持有股票且处于冷冻期、不持有股票且不处于冷冻期、不持有股票且当天卖出后处于冷冻期
            dp[0][0] = -prices[0]  # 初始状态：第一天持有股票的最大利润为买入股票的价格
            for i in range(1, n):
                dp[i][0] = max(dp[i-1][0], max(dp[i-1][3], dp[i-1][1]) - prices[i])  # 当前持有股票的最大利润等于前一天持有股票的最大利润或者前一天不持有股票且不处于冷冻期的最大利润减去当前股票的价格
                dp[i][1] = max(dp[i-1][1], dp[i-1][3])  # 当前不持有股票且处于冷冻期的最大利润等于前一天持有股票的最大利润加上当前股票的价格
                dp[i][2] = dp[i-1][0] + prices[i]  # 当前不持有股票且不处于冷冻期的最大利润等于前一天不持有股票的最大利润或者前一天处于冷冻期的最大利润
                dp[i][3] = dp[i-1][2]  # 当前不持有股票且当天卖出后处于冷冻期的最大利润等于前一天不持有股票且不处于冷冻期的最大利润
            return max(dp[n-1][3], dp[n-1][1], dp[n-1][2])  # 返回最后一天不持有股票的最大利润

            
            
        
```

## 714.[买卖股票的最佳时机含手续费](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)
```python
    class Solution(object):
        def maxProfit(self, prices, fee):
            """
            :type prices: List[int]
            :type fee: int
            :rtype: int
            """
            if len(prices) == 0: 
                return 0
            dp = [[0] * 2 for _ in range(len(prices))]
            dp[0][0] = -prices[0]-fee
            dp[0][1] = 0
            for i in range(1, len(prices)):
                dp[i][0] = max(dp[i-1][0], dp[i-1][1]-prices[i]-fee)
                dp[i][1] = max(dp[i-1][0]+prices[i], dp[i-1][1])
            return dp[-1][1]
            
        
```


## 股票问题总结
![总结图来自代码随想录知识星球](https://code-thinking.cdn.bcebos.com/pics/%E8%82%A1%E7%A5%A8%E9%97%AE%E9%A2%98%E6%80%BB%E7%BB%93.jpg "总结")
