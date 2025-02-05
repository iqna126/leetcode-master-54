# 第七章 回溯算法part02

今日任务： 39. 组合总和， 40.组合总和II， 131.分割回文串

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 39.[组合总和](https://leetcode.com/problems/combination-sum/)
```python
    class Solution(object):
        def combinationSum(self, candidates, target):
            """
            :type candidates: List[int]
            :type target: int
            :rtype: List[List[int]]
            """
            res = []
            self.backtracking(candidates, target, 0, 0, [], res)
            return res

        def backtracking(self, candidates, target, sum, startindex, path, res):
            if sum > target:
                return

            if sum == target:
                res.append(path[:])
                return
            
            for i in range(startindex, len(candidates)):
                sum += candidates[i]
                path.append(candidates[i])
                self.backtracking(candidates, target, sum, i, path, res)
                sum -= candidates[i]
                path.pop()
    
```

## 40.[组合总和II](https://leetcode.com/problems/combination-sum-ii/)
```python
    class Solution(object):
        def combinationSum2(self, candidates, target):
            """
            :type candidates: List[int]
            :type target: int
            :rtype: List[List[int]]
            """
            res = []
            candidates.sort()
            self.backtracking(candidates, target, 0, 0, [], res)
            return res

        def backtracking(self, candidates, target, sum, startindex, path, res):
            if sum > target:
                return

            if sum == target:
                res.append(path[:])
                return
            
            for i in range(startindex, len(candidates)):
                if i > startindex and candidates[i] == candidates[i - 1]:
                    continue
                sum += candidates[i]
                path.append(candidates[i])
                self.backtracking(candidates, target, sum, i+1, path, res)
                sum -= candidates[i]
                path.pop()
            
    
```

## 131.[分割回文串](https://leetcode.com/problems/palindrome-partitioning/)
```python
    class Solution(object):
        def partition(self, s):
            """
            :type s: str
            :rtype: List[List[str]]
            """
            res = []
            self.backtracking(s, 0, [], res)
            return res

        def backtracking(self, s, start_index, path, result ):
            # Base Case
            if start_index == len(s):
                result.append(path[:])
                return
            
            for i in range(start_index, len(s)):
                if s[start_index: i + 1] == s[start_index: i + 1][::-1]:
                    path.append(s[start_index:i+1])
                    self.backtracking(s, i+1, path, result) 
                    path.pop()       
  
    
```
