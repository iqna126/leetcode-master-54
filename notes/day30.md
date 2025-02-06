# 第七章 回溯算法part03

今日任务： 93.复原IP地址， 78.子集， 90.子集II

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 93.[复原IP地址](https://leetcode.com/problems/restore-ip-addresses/)
```python
    class Solution(object):
        def restoreIpAddresses(self, s):
            """
            :type s: str
            :rtype: List[str]
            """
            res = []
            self.backtracking(s,0,0,[],res)
            return res

        def backtracking(self, s, startindex, dot_number, path, res):
            if startindex == len(s) and dot_number ==4:
                res.append('.'.join(path))
                return
            if startindex >= len(s) or dot_number > 4:
                return

            for i in range(startindex, min(startindex + 3, len(s))):
                segment = s[startindex:i + 1]
                if len(segment) > 1 and segment[0] == '0':
                    continue
                
                if segment.isdigit() and int(segment) >= 0 and int(segment) <= 255:
                    path.append(segment)
                    dot_number += 1
                    self.backtracking(s, i+1, dot_number, path,res)
                    dot_number -= 1
                    path.pop()
    
```

## 78.[子集](https://leetcode.com/problems/subsets/)
```python
    class Solution(object):
        def subsets(self, nums):
            """
            :type nums: List[int]
            :rtype: List[List[int]]
            """
            res = []
            self.backtracking(nums, 0, [], res)
            return res
        
        def backtracking(self, nums, startindex, path, res):
            res.append(path[:])
            if startindex == len(nums):
                return
            for i in range(startindex, len(nums)):
                path.append(nums[i])
                self.backtracking(nums, i+1, path, res)
                path.pop()
        
```

## 90.[子集II](https://leetcode.com/problems/subsets-ii/)
```python
    class Solution(object):
        def subsetsWithDup(self, nums):
            """
            :type nums: List[int]
            :rtype: List[List[int]]
            """
            res = []
            nums.sort() # 要sort才能比nums[i]和nums[i-1]!!不要忘记了
            self.backtracking(nums, 0, [], res)
            return res
        
        def backtracking(self, nums, startindex, path, res):
            res.append(path[:])
            if startindex == len(nums):
                return
            for i in range(startindex, len(nums)):
                if i>startindex and nums[i] == nums[i-1]:
                    continue
                path.append(nums[i])
                self.backtracking(nums, i+1, path, res)
                path.pop()
                
    
```