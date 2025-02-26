# 第九章 动态规划part10

今日任务： 300.最长递增子序列， 674.最长连续递增序列， 718.最长重复子数组

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 300.[最长递增子序列](https://leetcode.com/problems/longest-increasing-subsequence/)
```python
    class Solution(object):
        def lengthOfLIS(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            if len(nums) <=1:
                return len(nums)
            dp = [1] * len(nums)
            res = 1
            for i in range(1,len(nums)):
                for j in range(i):
                    if nums[j] < nums[i]:
                        dp[i] = max(dp[i],dp[j]+1)
                res = max(res, dp[i])
            return res 
                
   
```

## 674.[最长连续递增序列](https://leetcode.com/problems/longest-continuous-increasing-subsequence/)
```python
    class Solution(object):
        def findLengthOfLCIS(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            if len(nums) <=1:
                return len(nums)
            dp = [1] * len(nums)
            res = 1
            for i in range(len(nums)-1):
                if nums[i] < nums[i+1]:
                        dp[i+1] = dp[i]+1
                res = max(res, dp[i+1])
            return res 

```

## 718.[最长重复子数组](https://leetcode.com/problems/maximum-length-of-repeated-subarray/)
```python
    class Solution(object):
        def findLength(self, nums1, nums2):
            """
            :type nums1: List[int]
            :type nums2: List[int]
            :rtype: int
            """
            dp = [[0] * (len(nums2) + 1) for _ in range(len(nums1) + 1)]
            # 记录最长公共子数组的长度
            result = 0

            # 遍历数组 nums1
            for i in range(1, len(nums1) + 1):
                # 遍历数组 nums2
                for j in range(1, len(nums2) + 1):
                    # 如果 nums1[i-1] 和 nums2[j-1] 相等
                    if nums1[i - 1] == nums2[j - 1]:
                        # 在当前位置上的最长公共子数组长度为前一个位置上的长度加一
                        dp[i][j] = dp[i - 1][j - 1] + 1
                    # 更新最长公共子数组的长度
                    if dp[i][j] > result:
                        result = dp[i][j]

            # 返回最长公共子数组的长度
            return result
            
            
   
```