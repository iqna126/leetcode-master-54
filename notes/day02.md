# 第一章  数组part02

今日任务： 209.长度最小的子数组, 59.螺旋矩阵II, 区间和  
附加: 开发商购买土地

文章和题目详解都在[代码随想录](https://programmercarl.com/)  
视频讲解指路卡哥[b站合集](https://space.bilibili.com/525438321/channel/collectiondetail?sid=180037)

## 209. [长度最小的子数组](https://leetcode.com/problems/minimum-size-subarray-sum/description/)
```python
{
    class Solution(object):
        def minSubArrayLen(self, target, nums):
            """
            :type target: int
            :type nums: List[int]
            :rtype: int
            """
            left, right, cur, length = 0, 0, 0, float('inf')
            while right < len(nums):
                cur += nums[right]
                while cur >= target:
                    length = min(length, right -left +1)
                    cur -= nums[left]
                    left += 1
                right += 1
            return length if length != float('inf') else 0
}
```

## 59. [螺旋矩阵II](https://leetcode.com/problems/spiral-matrix-ii/description/)
```python
{
    class Solution(object):
        def generateMatrix(self, n):
            """
            :type n: int
            :rtype: List[List[int]]
            """
            res = [[0] * n for _ in range(n)]
            left, right, top, bottom = 0, n-1, 0, n-1
            fill_value = 1
            while left <= right and top <= bottom:
                
                for i in range(left, right+1):
                    res[top][i] = fill_value
                    fill_value += 1 
                top +=1 

                for i in range(top, bottom+1):
                    res[i][right] = fill_value
                    fill_value += 1
                right -= 1 

                for i in range(right, left-1, -1):
                    res[bottom][i] = fill_value
                    fill_value += 1
                bottom -= 1

                for i in range(bottom, top-1, -1):
                    res[i][left] = fill_value
                    fill_value += 1 
                left += 1
            return res
                
                

}
```

## [区间和](https://www.programmercarl.com/kamacoder/0058.%E5%8C%BA%E9%97%B4%E5%92%8C.html)
题目描述: 给定一个整数数组 Array，请计算该数组在每个指定区间内元素的总和。  
输入描述: 第一行输入为整数数组 Array 的长度 n，接下来 n 行，每行一个整数，表示数组的元素。随后的输入为需要计算总和的区间，直至文件结束。  
输出描述: 输出每个指定区间内元素的总和。  
```python
{
    import sys
    input = sys.stdin.read
    def main():
        data = input().split()
        position = 0
        n = int(data[position])
        position += 1
        vec = []
        while position <= n:
            vec.append(int(data[position]))
            position += 1

        pre_sum_vec = [0] * n
        pre_sum = 0
        for i in range(n):
            pre_sum += vec[i]
            pre_sum_vec[i] = pre_sum

        results = []
        while position < len(data):
            a = int(data[position])
            b = int(data[position+1])
            if a == 0:
                value = pre_sum_vec[b]
            else:
                value = pre_sum_vec[b] - pre_sum_vec[a-1]
            results.append(value)
            position += 2

        for res in results:
            print(res)
    
    if __name__ == "__main__":
        main()

}
```

## [开发商购买土地](https://www.programmercarl.com/kamacoder/0044.%E5%BC%80%E5%8F%91%E5%95%86%E8%B4%AD%E4%B9%B0%E5%9C%9F%E5%9C%B0.html)
题目描述: 在一个城市区域内，被划分成了n * m个连续的区块，每个区块都拥有不同的权值，代表着其土地价值。目前，有两家开发公司，A 公司和 B 公司，希望购买这个城市区域的土地。现在，需要将这个城市区域的所有区块分配给 A 公司和 B 公司。然而，由于城市规划的限制，只允许将区域按横向或纵向划分成两个子区域，而且每个子区域都必须包含一个或多个区块。  
为了确保公平竞争，你需要找到一种分配方式，使得 A 公司和 B 公司各自的子区域内的土地总价值之差最小。  
输入描述: 第一行输入两个正整数，代表 n 和 m。 接下来的 n 行，每行输出 m 个正整数。  
输出描述: 请输出一个整数，代表两个子区域内土地总价值之间的最小差距。  
```python
{
    import sys
    input = sys.stdin.read
    def main():
        data = input().split()
        position = 0
        n = int(data[position])
        position += 1
        m = int(data[position])
        position += 1
        sum = 0
        vec = []
        for i in range(n):
            row = []
            for j in range(m):
                num = int(data[position])
                position += 1
                row.append(num)
                sum += num
            vec.append(row)

        # 统计横向
        horizontal = [0] * n
        for i in range(n):
            for j in range(m):
                horizontal[i] += vec[i][j]

        # 统计纵向
        vertical = [0] * m
        for j in range(m):
            for i in range(n):
                vertical[j] += vec[i][j]

        result = float('inf')
        horizontalCut = 0
        for i in range(n):
            horizontalCut += horizontal[i]
            result = min(result, abs(sum - 2 * horizontalCut))

        verticalCut = 0
        for j in range(m):
            verticalCut += vertical[j]
            result = min(result, abs(sum - 2 * verticalCut))

        print(result)

    if __name__ == "__main__":
        main()
}
```