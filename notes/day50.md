# 第九章 动态规划part12

今日任务： 115.不同的子序列， 583.两个字符串的删除操作， 72.编辑距离， 编辑距离总结

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 115.[不同的子序列](https://leetcode.com/problems/distinct-subsequences/)
```python
    class Solution(object):
        def numDistinct(self, s, t):
            """
            :type s: str
            :type t: str
            :rtype: int
            """
            # dp数组的定义： 以i-1结尾的s中有以j-1结尾的t的个数
            dp = [[0] * (len(t)+1) for _ in range(len(s)+1)]
            for i in range(len(s)+1):
                dp[i][0] = 1
            for i in range(1,len(s)+1):
                for j in range(1,len(t)+1):
                    if s[i-1] == t[j-1]:
                        dp[i][j] = dp[i-1][j-1] + dp[i-1][j]
                    else:
                        dp[i][j] = dp[i-1][j]  
            return dp[len(s)][len(t)]
            
            
    

```

## 583.[两个字符串的删除操作](https://leetcode.com/problems/delete-operation-for-two-strings/)
```python
    class Solution(object):
        def minDistance(self, word1, word2):
            """
            :type word1: str
            :type word2: str
            :rtype: int
            """
            dp = [[0] * (len(word2)+1) for _ in range(len(word1)+1)]
            for i in range(1, len(word1)+1):
                for j in range(1, len(word2)+1):
                    if word1[i-1] == word2[j-1]:
                        dp[i][j] = dp[i-1][j-1] + 1
                    else: 
                        dp[i][j] = max(dp[i-1][j],dp[i][j-1])
            return len(word1)+len(word2)-dp[len(word1)][len(word2)]- dp[len(word1)][len(word2)]
                

```

## 72.[编辑距离](https://leetcode.com/problems/edit-distance/)
```python
    class Solution(object):
        def minDistance(self, word1, word2):
            """
            :type word1: str
            :type word2: str
            :rtype: int
            """
            dp = [[0] * (len(word2)+1) for _ in range(len(word1)+1)]
            for i in range(len(word1)+1):
                dp[i][0] = i
            for j in range(len(word2)+1):
                dp[0][j] = j
            for i in range(1, len(word1)+1):
                for j in range(1, len(word2)+1):
                    if  word1[i-1] == word2[j-1]:
                        dp[i][j] = dp[i-1][j-1]
                    else:
                        dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])+1
            return dp[len(word1)][len(word2)]        
            

```

## [编辑距离总结](https://programmercarl.com/%E4%B8%BA%E4%BA%86%E7%BB%9D%E6%9D%80%E7%BC%96%E8%BE%91%E8%B7%9D%E7%A6%BB%EF%BC%8C%E5%8D%A1%E5%B0%94%E5%81%9A%E4%BA%86%E4%B8%89%E6%AD%A5%E9%93%BA%E5%9E%AB.html)
用动规五部曲！