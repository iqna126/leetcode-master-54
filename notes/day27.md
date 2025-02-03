# 第六章  二叉树part08

今日任务： 669.修剪二叉搜索树， 108.将有序数组转换为二叉搜索树， 538.把二叉搜索树转换为累加树， 总结

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 669.[修剪二叉搜索树](https://leetcode.com/problems/trim-a-binary-search-tree/)
```python
    class Solution(object):
        def trimBST(self, root, low, high):
            """
            :type root: Optional[TreeNode]
            :type low: int
            :type high: int
            :rtype: Optional[TreeNode]
            """
            if root is None:
                return 
            if root.val < low:
                return self.trimBST(root.right, low, high)
            if root.val > high:
                return self.trimBST(root.left, low, high)

            root.left = self.trimBST(root.left, low, high)
            root.right = self.trimBST(root.right, low, high)
            return root
```

## 108.[将有序数组转换为二叉搜索树](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)
```python
    class Solution(object):
        def sortedArrayToBST(self, nums):
            """
            :type nums: List[int]
            :rtype: Optional[TreeNode]
            """
            if not nums:
                return 
            mid = len(nums)//2
            print(mid)
            root = TreeNode(nums[mid])
            left = nums[:mid]
            right = nums[mid+1:]
            root.left = self.sortedArrayToBST(left)     
            root.right = self.sortedArrayToBST(right)  
            return root 
```

## 538.[把二叉搜索树转换为累加树](https://leetcode.com/problems/convert-bst-to-greater-tree/)
```python
    class Solution(object):
        def convertBST(self, root):
            """
            :type root: Optional[TreeNode]
            :rtype: Optional[TreeNode]
            """
            self.pre = 0
            self.dfs(root)
            return root


        def dfs(self, node):
            if node is None:
                return
            self.dfs(node.right)
            node.val += self.pre
            self.pre = node.val 
            self.dfs(node.left)
            
```

## 总结
![总结图来自代码随想录知识星球成员：青](https://code-thinking-1253855093.file.myqcloud.com/pics/20211030125421.png "总结")