# 第六章  二叉树part07

今日任务： 235.二叉搜索树的最近公共祖先， 701.二叉搜索树中的插入操作， 450.删除二叉搜索树中的节点

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 235.[二叉搜索树的最近公共祖先](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)
```python
    class Solution(object):
        def lowestCommonAncestor(self, root, p, q):
            """
            :type root: TreeNode
            :type p: TreeNode
            :type q: TreeNode
            :rtype: TreeNode
            """

```

## 701.[二叉搜索树中的插入操作](https://leetcode.com/problems/insert-into-a-binary-search-tree/)
```python
    class Solution(object):
        def __init__(self):
            self.parent = None

        def traversal(self, cur, val):
            if cur is None:
                node = TreeNode(val)
                if val > self.parent.val:
                    self.parent.right = node
                else:
                    self.parent.left = node
                return

            self.parent = cur
            if cur.val > val:
                self.traversal(cur.left, val)
            if cur.val < val:
                self.traversal(cur.right, val)

        def insertIntoBST(self, root, val):
            """
            :type root: Optional[TreeNode]
            :type val: int
            :rtype: Optional[TreeNode]
            """
            self.parent = TreeNode(0)
            if root is None:
                return TreeNode(val)
            self.traversal(root, val)
            return root
            

```

## 450.[删除二叉搜索树中的节点](https://leetcode.com/problems/delete-node-in-a-bst/)
```python
    class Solution(object):
        def deleteNode(self, root, key):
            """
            :type root: Optional[TreeNode]
            :type key: int
            :rtype: Optional[TreeNode]
            """
            if root is None:
                return root
            if root.val == key:
                if root.left is None and root.right is None:
                    return None
                elif root.left is None:
                    return root.right
                elif root.right is None:
                    return root.left
                else:
                    cur = root.right
                    while cur.left is not None:
                        cur = cur.left
                    cur.left = root.left
                    return root.right
            if root.val > key:
                root.left = self.deleteNode(root.left, key)
            if root.val < key:
                root.right = self.deleteNode(root.right, key)
            return root
        

```