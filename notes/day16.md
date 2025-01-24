# 第六章  二叉树part04

今日任务： 513.找树左下角的值， 112.路径总和， 113.路径总和ii， 106.从中序与后序遍历序列构造二叉树， 105.从前序与中序遍历序列构造二叉树

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 513.[找树左下角的值](https://leetcode.com/problems/find-bottom-left-tree-value/description/)
```python
    class Solution(object):
        def findBottomLeftValue(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: int
            """
            # 思路： 层序遍历最下层第一个
            if not root:
                return []
            queue = collections.deque([root])
            result = []
            while queue:
                level = []
                for _ in range(len(queue)):
                    cur = queue.popleft()
                    level.append(cur.val)
                    if cur.left:
                        queue.append(cur.left)
                    if cur.right:
                        queue.append(cur.right)
                result = level[0]
            return result
    
```

## 112.[路径总和](https://leetcode.com/problems/path-sum/description/)
```python
    class Solution(object):
        def hasPathSum(self, root, targetSum):
            """
            :type root: Optional[TreeNode]
            :type targetSum: int
            :rtype: bool
            """
            # 思路：借助查找二叉树所有路径的想法
            res = []
            path = []
            if not root:
                return False
            self.dfs(root, res, path)
            if targetSum in res: # 但是其实只要找到一个值就可以返回了不需要遍历整棵树
                return True
            else:
                return False

        def dfs(self, node, res, path):
            path.append(node.val)
            if node.left is None and node.right is None:
                one_path_sum = sum(path)
                res.append(one_path_sum)
                return
            if node.left:
                self. dfs(node.left, res, path)
                path.pop()
            if node.right:
                self.dfs( node.right, res, path)
                path.pop()
 
```

## 113.[路径总和ii](https://leetcode.com/problems/path-sum-ii/)
```python
    class Solution(object):
        def pathSum(self, root, targetSum):
            """
            :type root: Optional[TreeNode]
            :type targetSum: int
            :rtype: List[List[int]]
            """
            result = []
            self.traversal(root, targetSum, [], result)
            return result

        def traversal(self, node, count, path, result):
                if not node:
                    return
                path.append(node.val)
                count -= node.val
                if not node.left and not node.right and count == 0:
                    result.append(list(path))
                self.traversal(node.left, count, path, result)
                self.traversal(node.right, count, path, result)
                path.pop()

```

## 106.[从中序与后序遍历序列构造二叉树](https://leetcode.com/problems/balanced-binary-tree/)
```python
    class Solution(object):
        def buildTree(self, inorder, postorder):
            """
            :type inorder: List[int]
            :type postorder: List[int]
            :rtype: Optional[TreeNode]
            """
            if not postorder:
                return None
            
            root_val = postorder[-1]
            root = TreeNode(root_val)
            separator_index = inorder.index(root_val)

            inorder_left = inorder[:separator_index]
            inorder_right = inorder[separator_index+1:]

            postorder_left = postorder[:len(inorder_left)]
            postorder_right = postorder[len(inorder_left):len(postorder)-1]

            root.left = self.buildTree(inorder_left,postorder_left)
            root.right = self.buildTree(inorder_right,postorder_right)
            return root

   
```

## 105.[从前序与中序遍历序列构造二叉树](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
```python
    class Solution(object):
        def buildTree(self, preorder, inorder):
            """
            :type preorder: List[int]
            :type inorder: List[int]
            :rtype: Optional[TreeNode]
            """
            if not preorder:
                return None
            
            root_val = preorder[0]
            root = TreeNode(root_val)
            separator_index = inorder.index(root_val)

            inorder_left = inorder[:separator_index]
            inorder_right = inorder[separator_index+1:]

            preorder_left = preorder[1:len(inorder_left)+1]
            preorder_right = preorder[len(inorder_left)+1:]

            root.left = self.buildTree(preorder_left, inorder_left)
            root.right = self.buildTree(preorder_right, inorder_right)
            return root
    
   
```