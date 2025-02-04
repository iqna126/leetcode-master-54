# 第七章 回溯算法part01

今日任务： 理论基础， 77.组合， 216.组合总和III， 17.电话号码的字母组合 

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## [理论基础](https://programmercarl.com/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html#%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80)
回溯算法是一种搜索方法，其本质是穷举法。 
回溯算法可以用来解决的问题种类：
### 回溯三部曲
1. 回溯函数backtracking模版其返回值以及参数： 返回值一般为void， 参数的确定一般根据逻辑种需要什么参数就添加什么参数。 
2. 回溯函数的终止条件： 所有的回溯法问题都可以抽象为树形结构，查找的集合大小是树的宽度，递归的深度是树的深度，所以判断终止条件可以借鉴二叉树递归的终止条件判断
3. 回溯搜索的遍历过程：
```
    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) { // 横向遍历
        处理节点;
        backtracking(路径，选择列表); // 递归， 纵向遍历
        回溯，撤销处理结果
    }
```


## 77.[组合](https://leetcode.com/problems/combinations/)
```python
    class Solution(object):
        def combine(self, n, k):
            """
            :type n: int
            :type k: int
            :rtype: List[List[int]]
            """
            res = []
            path = []
            self.backtracking(n, k , 1, path, res)
            return res

        def backtracking(self, n, k, startindex, path, res):
            if len(path) == k:
                res.append(path[:])
                return
            for i in range(startindex, n - (k - len(path)) + 2):
                path.append(i)
                self.backtracking(n, k, i+1, path, res)
                path.pop()
    
```

## 216.[组合总和III](https://leetcode.com/problems/combination-sum-iii/)
```python
    class Solution(object):
        def combinationSum3(self, k, n):
            """
            :type k: int
            :type n: int
            :rtype: List[List[int]]
            """
            res = []
            path = []
            self.backtracking(n, k , 1, path, res)
            return res

        def backtracking(self, n, k, startindex, path, res):
            if len(path) == k and sum(path) == n:
                res.append(path[:])
                return
            for i in range(startindex, 10):
                path.append(i)
                self.backtracking(n, k, i+1, path, res)
                path.pop()
        
    
```

## 17.[电话号码的字母组合](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)
```python
    class Solution(object):
        def letterCombinations(self, digits):
            """
            :type digits: str
            :rtype: List[str]
            """
            digit2str = ["", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"]
            if len(digits) == 0:
                return []
            res = []
            self.backtracking(digits, 0, "", res, digit2str)
            return res

        def backtracking(self, digits, index, path, res, digit2str):
            if index == len(digits):
                res.append(path)
                return 
            cur = int(digits[index])
            letters = digit2str[cur]
            for i in range(len(letters)):
                path += letters[i]
                self.backtracking(digits, index+1, path, res, digit2str)
                path = path[:-1]
                
        
    
```
