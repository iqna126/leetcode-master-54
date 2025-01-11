# 第二章  链表part01

今日任务：链表理论基础，203.移除链表元素, 707.设计链表, 206.反转链表  

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 链表理论基础
单向链表定义
```python
{
    class ListNode(object):
        def __init__(self, val=0, next=None):
            self.val = val
            self.next = next

}
```

## 203.[移除链表元素](https://leetcode.com/problems/remove-linked-list-elements/description/) 
```python
{
    class Solution(object):
        def removeElements(self, head, val):
            """
            :type head: ListNode
            :type val: int
            :rtype: ListNode
            """

            dummy_head = ListNode(next = head)
            cur = dummy_head
            while cur.next:
                if cur.next.val == val:
                    cur.next = cur.next.next
                else:
                    cur = cur.next
            return dummy_head.next


}
```

## 707.[设计链表](https://leetcode.com/problems/design-linked-list/description/) 
```python
{
    class ListNode():
        def __init__(self, val = 0, next = None):
            self.val = val
            self.next = next
    
    class MyLinkedList(object):
        def __init__(self):
            self.dummy_head = ListNode()
            self.size = 0

        def get(self, index):
            """
            :type index: int
            :rtype: int
            """
            if index < 0 or index >= self.size:
                return -1
            cur = self.dummy_head.next
            for i in range(index):
                cur = cur.next
            return cur.val

        def addAtHead(self, val):
            """
            :type val: int
            :rtype: None
            """
            self.dummy_head.next = ListNode(val, self.dummy_head.next)
            self.size += 1 

        def addAtTail(self, val):
            """
            :type val: int
            :rtype: None
            """

            cur = self.dummy_head
            while cur.next:
                cur = cur.next
            cur.next = ListNode(val,next=None)
            self.size += 1 
                
        def addAtIndex(self, index, val):
            """
            :type index: int
            :type val: int
            :rtype: None
            """
            if index < 0 or index > self.size:
                return
            cur = self.dummy_head
            for i in range(index):
                cur = cur.next
            cur.next = ListNode(val, cur.next)
            self.size += 1

        def deleteAtIndex(self, index):
            """
            :type index: int
            :rtype: None
            """
            if index < 0 or index >= self.size:
                return
            cur = self.dummy_head
            for i in range(index):
                cur = cur.next
            cur.next = cur.next.next 
            self.size -= 1 
     

}
```

## 206.[反转链表](https://leetcode.com/problems/reverse-linked-list/description/) 
```python
{
    class Solution(object):
        def reverseList(self, head):
            """
            :type head: ListNode
            :rtype: ListNode
            """
            res = head
            pre = None
            while res:
                temp = res.next
                res.next = pre 
                pre = res
                res = temp
            return pre

}
```


