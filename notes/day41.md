# 第九章 动态规划part04

今日任务： 1049.最后一块石头的重量II， 494.目标和， 474.一和零

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 1049.[最后一块石头的重量II](https://leetcode.com/problems/last-stone-weight-ii/)
```python
    class Solution(object):
        def lastStoneWeightII(self, stones):
            """
            :type stones: List[int]
            :rtype: int
            """
            target = sum(stones) // 2
            dp = [0] * (target + 1)
            for stone in stones:
                for j in range(target, stone-1, -1):
                    dp[j] = max(dp[j], dp[j-stone] + stone)
            return sum(stones)-dp[-1]-dp[-1]

            

```

## 494.[目标和](https://leetcode.com/problems/target-sum/)
```python
    class Solution(object):
        def findTargetSumWays(self, nums, target):
            """
            :type nums: List[int]
            :type target: int
            :rtype: int
            """
            total_sum  = sum(nums)

            if (total_sum+target) % 2 != 0:
                return 0
            if abs(target) > total_sum:
                return 0

            positive_sum = (total_sum+target) //2

            dp = [0] * (positive_sum +1) 

            dp[0] = 1

            for num in nums:
                for j in range(positive_sum, num-1, -1):
                    dp[j] += dp[j-num]
            
            return dp[positive_sum]
```

## 474.[一和零](https://leetcode.com/problems/ones-and-zeroes/)
```python
    class Solution(object):
        def findMaxForm(self, strs, m, n):
            """
            :type strs: List[str]
            :type m: int
            :type n: int
            :rtype: int
            """
            dp = [[0] * (n + 1) for _ in range(m + 1)]  # 创建二维动态规划数组，初始化为0
            for s in strs:  # 遍历物品
                zeroNum = s.count('0')  # 统计0的个数
                oneNum = len(s) - zeroNum  # 统计1的个数
                for i in range(m, zeroNum - 1, -1):  # 遍历背包容量且从后向前遍历
                    for j in range(n, oneNum - 1, -1):
                        dp[i][j] = max(dp[i][j], dp[i - zeroNum][j - oneNum] + 1)  # 状态转移方程
            return dp[m][n]
            
```