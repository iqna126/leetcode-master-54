# 第五章  栈与队列part01

今日任务： 栈与队列理论基础， 232.用栈实现队列， 225. 用队列实现栈， 20. 有效的括号， 1047. 删除字符串中的所有相邻重复项

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 栈与队列理论基础
栈（stack）： 先进后出（LIFO），python中的实现可以用：list，deque  
队列（queue）： 先进先出（FIFO），python中的实现可以用：list，deque

## 232.[用栈实现队列](https://leetcode.com/problems/implement-queue-using-stacks/)
```python
{
    class MyQueue(object):
        def __init__(self):
            self.stack_take = []
            self.stack_out = []
        
        def push(self, x):
            """
            :type x: int
            :rtype: None
            """
            self.stack_take.append(x)

        def pop(self):
            """
            :rtype: int
            """
            if not self.stack_out:
                while self.stack_take:
                    self.stack_out.append(self.stack_take.pop())
            return self.stack_out.pop()

        def peek(self):
            """
            :rtype: int 
            """
            res = self.pop()
            self.stack_out.append(res)
            return res

        def empty(self):
            """
            :rtype: boolean
            """
            if not self.stack_out and not self.stack_take:
                return True
            else:
                return False

}
```

## 225.[用队列实现栈](https://leetcode.com/problems/implement-stack-using-queues/)
```python
{
    class MyStack(object):
        def __init__(self):
            self.queue = deque()
            
        def push(self, x):
            """
            :type x: int
            :rtype: None
            """
            self.queue.append(x)

        def pop(self):
            """
            :rtype: int
            """
            for i in range(len(self.queue)-1):
                temp = self.queue.popleft()
                self.queue.append(temp)
            res = self.queue.popleft()
            return res
            

        def top(self):
            """
            :rtype: int
            """
            res = self.pop()
            self.queue.append(res)
            return res


        def empty(self):
            """
            :rtype: boolean
            """
            if not self.queue:
                return True
            else:
                return False
            

}
```

## 20.[有效的括号](https://leetcode.com/problems/valid-parentheses/)
```python
{
    class Solution(object):
        def isValid(self, s):
            """
            :type s: str
            :rtype: bool
            """
            res = []
            for i in s:
                if i =='(':
                    res.append(')')
                elif i == '[':
                    res.append(']')
                elif i == '{':
                    res.append('}')
                elif not res or res[-1] != i:
                    return False
                else:
                    res.pop()
            return True if not res else False

}
```


## 1047. [删除字符串中的所有相邻重复项](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)
```python
{
    class Solution(object):
        def removeDuplicates(self, s):
            """
            :type s: str
            :rtype: str
            """
            res = []
            for i in s:
                if res and res[-1] == i:
                    res.pop()
                else:
                    res.append(i)
            return ''.join(res)

}
```



