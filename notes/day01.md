# 第一章  数组part01 

今日任务：数组理论基础，704. 二分查找，27. 移除元素, 977.有序数组的平方  
附加: 35.搜索插入位置 和 34. 在排序数组中查找元素的第一个和最后一个位置

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 数组理论基础  
数组的存储： 数组是存放在**连续内存空间**上的**相同类型**数据的集合 --> 删除或者增添元素的时候，要移动其他元素的地址，覆盖对应的元素  

数组的获取： 数组通过下标索引的方式获取到下标对应的数据（**从0开始的**）。


## 704. [二分查找](https://leetcode.com/problems/binary-search/description/) 
左闭右开  
```python
{
  class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left, right = 0, len(nums)
        while left < right:
          middle = (left + right) // 2
          if nums[middle] > target:
            right  = middle
          elif nums[middle] < target:
            left = middle +1
          else:
            return middle
        return -1
}
```

左闭右闭  
```python
{
  class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left, right = 0, len(nums)-1
        while left <= right:
          middle = (left + right) // 2
          if nums[middle] > target:
            right = middle - 1
          elif nums[middle] < target:
            left = middle + 1
          else:
            return middle
        return -1 
}
```



## 27. [移除元素](https://leetcode.com/problems/remove-element/description/)
暴力解法  
```python
{
  class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
}
```

双指针法   
```python
{
  class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
}
```



## 977.[有序数组的平方](https://leetcode.com/problems/squares-of-a-sorted-array/description/) 
双指针法  
```python
{
  class Solution(object):
      def sortedSquares(self, nums):
          """
          :type nums: List[int]
          :rtype: List[int]
          """
          
}
```

## 35.[搜索插入位置]()
双指针法  
```python
{
  class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """

}
```


## 34. [在排序数组中查找元素的第一个和最后一个位置](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
```python
{
  class Solution(object):
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
}
```

