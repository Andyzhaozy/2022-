# 1.13 每日一题

#### [747. 至少是其他数字两倍的最大数](https://leetcode-cn.com/problems/largest-number-at-least-twice-of-others/)

难度简单135收藏分享切换为英文接收动态反馈

给你一个整数数组 `nums` ，其中总是存在 **唯一的** 一个最大整数 。

请你找出数组中的最大元素并检查它是否 **至少是数组中每个其他数字的两倍** 。如果是，则返回 **最大元素的下标** ，否则返回 `-1` 。

 

**示例 1：**

```
输入：nums = [3,6,1,0]
输出：1
解释：6 是最大的整数，对于数组中的其他整数，6 大于数组中其他元素的两倍。6 的下标是 1 ，所以返回 1 。
```

**示例 2：**

```
输入：nums = [1,2,3,4]
输出：-1
解释：4 没有超过 3 的两倍大，所以返回 -1 。
```

**示例 3：**

```
输入：nums = [1]
输出：0
解释：因为不存在其他数字，所以认为现有数字 1 至少是其他数字的两倍。
```

 

**提示：**

- `1 <= nums.length <= 50`
- `0 <= nums[i] <= 100`
- `nums` 中的最大元素是唯一的

通过次数66,330

提交次数147,551



## 第一次尝试

~~~python
class Solution:
    def dominantIndex(self, nums: List[int]) -> int:
        currentmax = 0
        secondmax = 0
        length = len(nums)
        if length < 2:
            return 0
        for i in range(length):
            if nums[i] > nums[currentmax]:
                secondmax = currentmax
                currentmax = i
            elif nums[i] < nums[currentmax]:
                if nums[i] > nums[secondmax] or currentmax == secondmax:
                    secondmax = i
        if nums[currentmax] >= (2 * nums[secondmax]):
            return currentmax
        return -1
                
~~~

简单题,思路很清晰. 一次循环,保存最大的两个值就可以了.效率也不错