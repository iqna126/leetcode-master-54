# 第六章  二叉树part01

今日任务： 二叉树理论基础， 递归遍历， 迭代遍历， 统一迭代， 层序遍历

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 二叉树理论基础
python中二叉树节点的定义：
```python
    class TreeNode:
        def __init__(self, val, left = None, right = None):
            self.val = val
            self.left = left
            self.right = right
```

## [递归遍历](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%80%92%E5%BD%92%E9%81%8D%E5%8E%86.html)
### 递归三要素
1. 确定递归函数的参数和返回值： 确定哪些参数是递归的过程中需要处理的，那么就在递归函数里加上这个参数， 并且还要明确每次递归的返回值是什么进而确定递归函数的返回类型。
2. 确定终止条件： 写完了递归算法, 运行的时候，经常会遇到栈溢出的错误，就是没写终止条件或者终止条件写的不对，操作系统也是用一个栈的结构来保存每一层递归的信息，如果递归没有终止，操作系统的内存栈必然就会溢出。
3. 确定单层递归的逻辑： 确定每一层递归需要处理的信息。在这里也就会重复调用自己来实现递归的过程。  

144.[二叉树的前序遍历](https://leetcode.com/problems/binary-tree-preorder-traversal/)
```python
    class Solution(object):

        def preorderTraversal(self, root):
            """
            :type root: TreeNode
            :rtype: List[int]
            """
            res = []

            def dfs(node):
                if node is None:
                    return
                # 中左右
                res.append(node.val)
                dfs(node.left)
                dfs(node.right)
            
            dfs(root)
            return res
        
```
145.[二叉树的后序遍历](https://leetcode.com/problems/binary-tree-postorder-traversal/submissions/1515304376/)
```python
    class Solution(object):
        def postorderTraversal(self, root):
            """
            :type root: TreeNode
            :rtype: List[int]
            """
            res = []
            
            def dfs(node):
                if node is None:
                    return
                # 左右中
                dfs(node.left)
                dfs(node.right)
                res.append(node.val)
            
            dfs(root)
            return res
```
94.[二叉树的中序遍历](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)
```python
    class Solution(object):
        def inorderTraversal(self, root):
            """
            :type root: TreeNode
            :rtype: List[int]
            """
            res = []

            def dfs(node):
                if node is None:
                    return 
                # 左中右
                dfs(node.left)
                res.append(node.val)
                dfs(node.right)

            dfs(root)
            return res

```


## [迭代遍历](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E8%BF%AD%E4%BB%A3%E9%81%8D%E5%8E%86.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
144.[二叉树的前序遍历](https://leetcode.com/problems/binary-tree-preorder-traversal/)
```python
    class Solution(object):

        def preorderTraversal(self, root):
            """
            :type root: TreeNode
            :rtype: List[int]
            """
            if not root:
                return []

            res = []
            stack = [root]
            while stack:
                node = stack.pop()
                res.append(node.val)
                if node.right:
                    stack.append(node.right)
                if node.left:
                    stack.append(node.left)
            return res

        
```
145.[二叉树的后序遍历](https://leetcode.com/problems/binary-tree-postorder-traversal/submissions/1515304376/)
```python
    class Solution(object):
        def postorderTraversal(self, root):
            """
            :type root: TreeNode
            :rtype: List[int]
            """
            if not root:
                return []
            res = []
            stack = []
            cur = root
            while cur or stack:
                # 先迭代访问最底层的左子树节点
                if cur:     
                    stack.append(cur)
                    cur = cur.left		
                # 到达最左节点后处理栈顶节点    
                else:		
                    cur = stack.pop()
                    res.append(cur.val)
                    # 取栈顶元素右节点
                    cur = cur.right	
            return res
```
94.[二叉树的中序遍历](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)
```python
    class Solution(object):
        def inorderTraversal(self, root):
            """
            :type root: TreeNode
            :rtype: List[int]
            """
            if not root:
                return []

            res = []
            stack=[root]
            while stack:
                node = stack.pop()
                res.append(node.val)
                if node.left:
                    stack.append(node.left)
                if node.right:
                    stack.append(node.right)
            return res[::-1]


```



## [统一迭代](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E7%BB%9F%E4%B8%80%E8%BF%AD%E4%BB%A3%E6%B3%95.html)
94.[二叉树的中序遍历](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)
```python
    class Solution(object):
        def inorderTraversal(self, root):
            """
            :type root: TreeNode
            :rtype: List[int]
            """
            res = []
            stack = []
            if root:
                stack.append(root)
            while stack:
                node = stack.pop()
                if node != None:
                    if node.right: #添加右节点（空节点不入栈）
                        stack.append(node.right)
                    
                    stack.append(node) #添加中节点
                    stack.append(None) #中节点访问过，但是还没有处理，加入空节点做为标记。
                    
                    if node.left: #添加左节点（空节点不入栈）
                        stack.append(node.left)
                else: #只有遇到空节点的时候，才将下一个节点放进结果集
                    node = stack.pop() #重新取出栈中元素
                    res.append(node.val) #加入到结果集
            return res


```

## [层序遍历](https://programmercarl.com/0102.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
```python
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
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
            result.append(level)
        return result
```


