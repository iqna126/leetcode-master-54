# 第九章 动态规划part13

今日任务： 647.回文子串， 516.最长回文子序列， 动态规划总结篇

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 647.[回文子串](https://leetcode.com/problems/palindromic-substrings/)
```python
    class Solution(object):
        def countSubstrings(self, s):
            """
            :type s: str
            :rtype: int
            """
            # whether s[i,j] is a palindromic substring
            dp = [[False] * len(s) for _ in range(len(s))]
            res = 0 
            for i in range(len(s)-1,-1,-1):
                for j in range(i,len(s)):
                    if s[i] == s[j]:
                        if j-i<=1:
                            res +=1
                            dp[i][j] = True
                        elif dp[i+1][j-1]:
                            res += 1
                            dp[i][j] = True
            return res
            

```

## 516.[最长回文子序列](https://leetcode.com/problems/longest-palindromic-subsequence/)
```python
    class Solution(object):
        def longestPalindromeSubseq(self, s):
            """
            :type s: str
            :rtype: int
            """
            dp = [[0] * len(s) for _ in range(len(s))]
            for i in range(len(s)):
                dp[i][i] = 1
            for i in range(len(s)-1, -1, -1):
                for j in range(i+1, len(s)):
                    if s[i] == s[j]:
                        dp[i][j] = dp[i+1][j-1] + 2
                    else:
                        dp[i][j] = max(dp[i+1][j], dp[i][j-1])
            return dp[0][-1]
        

```

## [动态规划总结篇](https://programmercarl.com/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E6%80%BB%E7%BB%93%E7%AF%87.html#%E5%8A%A8%E8%A7%84%E7%BB%93%E6%9D%9F%E8%AF%AD)
![总结图来自代码随想录知识星球成员： 青](https://kstar-1253855093.cos.ap-nanjing.myqcloud.com/baguwenpdf/_%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE_%E9%9D%92.png "总结")
