# 第八章 贪心算法 part01

今日任务： 理论基础， 455.分发饼干， 376.摆动序列， 53.最大子序和

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## [理论基础](https://programmercarl.com/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
贪心的本质是选择每一阶段的局部最优，从而达到全局最优。


## 455.[分发饼干](https://leetcode.com/problems/assign-cookies/)
```python
    class Solution(object):
        def findContentChildren(self, g, s):
            """
            :type g: List[int]
            :type s: List[int]
            :rtype: int
            """
            g.sort()  
            s.sort() 
            res = 0
            index = len(s) - 1  
            for i in range(len(g)-1, -1, -1): 
                if index >= 0 and s[index] >= g[i]: 
                    result += 1
                    index -= 1
            return result       
        
            
```

## 376.[摆动序列](https://leetcode.com/problems/wiggle-subsequence/)
```python
    class Solution(object):
        def wiggleMaxLength(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            if len(nums)<=1:
                return len(nums)
            res = 1
            curDiff = 0
            preDiff = 0
            for i in range(len(nums)-1):
                curDiff = nums[i+1] - nums[i]
                if (preDiff <= 0 and curDiff >0) or (preDiff >= 0 and curDiff<0):
                    res += 1 
                    preDiff = curDiff
            return res 
                
            
```

## 53.[最大子序和](https://leetcode.com/problems/maximum-subarray/)
```python
class Solution(object):
        def maxSubArray(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            result = float('-inf')  # 初始化结果为负无穷大
            count = 0
            for i in range(len(nums)):
                count += nums[i]
                if count > result:  # 取区间累计的最大值（相当于不断确定最大子序终止位置）
                    result = count
                if count <= 0:  # 相当于重置最大子序起始位置，因为遇到负数一定是拉低总和
                    count = 0
            return result
                
            
```