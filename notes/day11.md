# 第五章  栈与队列part02

今日任务： 150.逆波兰表达式求值， 239.滑动窗口最大值， 347.前K个高频元素， 栈与队列总结

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 150.[逆波兰表达式求值](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
```python
{
    from operator import add, sub, mul
    class Solution(object):
        
        def div(x, y):
            return int(x/y) if x*y > 0 else -int(abs(x)/abs(y))
        
        op_map = {'+': add, '-': sub, '*': mul, '/': div}

        def evalRPN(self, tokens):
            """
            :type tokens: List[str]
            :rtype: int
            """ 
            stack = []
            for j in range(len(tokens)):
                i = tokens[j]
                if i in self.op_map:
                    temp1 = stack.pop()
                    temp2 = stack.pop()
                    temp = self.op_map[i](temp2,temp1)
                    stack.append(temp)
                    # print(stack)
                else:
                    stack.append(int(i))
                    # print(stack)
            return stack.pop()
        



            

}
```

## 239.[滑动窗口最大值](https://leetcode.com/problems/sliding-window-maximum/)
```python
{
    from collections import deque
    class mono_queue:
        def __init__(self):
            self.queue = deque()
        
        def pop(self, value):
            if self.queue and value==self.queue[0]:
                self.queue.popleft()

        def push(self, value):
            while self.queue and value>self.queue[-1]:
                self.queue.pop()
            self.queue.append(value)

        def front(self):
            return self.queue[0]

    class Solution(object):
        def maxSlidingWindow(self, nums, k):
            """
            :type nums: List[int]
            :type k: int
            :rtype: List[int]
            """
            store = mono_queue()
            res = []
            for i in range(k):
                store.push(nums[i])
            res.append(store.front())
            for i in range(k,len(nums)):
                store.pop(nums[i-k])
                store.push(nums[i])
                res.append(store.front())
            return res

            

}
```

## 347.[前K个高频元素](https://leetcode.com/problems/top-k-frequent-elements/)
```python
{
    import heapq
    class Solution(object):
        def topKFrequent(self, nums, k):
            """
            :type nums: List[int]
            :type k: int
            :rtype: List[int]
            """
            store = {}
            for i in range(len(nums)):
                store[nums[i]] = store.get(nums[i],0)+1
            
            pri_que = []
            for key, freq in store.items():
                heapq.heappush(pri_que,(freq,key))
                if len(pri_que) > k:
                    heapq.heappop(pri_que)
            
            res = []
            for i in range(k-1,-1,-1):
                res.append(heapq.heappop(pri_que)[1])
            return res
        
}
```

## 栈与队列总结 
### 灵魂四问小结 C++ 部分：
1. stack和queue在C++中严格来说不是容器，而是容器适配器(container adaptor)。它们是基于其他容器实现的接口。  
2. 现代C++使用的STL版本主要是基于SGI STL实现的。不同编译器可能有细微差异，但基本实现理念是一致的。  
3. C++中的stack和queue默认是基于deque容器实现的。也可以指定使用其他满足要求的容器：  
    1. stack可以基于vector、deque或list实现
    2. queue可以基于deque或list实现

4. C++中的stack和queue不提供迭代器。这两种数据结构的核心思想就是限制访问方式：  
    1. stack只允许在一端进行操作， 先入后出（LIFO）
    2. queue只允许在一端入队，另一端出队， 先入先出（FIFO）

### 灵魂四问小结 Python 部分：
1. Python中对应的实现是：    
collections.deque可以用作stack和queue
queue模块提供了Queue类
2. Python中没有明确的STL版本概念，这些实现是Python标准库的一部分，随Python版本更新。
3. Python的实现方式：
    1. deque是基于双向链表实现的
    2. Queue类在底层也是使用deque实现的，但增加了线程安全特性


4. 迭代器的提供上， Python中的情况不同：
    1. deque是可迭代的，支持下标访问
    2. Queue对象本身不支持直接迭代，需要通过get()方法逐个获取元素

### 最大的区别是：
C++通过容器适配器严格限制了接口，而Python的实现更灵活  
Python的deque既可以用作stack也可以用作queue，而且支持迭代； Queue类主要用于多线程场景，增加了线程安全机制




