# 第十章 单调栈part02

今日任务： 42.接雨水， 84.柱状图中最大的矩形

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 42.[接雨水](https://leetcode.com/problems/trapping-rain-water/)
```python
    class Solution(object):
        def trap(self, height):
            """
            :type height: List[int]
            :rtype: int
            """
            if len(height) <= 2:
                return 0
            mono_stack = [0]
            res = 0
            for i in range(1,len(height)):
                while len(mono_stack)>=1 and height[i] > height[mono_stack[-1]]:
                    # print(mono_stack)
                    mid = mono_stack[-1]
                    mono_stack.pop()
                    # print("mono stack after pop: ", mono_stack)
                    if len(mono_stack) > 0:
                        h = (min(height[mono_stack[-1]], height[i])-height[mid])
                        # print("height: ", h)
                        w = (i-mono_stack[-1]-1)
                        # print("width: ", w)
                        res += h*w
                mono_stack.append(i)
            return res
        
```

## 84.[柱状图中最大的矩形](https://leetcode.com/problems/largest-rectangle-in-histogram/)
```python
    class Solution(object):
        def largestRectangleArea(self, heights):
            """
            :type heights: List[int]
            :rtype: int
            """
            # 输入数组首尾各补上一个0（与42.接雨水不同的是，本题原首尾的两个柱子可以作为核心柱进行最大面积尝试
            heights.insert(0, 0)
            heights.append(0)
            res = 0
            mono_stack = [0]
            for i in range(1,len(heights)):
                while len(mono_stack) > 0 and heights[i] < heights[mono_stack[-1]]:
                    mid = mono_stack[-1]
                    mono_stack.pop()
                    if len(mono_stack) > 0: 
                        h = heights[mid]
                        w = i - mono_stack[-1] -1
                        res = max(res, h*w)
                mono_stack.append(i)
            return res
            
   
```