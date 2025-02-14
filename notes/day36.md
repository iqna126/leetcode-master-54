# 第八章 贪心算法 part05

今日任务： 56.合并区间， 738.单调递增的数字， 总结
附加任务： 968.监控二叉树

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 56.[合并区间](https://leetcode.com/problems/merge-intervals/)
```python
    class Solution(object):
        def merge(self, intervals):
            """
            :type intervals: List[List[int]]
            :rtype: List[List[int]]
            """
            if len(intervals) == 1:
                return intervals
            res = []
            intervals.sort(key = lambda x:(x[0],x[1]))
            for i in range(1,len(intervals)):
                start = intervals[i-1][0]
                if intervals[i][0] > intervals[i-1][1]:
                    if i == 1:
                        res.append([intervals[i-1][0],intervals[i-1][1]])
                    res.append([intervals[i][0],intervals[i][1]])
                elif intervals[i][0]<=intervals[i-1][1]:
                    if len(res) != 0:
                        res.pop()
                    intervals[i][0] = intervals[i-1][0]
                    intervals[i][1] = max(intervals[i-1][1], intervals[i][1])
                    res.append([intervals[i][0],intervals[i][1]])
            return res
            
```

随想录代码
```python
    class Solution:
        def merge(self, intervals):
            result = []
            if len(intervals) == 0:
                return result  # 区间集合为空直接返回

            intervals.sort(key=lambda x: x[0])  # 按照区间的左边界进行排序

            result.append(intervals[0])  # 第一个区间可以直接放入结果集中

            for i in range(1, len(intervals)):
                if result[-1][1] >= intervals[i][0]:  # 发现重叠区间
                    # 合并区间，只需要更新结果集最后一个区间的右边界，因为根据排序，左边界已经是最小的
                    result[-1][1] = max(result[-1][1], intervals[i][1])
                else:
                    result.append(intervals[i])  # 区间不重叠

            return result
```

## 738.[单调递增的数字](https://leetcode.com/problems/monotone-increasing-digits/)
```python
    class Solution(object):
        def monotoneIncreasingDigits(self, n):
            """
            :type n: int
            :rtype: int
            """
            n_list = list(str(n))

            for i in range(len(n_list) - 1, 0, -1):
                if n_list[i-1] > n_list[i]:
                    n_list[i-1] = str(int(n_list[i-1])-1) # 不用变成int(n_list[i-1])-1因为还要把后面变成9
                    for j in range(i,len(n_list)):
                        n_list[j] = str(9)
                
            return int(''.join(n_list))

        

   
```

## 968.[监控二叉树](https://leetcode.com/problems/binary-tree-cameras/)
```python
    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, val=0, left=None, right=None):
    #         self.val = val
    #         self.left = left
    #         self.right = right
    class Solution(object):
        def minCameraCover(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: int
            """
            self.res = 0
            if self.dfs(root) ==0:
                self.res +=1
            return self.res
            
        def dfs(self, node):
            # 终止条件是遇到叶子节点
            if not node:
                return 2
            left = self.dfs(node.left)
            right = self.dfs(node.right)

            if left == 0 or right == 0:
                self.res +=1 # need to use class variable or mutable variable to update its value
                return 1
            if left == 1 or right == 1:
                return 2
            if left == 2 and right == 2:
                return 0
                
   
```

## [总结](https://programmercarl.com/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95%E6%80%BB%E7%BB%93%E7%AF%87.html#%E8%B4%AA%E5%BF%83%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80)
![总结图来自代码随想录知识星球成员：海螺人](https://code-thinking-1253855093.file.myqcloud.com/pics/%E8%B4%AA%E5%BF%83%E6%80%BB%E7%BB%93water.png "总结")