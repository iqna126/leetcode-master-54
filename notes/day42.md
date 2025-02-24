# 第九章 动态规划part05

今日任务： 完全背包， 518.零钱兑换II， 377.组合总和Ⅳ， 70.爬楼梯（进阶）

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## [完全背包， 卡码网52. 携带研究材料](https://kamacoder.com/problempage.php?pid=1052)
```python
    def knapsack(n, bag_weight, weight, value):
        dp = [[0] * (bag_weight + 1) for _ in range(n)]

        # 初始化
        for j in range(weight[0], bag_weight + 1):
            dp[0][j] = dp[0][j - weight[0]] + value[0]

        # 动态规划
        for i in range(1, n):
            for j in range(bag_weight + 1):
                if j < weight[i]:
                    dp[i][j] = dp[i - 1][j]
                else:
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - weight[i]] + value[i])

        return dp[n - 1][bag_weight]

    # 输入
    n, bag_weight = map(int, input().split())
    weight = []
    value = []
    for _ in range(n):
        w, v = map(int, input().split())
        weight.append(w)
        value.append(v)

    # 输出结果
    print(knapsack(n, bag_weight, weight, value))
   
```

## 518.[零钱兑换II](https://leetcode.com/problems/coin-change-ii/)
```python
    class Solution(object):
        def change(self, amount, coins):
            """
            :type amount: int
            :type coins: List[int]
            :rtype: int
            """
            dp = [0] * (amount+1)
            dp[0] = 1
            for coin in coins:
                for j in range(coin,amount+1):
                    dp[j] += dp[j-coin]
            return dp[amount]

```

## 377.[组合总和Ⅳ](https://leetcode.com/problems/combination-sum-iv/)
```python
    class Solution(object):
        def combinationSum4(self, nums, target):
            """
            :type nums: List[int]
            :type target: int
            :rtype: int
            """
            # 排列的顺序 外层遍历背包，内层遍历物品
            dp = [0] * (target+1)
            dp[0] = 1
            for j in range(1, target+1):
                for num in nums:
                    if j-num >= 0:
                        dp[j] += dp[j-num]
            return dp[target]

```

## 70.[爬楼梯（进阶）](https://leetcode.com/problems/climbing-stairs/)
```python
    class Solution(object):
        def climbStairs(self, n):
            """
            :type n: int
            :rtype: int
            """
            dp = [0]*(n+1) # 背包总容量
            dp[0] = 1 
            # 排列题，注意循环顺序，背包在外物品在内
            for j in range(1,n+1):
                for i in range(1,3):
                    if j>=i:
                        dp[j] += dp[j-i] # 这里i就是重量而非index
            return dp[n]

            
            

```