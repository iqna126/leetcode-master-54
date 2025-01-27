# 第六章  二叉树part06

今日任务： 530.二叉搜索树的最小绝对差， 501.二叉搜索树中的众数， 236.二叉树的最近公共祖先

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 530.[二叉搜索树的最小绝对差](https://leetcode.com/problems/minimum-absolute-difference-in-bst/)
```python
    class Solution(object):
        def getMinimumDifference(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: int
            """
            res = []
            def dfs(node):
                if node is None:
                    return
                dfs(node.left)
                res.append(node.val)
                dfs(node.right)
            dfs(root)
            if len(res)<2:
                return 0
            value = np.inf
            for i in range(len(res)-1):
                value = min(value, res[i+1]-res[i])
            return value
```

双指针法：
```python
    class Solution(object):
        def __init__(self):
            self.res = float('inf')
            self.pre = None
        
        def traversal(self, cur):
            if cur is None:
                return 
            self.traversal(cur.left)
            if self.pre is not None:
                self.res = min(self.res, cur.val-self.pre.val)
            self.pre = cur
            self.traversal(cur.right)
        

        def getMinimumDifference(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: int
            """
            self.traversal(root)
            return self.res
```

## 501.[二叉搜索树中的众数](https://leetcode.com/problems/find-mode-in-binary-search-tree/)
```python
    class Solution(object):
        def __init__(self):
            self.maxcount = 0
            self.count = 0
            self.pre = None
            self.res = []

        def dfs(self, node):
            if node is None:
                return
            
            self.dfs(node.left)
            if self.pre is None:
                self.count = 1
            elif self.pre.val == node.val:
                self.count += 1
            else:
                self.count = 1
            self.pre = node

            if self.count == self.maxcount:
                self.res.append(node.val)

            if self.count > self.maxcount:
                self.maxcount = self.count
                self.res = [node.val]
            self.dfs(node.right)

        def findMode(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: List[int]
            """
            self.maxcount = 0
            self.count = 0
            self.pre = None
            self.res = []

            self.dfs(root)
            return self.res
```

## 236.[二叉树的最近公共祖先](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
```python
    class Solution(object):
        def lowestCommonAncestor(self, root, p, q):
            """
            :type root: TreeNode
            :type p: TreeNode
            :type q: TreeNode
            :rtype: TreeNode
            """
            if root == q or root == p or root is None:
                return root

            left = self.lowestCommonAncestor(root.left, p, q)
            right = self.lowestCommonAncestor(root.right, p, q)

            if left is not None and right is not None:
                return root

            if left is None and right is not None:
                return right
            elif left is not None and right is None:
                return left
            else: 
                return None
```
