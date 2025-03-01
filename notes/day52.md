# 第十章 单调栈part01

今日任务： 739.每日温度， 496.下一个更大元素I， 503.下一个更大元素II 

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 739.[每日温度](https://leetcode.com/problems/daily-temperatures/)
```python
    class Solution(object):
        def dailyTemperatures(self, temperatures):
            """
            :type temperatures: List[int]
            :rtype: List[int]
            """
            stack= [0]
            res = [0] * len(temperatures)
            for i in range(1,len(temperatures)):
                while len(stack) != 0 and temperatures[i]>temperatures[stack[-1]]:
                    res[stack[-1]] = i-stack[-1]
                    stack.pop()
                stack.append(i)
            return res 


        
```

## 496.[下一个更大元素I](https://leetcode.com/problems/next-greater-element-i/)
```python
    class Solution(object):
        def nextGreaterElement(self, nums1, nums2):
            """
            :type nums1: List[int]
            :type nums2: List[int]
            :rtype: List[int]
            """
            res = [-1] * len(nums1)
            nums2_stack = [0]
            for i in range(1,len(nums2)):
                while len(nums2_stack) != 0 and nums2[i] > nums2[nums2_stack[-1]]:
                    if nums2[nums2_stack[-1]] in nums1:
                        index = nums1.index(nums2[nums2_stack[-1]])
                        res[index] = nums2[i]
                    nums2_stack.pop()
                nums2_stack.append(i)
            return res
               
```

## 503.[下一个更大元素II](https://leetcode.com/problems/next-greater-element-ii/)
```python
    class Solution(object):
        def nextGreaterElements(self, nums):
            """
            :type nums: List[int]
            :rtype: List[int]
            """
            dp = [-1] * len(nums)
            stack = []
            for i in range(len(nums)*2):
                while(len(stack) != 0 and nums[i%len(nums)] > nums[stack[-1]]):
                        dp[stack[-1]] = nums[i%len(nums)]
                        stack.pop()
                stack.append(i%len(nums))
            return dp
```
