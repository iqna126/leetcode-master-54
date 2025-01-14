# 第三章  哈希表part01 

今日任务: 哈希表理论基础, 242.有效的字母异位词, 349.两个数组的交集, 202.快乐数, 1.两数之和  

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 哈希表(Hash table)理论基础
**当我们遇到了要快速判断一个元素是否出现集合里的时候，就要考虑哈希法。**
### 常见的三种哈希结构
1. 数组
2. 集合（set）
3. 映射（map）
python中的dict


## 242.[有效的字母异位词](https://leetcode.com/problems/valid-anagram/description/) 
```python
{
    class Solution(object):
        def isAnagram(self, s, t):
            """
            :type s: str
            :type t: str
            :rtype: bool
            """
            res = [0] * 26
            for i in s:
                res[ord(i)-ord("a")] += 1 # i 不加引号因为i本身就是s里面的每一个字符
            for i in t:
                res[ord(i)-ord("a")] -= 1
            
            for i in range(26):
                if res[i] != 0:
                    return False
            return True


}
```

## 349.[两个数组的交集](https://leetcode.com/problems/intersection-of-two-arrays/description/) 
```python
{
    class Solution(object):
        def intersection(self, nums1, nums2):
            """
            :type nums1: List[int]
            :type nums2: List[int]
            :rtype: List[int]
            """
            return list(set(nums1) & set(nums2))

}
```

## 202.[快乐数](https://leetcode.com/problems/happy-number/description/) 
```python
{
    class Solution(object):
        def isHappy(self, n):
            """
            :type n: int
            :rtype: bool
            """

            def process(n):
                res = 0
                while n:
                    n, r = divmod(n,10)
                    res += r**2
                return res
            
            record_sum = set()
            while n != 1:
                n = process(n)
                if n in record_sum:
                    return False
                record_sum.add(n)
            return True

}
```

## 1.[两数之和](https://leetcode.com/problems/two-sum/description/) 
```python
{
    class Solution(object):
        def twoSum(self, nums, target):
            """
            :type nums: List[int]
            :type target: int
            :rtype: List[int]
            """
            store_nums = {}
            for i in range(len(nums)):
                search = target - nums[i]
                if search in store_nums: #　每个数只能用一次， 但是给的数组里可能有两个一样的数
                    return [i, store_nums[search]]
                else:
                    store_nums[nums[i]] = i
            
}
```