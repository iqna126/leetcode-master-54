# 第六章  二叉树part02

今日任务： 226.翻转二叉树， 101.对称二叉树， 104.二叉树的最大深度， 111.二叉树的最小深度

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 递归三要素
1. 确定递归函数的参数和返回值： 确定哪些参数是递归的过程中需要处理的，那么就在递归函数里加上这个参数， 并且还要明确每次递归的返回值是什么进而确定递归函数的返回类型。
2. 确定终止条件： 写完了递归算法, 运行的时候，经常会遇到栈溢出的错误，就是没写终止条件或者终止条件写的不对，操作系统也是用一个栈的结构来保存每一层递归的信息，如果递归没有终止，操作系统的内存栈必然就会溢出。
3. 确定单层递归的逻辑： 确定每一层递归需要处理的信息。在这里也就会重复调用自己来实现递归的过程。  

## 226.[翻转二叉树](https://leetcode.com/problems/invert-binary-tree/description/)
```python
    class Solution(object):
        def invertTree(self, root):
            """
            :type root: TreeNode
            :rtype: TreeNode
            """
            # 要从上向下翻转，不然的话就会重复翻转了
            def dfs(node):
                if node is None:
                    return
                node.left, node.right = node.right, node.left
                dfs(node.left)
                dfs(node.right)
            
            dfs(root)
            return root
        
```

## 101.[对称二叉树](https://leetcode.com/problems/symmetric-tree/description/)
```python
    class Solution(object):
        def isSymmetric(self, root):
            """
            :type root: TreeNode
            :rtype: bool
            """
            if not root:
                return True
            else:
                return self.compare(root.left,root.right)

        def compare(self, left, right):
            if left== None and right == None:
                return True
            elif left == None and right != None:
                return False
            elif left != None and right == None:
                return False
            elif left.val != right.val:
                return False

            inside = self.compare(left.right, right.left)
            outside = self.compare(left.left, right.right)
            return inside and outside
            
```


## 104.[二叉树的最大深度](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)
```python
    class Solution(object):
        def maxDepth(self, root):
            """
            :type root: TreeNode
            :rtype: int
            """
            def dfs(node):
                if node is None:
                    return 0
                
                left_height = dfs(node.left)
                right_height = dfs(node.right)
                height = 1+max(left_height, right_height)
                return height
            
            return dfs(root)
            

    
        
```

## 111.[二叉树的最小深度](https://leetcode.com/problems/minimum-depth-of-binary-tree/description/)
```python
    class Solution(object):
        def getDepth(self, node):
            if node is None:
                return 0
            leftDepth = self.getDepth(node.left)  # 左
            rightDepth = self.getDepth(node.right)  # 右
            
            # 当一个左子树为空，右不为空，这时并不是最低点
            if node.left is None and node.right is not None:
                return 1 + rightDepth
            
            # 当一个右子树为空，左不为空，这时并不是最低点
            if node.left is not None and node.right is None:
                return 1 + leftDepth
            
            result = 1 + min(leftDepth, rightDepth)
            return result

        def minDepth(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: int
            """
            return self.getDepth(root)
        
            

   
        
```
