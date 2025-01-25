# 第六章  二叉树part05

今日任务： 654.最大二叉树， 617.合并二叉树， 700.二叉搜索树中的搜索， 98.验证二叉搜索树

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 654.[最大二叉树](https://leetcode.com/problems/maximum-binary-tree/)
```python
    class Solution(object):
        def constructMaximumBinaryTree(self, nums):
            """
            :type nums: List[int]
            :rtype: Optional[TreeNode]
            """
            if not nums:
                return None
            root_val = max(nums)
            root = TreeNode(root_val)
            separator_index = nums.index(root_val)

            nums_left = nums[:separator_index]
            nums_right = nums[separator_index+1:]
            
            root.left = self.constructMaximumBinaryTree(nums_left)
            root.right = self.constructMaximumBinaryTree(nums_right)
            return root

```

## 617.[合并二叉树](https://leetcode.com/problems/merge-two-binary-trees/)
```python
    class Solution(object):
        def mergeTrees(self, root1, root2):
            """
            :type root1: Optional[TreeNode]
            :type root2: Optional[TreeNode]
            :rtype: Optional[TreeNode]
            """

            if root1 is None:
                return root2
            if root2 is None: 
                return root1
            
            root1.val += root2.val
            root1.left = self.mergeTrees(root1.left, root2.left)
            root1.right = self.mergeTrees(root1.right, root2.right)

            return root1

```

## 700.[二叉搜索树中的搜索](https://leetcode.com/problems/search-in-a-binary-search-tree/)
```python
        class Solution(object):
        def searchBST(self, root, val):
            """
            :type root: Optional[TreeNode]
            :type val: int
            :rtype: Optional[TreeNode]
            """

            return self.dfs(root, val)
        
        def dfs(self, node, val):
            if node is None:
                return node

            if node.val > val:
                return self.dfs(node.left, val)
            elif node.val <val:
                return self.dfs(node.right, val)
            else:
                return node
            
```

## 98.[验证二叉搜索树](https://leetcode.com/problems/validate-binary-search-tree//)
```python
    class Solution(object):
        def isValidBST(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: bool
            """
            res = []
            def dfs(node):
                if node is None:
                    return 
                dfs(node.left)
                res.append(node.val)
                dfs(node.right)
            dfs(root)
            for i in range(len(res)-1):
                if res[i]>=res[i+1]:
                    return False
            return True


```