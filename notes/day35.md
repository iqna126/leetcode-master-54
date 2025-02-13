# 第八章 贪心算法 part04

今日任务： 452.用最少数量的箭引爆气球， 435.无重叠区间， 763.划分字母区间

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 452.[用最少数量的箭引爆气球](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/)
```python
    class Solution(object):
        def findMinArrowShots(self, points):
            """
            :type points: List[List[int]]
            :rtype: int
            """
            if len(points) == 0:
                return 0 # 没有气球不需要射箭
            res = 1
            points.sort(key = lambda x: (x[0],x[1]))
            for i in range(1,len(points)):
                if points[i][0]>points[i-1][1]:
                    res += 1
                else: 
                    points[i][1] = min(points[i][1],points[i-1][1])
            return res
            
        
            
```

## 435.[无重叠区间](https://leetcode.com/problems/non-overlapping-intervals/)
```python
    class Solution(object):
        def eraseOverlapIntervals(self, intervals):
            """
            :type intervals: List[List[int]]
            :rtype: int
            """
            res = 0 
            intervals.sort(key = lambda x :(x[0],x[1]))
            for i in range(1, len(intervals)):
                if intervals[i][0]<intervals[i-1][1]:
                    res += 1
                    intervals[i][1] = min(intervals[i][1], intervals[i-1][1])
            return res
            
            
            
```

## 763.[划分字母区间](https://leetcode.com/problems/partition-labels/)
```python
    class Solution(object):
        def partitionLabels(self, s):
            """
            :type s: str
            :rtype: List[int]
            """
            last_position = {}
            for i in range(len(s)):
                last_position[s[i]] = i
            res = []
            curmax = 0
            j=0
            for i in range(len(s)):
                curmax = max(curmax, last_position[s[i]])
                if i==curmax:
                    res.append(i+1-j)
                    j = i+1

            return res
                
            
```
