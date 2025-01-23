# 第六章  二叉树part03

今日任务： 110.平衡二叉树， 257.二叉树的所有路径， 404.左叶子之和， 222.完全二叉树的节点个数

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 递归三要素
1. 确定递归函数的参数和返回值： 确定哪些参数是递归的过程中需要处理的，那么就在递归函数里加上这个参数， 并且还要明确每次递归的返回值是什么进而确定递归函数的返回类型。
2. 确定终止条件： 写完了递归算法, 运行的时候，经常会遇到栈溢出的错误，就是没写终止条件或者终止条件写的不对，操作系统也是用一个栈的结构来保存每一层递归的信息，如果递归没有终止，操作系统的内存栈必然就会溢出。
3. 确定单层递归的逻辑： 确定每一层递归需要处理的信息。在这里也就会重复调用自己来实现递归的过程。 

## 110.[平衡二叉树](https://leetcode.com/problems/balanced-binary-tree/)
```python
    class Solution(object):
        def isBalanced(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: bool
            """
            def dfs(node):
                if node is None:
                    return 0
                
                left_height = dfs(node.left)
                if left_height == -1:
                    return -1
                right_height = dfs(node.right)
                if right_height == -1:
                    return -1
                if abs(left_height - right_height) > 1:
                    return -1
                else: 
                    return 1+max(left_height,right_height)


            if not root:
                return True
            elif dfs(root) != -1:
                return True
            else: 
                return False

```

## 257.[二叉树的所有路径](https://leetcode.com/problems/binary-tree-paths/description/)
```python
    class Solution(object):
        def binaryTreePaths(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: List[str]
            """
            res = []
            path = []
            if not root:
                return res
            self.dfs(root, res, path)
            return res

        def dfs(self, node, res, path):
            path.append(node.val)
            if node.left is None and node.right is None:
                one_path = '->'.join(map(str,path))
                res.append(one_path)
                return
            if node.left:
                self. dfs(node.left, res, path)
                path.pop()
            if node.right:
                self.dfs( node.right, res, path)
                path.pop()
            
    
```

## 404.[左叶子之和](https://leetcode.com/problems/sum-of-left-leaves/)
```python
    class Solution(object):
        def sumOfLeftLeaves(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: int
            """
            if root is None:
                return 0
            if root.left is None and root.right is None:
                return 0
            
            leftValue = self.sumOfLeftLeaves(root.left)  # 左
            if root.left and not root.left.left and not root.left.right:  # 左子树是左叶子的情况
                leftValue = root.left.val
                
            rightValue = self.sumOfLeftLeaves(root.right)  # 右

            sum_val = leftValue + rightValue  # 中
            return sum_val
    
```

## 222.[完全二叉树的节点个数](https://leetcode.com/problems/count-complete-tree-nodes/description/)
```python
    class Solution(object):
        def countNodes(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: int
            """
            def dfs(node):
                if node is None:
                    return 0
                left_number = dfs(node.left)
                right_number = dfs(node.right)
                sum = left_number + right_number + 1
                return sum

            
            if not root:
                return 0
            return dfs(root)

        

    
```