# 1.11 每日一题

今天的每日一题是 hard , 看了下没什么思路就没有浪费时间了,就随机一题

#### [215. 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

难度中等1445收藏分享切换为英文接收动态反馈

给定整数数组 `nums` 和整数 `k`，请返回数组中第 `**k**` 个最大的元素。

请注意，你需要找的是数组排序后的第 `k` 个最大的元素，而不是第 `k` 个不同的元素。

 

**示例 1:**

```
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```

**示例 2:**

```
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

 

**提示：** 

- `1 <= k <= nums.length <= 104`
- `-104 <= nums[i] <= 104`

## 第一次尝试

~~~python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        ## 手写排序, 没有用 random 选择 pivot
        def partion(lst, left, right):
            pivot = lst[left]
            while left < right:
                while left < right and lst[right] >= pivot:
                    right -= 1
                lst[left] = lst[right]
                while left < right and lst[left] <= pivot:
                    left += 1
                lst[right] = lst[left]
            lst[left] = pivot
            return left
        def quicksort(lst, left = None, right = None):
            if not isinstance(left, int):
                left = 0
            if not isinstance(right, int):
                right = len(lst) - 1
            
            if left < right:
                partionIndex = partion(lst, left, right)
                quicksort(lst, left, partionIndex - 1)
                quicksort(lst, partionIndex + 1, right)
            return lst
        return result[len(result) - k]

~~~

思路不难,一开始直接使用库函数,但是感觉如果是面试有点不尊重面试官又写了一个快速排序,但是效率低了好多.

执行结果：

通过

显示详情



添加备注

执行用时：2908 ms, 在所有 Python3 提交中击败了5.90%的用户

内存消耗：21 MB, 在所有 Python3 提交中击败了6.69%的用户

通过测试用例：32 / 32

炫耀一下:











写题解，分享我的解题思路

| 提交结果                                                     | 执行用时 | 内存消耗 | 语言    | 提交时间         | 备注     |
| :----------------------------------------------------------- | :------- | :------- | :------ | :--------------- | :------- |
| [通过](https://leetcode-cn.com/submissions/detail/257420086/) | 2908 ms  | 21 MB    | Python3 | 2022/01/11 22:02 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/257420041/) | 2952 ms  | 20.9 MB  | Python3 | 2022/01/11 21:25 | 添加备注 |
| [超出时间限制](https://leetcode-cn.com/submissions/detail/257419023/) | N/A      | N/A      | Python3 | 2022/01/11 21:23 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/257283163/) | 40 ms    | 15.5 MB  | Python3 | 2022/01/11 15:28 | 添加备注 |