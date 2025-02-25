# 第九章 动态规划part11

今日任务： 1143.最长公共子序列， 1035.不相交的线， 53.最大子序和， 392.判断子序列

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 1143.[最长公共子序列](https://leetcode.com/problems/longest-common-subsequence/)
```python
    class Solution(object):
        def longestCommonSubsequence(self, text1, text2):
            """
            :type text1: str
            :type text2: str
            :rtype: int
            """
            dp = [[0] * (len(text2)+1) for _ in range(len(text1)+1)] # 注意初始化数组的顺序 dp[i][j]的定义是i-1，j-1为下标的最大公共子序列
            for i in range(1,len(text1)+1):
                for j in range(1, len(text2)+1):
                    if text1[i-1] == text2[j-1]:
                        dp[i][j] = dp[i-1][j-1] + 1
                    else:
                        dp[i][j] = max(dp[i][j-1], dp[i-1][j])
            return dp[len(text1)][len(text2)]
            
            
    

```

## 1035.[不相交的线](https://leetcode.com/problems/uncrossed-lines/)
```python
    class Solution(object):
        def maxUncrossedLines(self, nums1, nums2):
            """
            :type nums1: List[int]
            :type nums2: List[int]
            :rtype: int
            """
            dp = [[0] * (len(nums2)+1) for _ in range(len(nums1)+1)]
            for i in range(1,len(nums1)+1):
                for j in range(1, len(nums2)+1):
                    if nums1[i-1] == nums2[j-1]:
                        dp[i][j] = dp[i-1][j-1] + 1
                        # print("i: ", i, " j: ", j, " dp[i][j]: ", dp[i][j])
                    else:
                        dp[i][j] = max(dp[i-1][j], dp[i][j-1])
                        # print("i: ", i, " j: ", j, " dp[i][j]: ", dp[i][j])
            return dp[len(nums1)][len(nums2)]
            

```

## 53.[最大子序和](https://leetcode.com/problems/maximum-subarray/description/)
```python
    class Solution(object):
        def maxSubArray(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            # dp解法
            dp = [0] * len(nums)
            dp[0] = nums[0]
            res = nums[0]
            for i in range(1,len(nums)):
                dp[i] = max(nums[i], dp[i-1]+nums[i])
                # print("i: ", i, " dp[i]: ", dp[i])
                res = max(res, dp[i])
            return res

```

## 392.[判断子序列](https://leetcode.com/problems/is-subsequence/)
```python
    class Solution(object):
        def isSubsequence(self, s, t):
            """
            :type s: str
            :type t: str
            :rtype: bool
            """
            dp = [[0] * (len(t)+1) for _ in range(len(s)+1)]
            for i in range(1,len(s)+1):
                for j in range(1,len(t)+1):
                    if s[i-1] == t[j-1]:
                        dp[i][j] = dp[i-1][j-1] + 1
                    else:
                        dp[i][j] = dp[i][j-1]    
            if dp[len(s)][len(t)] == len(s):
                return True
            else:
                return False     
                
    

```
