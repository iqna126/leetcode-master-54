# 第二章  链表part02

今日任务： 24. 两两交换链表中的节点， 19.删除链表的倒数第N个节点， 面试题 02.07. 链表相交， 142.环形链表II， 总结

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 24.[两两交换链表中的节点](https://leetcode.com/problems/swap-nodes-in-pairs/description/) 
```python
{
    class Solution(object):
        def swapPairs(self, head):
            """
            :type head: ListNode
            :rtype: ListNode
            """
            dummy_head = ListNode(next=head)
            cur = dummy_head

            while cur.next and cur.next.next:
                temp1 = cur.next
                temp2 = cur.next.next.next
                cur.next = cur.next.next
                cur.next.next = temp1
                temp1.next = temp2
                cur = cur.next.next
            return dummy_head.next

}
```


## 19.[删除链表的倒数第N个节点](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/) 
```python
{
    class Solution(object):
        def removeNthFromEnd(self, head, n):
            """
            :type head: ListNode
            :type n: int
            :rtype: ListNode
            """
            dummy_head = ListNode(next = head)
            slow = dummy_head
            fast = dummy_head

            for i in range(n):
                fast = fast.next
            while fast.next:
                fast = fast.next
                slow = slow.next
            slow.next = slow.next.next
            return dummy_head.next

}
```


## [面试题 02.07. 链表相交](https://programmercarl.com/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4.html)
同leetcode 160.[Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)  
```python
{
    class Solution(object):
        def getIntersectionNode(self, headA, headB):
            """
            :type head1, head1: ListNode
            :rtype: ListNode
            """
            dummyA = ListNode(next = headA)
            dummyB = ListNode(next = headB)
            curA = dummyA
            curB = dummyB
            lenA, lenB = 0, 0 

            while curA:
                curA = curA.next
                lenA += 1
            
            while curB:
                curB = curB.next
                lenB += 1
            
            if lenA < lenB:
                lenB, lenA = lenA, lenB
                dummyB, dummyA = dummyA, dummyB
            
            curA = dummyA.next
            curB = dummyB.next
            
            for i in range(lenA-lenB):
                curA = curA.next
            
            while curA and curB:
                if curA == curB:
                    return curA
                else:
                    curA = curA.next
                    curB = curB.next
            return None
       
}
```


## 142.[环形链表II](https://leetcode.com/problems/linked-list-cycle-ii/description/)
```python
{
    class Solution(object):
        def detectCycle(self, head):
            """
            :type head: ListNode
            :rtype: ListNode
            """

            dummy_head = ListNode(next = head)
            slow = dummy_head
            fast = dummy_head

            while fast.next and fast.next.next:
                fast = fast.next.next
                slow = slow.next
                if fast == slow:
                    slow = dummy_head
                    while slow != fast:
                        fast = fast.next
                        slow = slow.next
                    return slow
            return None

}
```

## 总结
总是用dummy_head， 多画图，多检查边界条件
