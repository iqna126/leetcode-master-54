# 第九章 动态规划part02

今日任务： 62.不同路径， 63.不同路径II，
附加任务： 343.整数拆分， 96.不同的二叉搜索树
 
文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 62.[不同路径](https://leetcode.com/problems/unique-paths/)
```python
    class Solution(object):
        def uniquePaths(self, m, n):
            """
            :type m: int
            :type n: int
            :rtype: int
            """
            dp = [[0 for _ in range(n)] for _ in range(m)]
            for i in range(m):
                dp[i][0] = 1
            for i in range(n):
                dp[0][i] = 1
            for i in range(1, m):
                for j in range(1, n):
                    dp[i][j] = dp[i-1][j] + dp[i][j-1]
            return dp[m-1][n-1]
            

```

## 63.[不同路径II](https://leetcode.com/problems/unique-paths-ii/)
```python
    class Solution(object):
        def uniquePathsWithObstacles(self, obstacleGrid):
            """
            :type obstacleGrid: List[List[int]]
            :rtype: int
            """
            m = len(obstacleGrid)
            n = len(obstacleGrid[0])
            if obstacleGrid[m - 1][n - 1] == 1 or obstacleGrid[0][0] == 1:
                return 0
            dp = [[0 for _ in range(n)] for _ in range(m)]
            
            dp[0][0] = 1 if obstacleGrid[0][0] == 0 else 0
            for i in range(1, m):
                if obstacleGrid[i][0] == 0:
                    dp[i][0] = dp[i - 1][0]
            
            for j in range(1, n):
                if obstacleGrid[0][j] == 0:
                    dp[0][j] = dp[0][j - 1]

            for i in range(1, m):
                for j in range(1, n):
                    if obstacleGrid[i][j] == 1:
                        continue
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
            
            return dp[m - 1][n - 1] 

```

## 343.[整数拆分](https://leetcode.com/problems/integer-break/)
```python
    class Solution(object):
        def integerBreak(self, n):
            """
            :type n: int
            :rtype: int
            """
            

```

## 96.[不同的二叉搜索树](https://leetcode.com/problems/unique-binary-search-trees/)
```python
    class Solution(object):
        def numTrees(self, n):
            """
            :type n: int
            :rtype: int
            """
            

```