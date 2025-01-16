# 第四章  字符串part01 

今日任务： 344.反转字符串， 541. 反转字符串II， 卡码网：54.替换数字

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)


## 344.[反转字符串](https://leetcode.com/problems/reverse-string/description/)
```python
{
    class Solution(object):
        def reverseString(self, s):
            """
            :type s: List[str]
            :rtype: None Do not return anything, modify s in-place instead.
            """
            front, end = 0, len(s)-1
            while front < end:
                s[front], s[end] = s[end], s[front]
                front += 1 
                end -= 1
            

}
```

## 541.[反转字符串II](https://leetcode.com/problems/reverse-string-ii/description/) 
```python
{
    class Solution(object):
        def reverseStr(self, s, k):
            """
            :type s: str
            :type k: int
            :rtype: str
            """
            
            s_list = list(s)
            count = 0 
            front = 0
            while front < len(s):
                front, end = count * 2 * k, min((count * 2 + 1)* k -1,len(s)-1)
                while front < end:
                    s_list[front], s_list[end] = s_list[end], s_list[front]
                    front += 1
                    end -= 1
                count += 1
                front, end = count * 2 * k, (count * 2 + 1) * k -1
            return "".join(s_list)         

}
```

## 卡码网：54.[替换数字](https://programmercarl.com/kamacoder/0054.%E6%9B%BF%E6%8D%A2%E6%95%B0%E5%AD%97.html) 
```python
{
    class Solution(object):
        def subsitute_numbers(self, s):
            """
            :type s: str
            :rtype: str
            """
            
            count = sum(1 for char in s if char.isdigit()) # 统计数字的个数
            expand_len = len(s) + (count * 5)  # 计算扩充后字符串的大小， x->number， 每有一个数字就要增加五个长度
            res = [''] * expand_len
            
            new_index = expand_len - 1 # 指向扩充后字符串末尾
            old_index = len(s) - 1 # 指向原字符串末尾
            
            while old_index >= 0: # 从后往前， 遇到数字替换成“number”
                if s[old_index].isdigit():
                    res[new_index-5:new_index+1] = "number"
                    new_index -= 6
                else:
                    res[new_index] = s[old_index]
                    new_index -= 1
                old_index -= 1
            
            return "".join(res)
            
    if __name__ == "__main__":
        solution = Solution()

        while True:
            try:
                s = input()
                result = solution.subsitute_numbers(s)
                print(result)
            except EOFError:
                break        

}
```