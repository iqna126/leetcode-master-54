# 第九章 动态规划part03

今日任务： 01.背包问题 二维， 01.背包问题 一维， 416.分割等和子集 

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 01.[背包问题 二维， 卡码网46. 携带研究材料](https://kamacoder.com/problempage.php?pid=1046)
```python
    n, bagweight = map(int, input().split())
    weight = list(map(int, input().split()))
    value = list(map(int, input().split()))

    dp = [[0] * (bagweight + 1) for _ in range(n)]

    for j in range(weight[0], bagweight + 1):
        dp[0][j] = value[0]

    for i in range(1, n):
        for j in range(bagweight + 1):
            if j < weight[i]:
                dp[i][j] = dp[i - 1][j]
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i])

    print(dp[n - 1][bagweight])
```

## 01.[背包问题 一维， 卡码网46. 携带研究材料](https://kamacoder.com/problempage.php?pid=1046)
```python
    n, bagweight = map(int, input().split())
    weight = list(map(int, input().split()))
    value = list(map(int, input().split()))

    dp = [0] * (bagweight + 1)  # 创建一个动态规划数组dp，初始值为0
    dp[0] = 0  # 初始化dp[0] = 0,背包容量为0，价值最大为0
    for i in range(n):  # 应该先遍历物品，如果遍历背包容量放在上一层，那么每个dp[j]就只会放入一个物品
        for j in range(bagweight, weight[i]-1, -1):  # 倒序遍历背包容量是为了保证物品i只被放入一次
            dp[j] = max(dp[j], dp[j - weight[i]] + value[i])

    print(dp[bagweight])

```

## 416.[分割等和子集](https://leetcode.com/problems/partition-equal-subset-sum/)
```python
    class Solution(object):
        def canPartition(self, nums):
            """
            :type nums: List[int]
            :rtype: bool
            """
            if sum(nums) % 2 != 0:
                return False
            target = sum(nums) // 2
            dp = [0] * (target + 1)
            for num in nums:
                for j in range(target, num-1, -1):
                    dp[j] = max(dp[j], dp[j-num] + num)
            return dp[-1] == target


```