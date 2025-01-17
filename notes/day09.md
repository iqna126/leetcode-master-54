# 第四章  字符串part02

今日任务： 151.翻转字符串里的单词， 卡码网： 55.右旋转字符串， 28.实现 strStr()， 459.重复的子字符串， 字符串总结， 双指针回顾

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 151.[翻转字符串里的单词](https://leetcode.com/problems/reverse-words-in-a-string/description/)
```python
{
    class Solution(object):
        def reverseWords(self, s):
            """
            :type s: str
            :rtype: str
            """
            words = s.split()
            left, right = 0, len(words) - 1
            while left < right:
                words[left], words[right] = words[right], words[left]
                left += 1
                right -= 1
    
            return " ".join(words)
            

}
```

## 卡码网55.[右旋转字符串](https://programmercarl.com/kamacoder/0055.%E5%8F%B3%E6%97%8B%E5%AD%97%E7%AC%A6%E4%B8%B2.html)
```python
{
    class Solution(object):
        def right_turn_string(self, k, s):
            """
            :type k: int
            :type s: string
            :rtype res: string
            """
            res = s[-k:] + s[:-k]
            return res
            
    if __name__ == "__main__":
        solution = Solution()

        while True:
            try:
                k = int(input())
                s = input()
                result = solution.right_turn_string(k, s)
                print(result)
            except EOFError:
                break     


}
```

## 28.[实现 strStr()](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/)
```python
{
    class Solution(object):
        def getNext(self, Next, s):
            Next[0] = 0
            j = 0
            for i in range(1,len(s)):
                while j > 0 and s[j] != s[i]:
                    j = Next[j-1]
                if s[j] == s[i]:
                    j += 1 
                Next[i] = j

        def strStr(self, haystack, needle):
            """
            :type haystack: str
            :type needle: str
            :rtype: int
            """
            if len(needle) == 0: # 注意判断needle为空的情况
                return 0
            Next = [0] * len(needle)
            self.getNext(Next, needle)
            j = 0
            for i in range(len(haystack)):
                while j > 0 and haystack[i] != needle[j]:
                    j = Next[j-1]
                if haystack[i] == needle[j]:
                    j += 1
                if j == len(needle):
                    return i-j+1
            return -1
            

}
```

## 459.[重复的子字符串](https://leetcode.com/problems/repeated-substring-pattern/description/)
```python
{
    class Solution(object):
        def repeatedSubstringPattern(self, s):
            """
            :type s: str
            :rtype: bool
            """
            n = len(s)
            if n <= 1:
                return False
            ss = s[1:]+s[:-1]
            print(ss.find(s))
            return ss.find(s) != -1

            

}
```

## 字符串总结
### KMP算法
KMP的主要思想是当出现字符串不匹配时，可以知道一部分之前已经匹配的文本内容，可以利用这些信息避免从头再去做匹配了。  
理解前缀表的概念，和前缀表获得的代码。


## 双指针回顾
双指针的方法在很多时候可以提高代码的效率！