# 第三章  哈希表part01 

今日任务: 454.四数相加 II, 383.赎金信, 15.三数之和, 18.四数之和, 总结

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 454.[四数相加](https://leetcode.com/problems/4sum-ii/) 
```python
{
    class Solution(object):
        def fourSumCount(self, nums1, nums2, nums3, nums4):
            """
            :type nums1: List[int]
            :type nums2: List[int]
            :type nums3: List[int]
            :type nums4: List[int]
            :rtype: int
            """
            one_two_sum = {}
            for num1 in nums1:
                for num2 in nums2:
                    one_two_sum[num1+num2] = one_two_sum.get(num1+num2, 0)+1
            count = 0
            for num3 in nums3:
                for num4 in nums4:
                    if -num3-num4 in one_two_sum:
                        count += one_two_sum.get(-num3-num4,0)

            return count
            

}
```

## 383.[赎金信](https://leetcode.com/problems/ransom-note/description/) 
```python
{
    class Solution(object):
        def canConstruct(self, ransomNote, magazine):
            """
            :type ransomNote: str
            :type magazine: str
            :rtype: bool
            """
            store_note = {}
            for m in magazine:
                store_note[ord(m)-ord("a")] = store_note.get(ord(m)-ord("a"), 0)+1
            for s in ransomNote:
                temp = store_note.get(ord(s)-ord("a"),0)
                if temp ==0:
                    return False
                else:
                    store_note[ord(s)-ord("a")] = store_note.get(ord(s)-ord("a"))-1
            return True

}
```

## 15.[三数之和](https://leetcode.com/problems/3sum/description/) 
```python
{
    class Solution(object):
        def threeSum(self, nums):
            """
            :type nums: List[int]
            :rtype: List[List[int]]
            """

            nums.sort()
            res = []

            for i in range(len(nums)-2):
                #可以加入剪枝
                if nums[i]>0:
                    return res

                if i >0 and nums[i] == nums[i-1]:
                    continue
                
                left = i + 1
                right = len(nums) - 1
                while left < right:
                    total = nums[i] + nums[left] + nums[right]
                    if total <0:
                        left += 1
                    elif total >0:
                        right -= 1
                    else:
                        res.append([nums[i], nums[left], nums[right]])
                        left += 1
                        right -= 1
                        while left < right and nums[left] == nums[left-1]:
                            left += 1
                        while left < right and nums[right] == nums[right+1]:
                            right -= 1
            return res
            

}
```

## 18.[四数之和](https://leetcode.com/problems/4sum/description/) 
```python
{
    class Solution(object):
        def fourSum(self, nums, target):
            """
            :type nums: List[int]
            :type target: int
            :rtype: List[List[int]]
            """
            
            nums.sort()
            res = []

            for i in range(len(nums)-3):
                #可以加入剪枝
                if nums[i]>target and nums[i]>0:
                    return res
                if i > 0 and nums[i] == nums[i-1]:
                    continue
                for k in range(len(nums)-1,2,-1):
                    #可以加入剪枝
                    #和i的剪枝不同
                    if nums[k]+nums[i]+nums[k-1]+nums[k-2]<target:
                        break
                    if nums[k]+nums[i]+nums[i+1]+nums[i+2]>target:
                        continue
                    if k <len(nums)-1 and nums[k] == nums[k+1]:
                        continue

                    left = i+1
                    right = k-1
                    while left < right:
                        total = nums[i]+nums[k]+nums[left]+nums[right]            
                        if total > target:
                            right -= 1
                        elif total < target:
                            left +=1 
                        else: 
                            res.append([nums[i], nums[left], nums[right], nums[k]])  
                            left += 1
                            right -= 1 
                            while left< right and nums[left] == nums[left-1]:
                                left +=1
                            while left< right and nums[right] == nums[right+1]:
                                right -=1
            return res     



            
}
```

## 总结
### 哈希表的使用
一般来说哈希表都是用来快速判断一个元素是否出现集合里。  
1. 数组作为哈希表：需要**限制数值的大小**，数组的大小是有限的，受到系统栈空间（不是数据结构的栈）的限制。 而且如果哈希值比较少、特别分散、跨度非常大，使用数组就造成空间的极大浪费。（虽然也可以用map，但是这样会消耗更多空间，因为map要维护其底层实现方法（红黑树或者符号表），还需要做哈希函数的运算。）
2. set作为哈希表
3. map作为哈希表：有< key, value >的结构，本题可以用key保存数值，用value保存对应数值需要的其他信息。  
使用set和map要注意用到的数据结构的底层实现是什么。  
但是同样是判断元素出现在集合，但是需要考虑去重的情况的时候，要考虑哈希表是否依旧合适。
### 去重逻辑
要注意去重逻辑的写法，i++之后判断nums[i]==nums[i-1] 和 判断nums[i]==nums[i+1] continue的结果完全不同。
### 添加剪枝