# 第九章 动态规划part07

今日任务： 198.打家劫舍， 213.打家劫舍II， 337.打家劫舍III

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 198.[打家劫舍](https://leetcode.com/problems/house-robber/)
```python
    class Solution(object):
        def rob(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            dp = [0] * len(nums)
            dp[0] = nums[0]
            if len(nums)>1:
                dp[1] = max(nums[0], nums[1])        
                for i in range(2,len(nums)):
                    dp[i] = max(dp[i-2]+nums[i], dp[i-1])
            return dp[len(nums)-1]
            
            
```

## 213.[打家劫舍II](https://leetcode.com/problems/house-robber-ii/)
```python
    class Solution(object):
        def rob(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            n = len(nums)
            if n == 0:
                return 0
            if n == 1:
                return nums[0]
            one_nm1 = self.robberI(nums, 0, n-2)
            two_n = self.robberI(nums, 1, n-1)

            return max(one_nm1, two_n)

        def robberI(self, nums, start_index, end_index):
            if end_index == start_index:
                return  nums[start_index]
            dp_len = end_index - start_index
            dp = [0] * (dp_len + 1)
            dp[0] = nums[start_index]
            dp[1] = max(nums[start_index], nums[start_index + 1])
            for i in range(2,dp_len+1):
                dp[i] = max(dp[i-1], dp[i-2]+nums[i+start_index])
                print("dp[i]: ", dp[i], " i: ", i)
            return dp[-1]


```

## 337.[打家劫舍III](https://leetcode.com/problems/house-robber-iii/)
```python
    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, val=0, left=None, right=None):
    #         self.val = val
    #         self.left = left
    #         self.right = right
    class Solution(object):
        def rob(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: int
            """
            # dp数组（dp table）以及下标的含义：
            # 1. 下标为 0 记录 **不偷该节点** 所得到的的最大金钱
            # 2. 下标为 1 记录 **偷该节点** 所得到的的最大金钱
            dp = self.dfs(root)
            return max(dp)
        
        def dfs(self, node):
            if node is None:
                return [0,0]
            
            left = self.dfs(node.left)
            right = self.dfs(node.right)

            not_cur = max(left[0], left[1])+max(right[0], right[1])
            rob_cur = node.val + left[0] + right[0]
            return [not_cur, rob_cur]
        

```