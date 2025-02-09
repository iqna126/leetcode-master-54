# 第七章 回溯算法part04

今日任务： 491.递增子序列， 46.全排列， 47.全排列II， 总结  
附加任务： 332.重新安排行程， 51.N皇后， 37.解数独

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 491.[递增子序列](https://leetcode.com/problems/non-decreasing-subsequences/)
```python
    class Solution(object):
        def findSubsequences(self, nums):
            """
            :type nums: List[int]
            :rtype: List[List[int]]
            """
            res = []
            self.backtracking(nums,0, [], res)
            return res

        def backtracking(self, nums, startindex, path, res):
            if startindex > len(nums):
                return
            if len(path) >= 2:
                res.append(path[:])
            
            used = set()
            for i in range(startindex,len(nums)):
                if (path and nums[i] < path[-1]) or nums[i] in used: # 这里注意要检查是否是本层使用过的元素， 因为不能行子集II里那样排序，所以不能比较 nums[i] 和 nums[i-1]， 要比较现在添加的数字nums[i] 是不是已经在本层添加过了
                    continue
                used.add(nums[i])
                path.append(nums[i])
                self.backtracking(nums, i+1, path, res)
                path.pop()
            
   
```

## 46.[全排列](https://leetcode.com/problems/permutations/)
```python
    class Solution(object):
        def permute(self, nums):
            """
            :type nums: List[int]
            :rtype: List[List[int]]
            """
            res = []
            self.backtracking(nums,[], [False] * len(nums), res)
            return res

        def backtracking(self, nums, path, used, res):
            if len(path) == len(nums):
                res.append(path[:])
                return

            
            for i in range(len(nums)):
                if used[i]:
                    continue
                used[i] = True
                path.append(nums[i])
                self.backtracking(nums,path,used,res)
                path.pop()
                used[i] = False
                
   
```

## 47.[全排列II](https://leetcode.com/problems/permutations-ii/)
```python
    class Solution(object):
        def permuteUnique(self, nums):
            """
            :type nums: List[int]
            :rtype: List[List[int]]
            """
            res = []
            self.backtracking(nums,[], [False] * len(nums), res)
            return res

        def backtracking(self, nums, path, used, res):
            if len(path) == len(nums):
                res.append(path[:])
                return
            uset = set()
            for i in range(len(nums)):
                if used[i] or nums[i] in uset:
                    continue
                used[i] = True
                uset.add(nums[i])
                path.append(nums[i])
                self.backtracking(nums,path,used,res)
                path.pop()
                used[i] = False
            
    
    
```

## 332.[重新安排行程](https://leetcode.com/problems/reconstruct-itinerary/)
```python
   class Solution(object):
        def findItinerary(self, tickets):
            """
            :type tickets: List[List[str]]
            :rtype: List[str]
            """
        
    
```

## 51.[N皇后](https://leetcode.com/problems/n-queens/)
```python
   class Solution(object):
        def solveNQueens(self, n):
            """
            :type n: int
            :rtype: List[List[str]]
            """
        
    
```

## 37.[解数独](https://leetcode.com/problems/sudoku-solver/)
```python
    class Solution(object):
        def solveSudoku(self, board):
            """
            :type board: List[List[str]]
            :rtype: None Do not return anything, modify board in-place instead.
            """
            
    
```

## [总结](https://programmercarl.com/%E5%9B%9E%E6%BA%AF%E6%80%BB%E7%BB%93.html)
