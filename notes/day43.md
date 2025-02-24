# 第九章 动态规划part06

今日任务： 322.零钱兑换， 279.完全平方数， 139.单词拆分， 多重背包问题， 背包问题总结

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 322.[零钱兑换](https://leetcode.com/problems/coin-change/)
```python
    class Solution(object):
        def coinChange(self, coins, amount):
            """
            :type coins: List[int]
            :type amount: int
            :rtype: int
            """
            dp = [float('inf')] * (amount+1)
            dp[0] = 0
            for coin in coins:
                for j in range(coin,amount+1):
                    if dp[j-coin] != float('inf'): # j-coin凑不出来，就还是初始值inf，于是跳过
                        dp[j] = min(dp[j], dp[j-coin]+1)
            if dp[amount] == float('inf'):
                return -1
            else:
                return dp[amount]
            

```

## 279.[完全平方数](https://leetcode.com/problems/perfect-squares/)
```python
    class Solution(object):
        def numSquares(self, n):
            """
            :type n: int
            :rtype: int
            """
            dp = [float('inf')] * (n+1)
            dp[0] = 0
            for i in range(1,int(n**0.5)+1):
                for j in range(i*i, n+1):
                    dp[j] = min(dp[j-i*i]+1, dp[j])
            return dp[n]

            

```

## 139.[单词拆分](https://leetcode.com/problems/word-break/)
```python
    class Solution(object):
        def wordBreak(self, s, wordDict):
            """
            :type s: str
            :type wordDict: List[str]
            :rtype: bool
            """
            wordSet = set(wordDict)
            n = len(s)
            dp = [False] * (n + 1)  # dp[i] 表示字符串的前 i 个字符是否可以被拆分成单词
            dp[0] = True  # 初始状态，空字符串可以被拆分成单词

            for i in range(1, n + 1): # 遍历背包
                for j in range(i): # 遍历单词
                    if dp[j] and s[j:i] in wordSet:
                        dp[i] = True  # 如果 s[0:j] 可以被拆分成单词，并且 s[j:i] 在单词集合中存在，则 s[0:i] 可以被拆分成单词
                        break

            return dp[n]
                

```


## [多重背包问题, 56. 携带矿石资源（第八期模拟笔试）](https://kamacoder.com/problempage.php?pid=1066)
```python
    C, N = input().split(" ")
    C, N = int(C), int(N)

    # value数组需要判断一下非空不然过不了
    weights = [int(x) for x in input().split(" ")]
    values = [int(x) for x in input().split(" ") if x]
    nums = [int(x) for x in input().split(" ")]

    dp = [0] * (C + 1)
    # 遍历背包容量
    for i in range(N):
        for j in range(C, weights[i] - 1, -1):
            for k in range(1, nums[i] + 1):
                # 遍历 k，如果已经大于背包容量直接跳出循环
                if k * weights[i] > j:
                    break
                dp[j] = max(dp[j], dp[j - weights[i] * k] + values[i] * k) 
    print(dp[-1])

```


## [背包问题总结](https://programmercarl.com/%E8%83%8C%E5%8C%85%E6%80%BB%E7%BB%93%E7%AF%87.html)
### 动规五部曲！
1. 确定dp数组（dp table）以及下标的含义
2. 确定递推公式
3. dp数组如何初始化
4. 确定遍历顺序
5. 举例推导dp数组

### 背包种类：
1. 01背包： 有n件物品和一个最多能背重量为w的背包。第i件物品的重量是weight[i]，得到的价值是value[i] 。**每件物品只能用一次**，求解将哪些物品装入背包里物品价值总和最大。
2. 完全背包： 有n件物品和一个最多能背重量为w的背包。第i件物品的重量是weight[i]，得到的价值是value[i] 。**每件物品都有无限个**（也就是可以放入背包多次），求解将哪些物品装入背包里物品价值总和最大。    
如果求组合数就是外层for循环遍历物品，内层for遍历背包。  
如果求排列数就是外层for遍历背包，内层for循环遍历物品。
3. 多重背包:： 有n种物品和一个容量为w的背包。**第i种物品最多有M[i]件可用**，每件耗费的空间是weight[i] ，价值是value[i] 。求解将哪些物品装入背包可使这些物品的耗费的空间 总和不超过背包容量，且价值总和最大。**但是可以把M[i]拆开将问题转化成01背包**



![总结图来自代码随想录知识星球成员：海螺人](https://code-thinking-1253855093.file.myqcloud.com/pics/%E8%83%8C%E5%8C%85%E9%97%AE%E9%A2%981.jpeg "总结")
