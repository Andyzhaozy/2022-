# 1.12 每日一题

#### [334. 递增的三元子序列](https://leetcode-cn.com/problems/increasing-triplet-subsequence/)

难度中等453

给你一个整数数组 `nums` ，判断这个数组中是否存在长度为 `3` 的递增子序列。

如果存在这样的三元组下标 `(i, j, k)` 且满足 `i < j < k` ，使得 `nums[i] < nums[j] < nums[k]` ，返回 `true` ；否则，返回 `false`。

 

**示例 1：**

```
输入：nums = [1,2,3,4,5]
输出：true
解释：任何 i < j < k 的三元组都满足题意
```

**示例 2：**

```
输入：nums = [5,4,3,2,1]
输出：false
解释：不存在满足题意的三元组
```

**示例 3：**

```
输入：nums = [2,1,5,0,4,6]
输出：true
解释：三元组 (3, 4, 5) 满足题意，因为 nums[3] == 0 < nums[4] == 4 < nums[5] == 6
```

 

**提示：**

- `1 <= nums.length <= 5 * 105`
- `-231 <= nums[i] <= 231 - 1`

 

**进阶：**你能实现时间复杂度为 `O(n)` ，空间复杂度为 `O(1)` 的解决方案吗？





## 第一种方法

~~~python
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        if len(nums) < 3:
            return False
        length = len(nums)
        left = [0 for i in range(length)]
        left[0] = nums[0]
        for i in range(1, length):
            left[i] = min(left[i-1], nums[i])
        right = [0 for i in range(length)]
        right[length - 1] = nums[length - 1]
        for i in range(length - 2, -1, -1):
            right[i] = max(nums[i], right[i + 1])
        for i in range(1, length - 1):
            if left[i - 1] < nums[i] and nums[i] < right[i + 1]:
                return True
        return False
~~~

这种方法就额外在创建 两个 数组 

一个储存 左边最小值

一个储存 右边最大值

然后和 num 比较



## 第二个方法

~~~python
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        if len(nums) < 3:
            return False
        first = float('inf')
        second = float('inf')
        for i in nums:
            if i < first:
                first = i
            elif i > first:
                if i > second:
                    return True
                elif i < second:
                    second = i
        return False
~~~

这个方法超级机智 ***贪心***

一开始迷迷糊糊想出来的, 但觉得是错的,结果是对的,太离谱了

![](/Users/andy/Desktop/2022-/January/Screen Shot 2022-01-12 at 9.05.35 PM.png)

执行结果：

通过

显示详情



添加备注

执行用时：76 ms, 在所有 Python3 提交中击败了41.17%的用户

内存消耗：23.9 MB, 在所有 Python3 提交中击败了88.69%的用户

通过测试用例：76 / 76

炫耀一下:











写题解，分享我的解题思路

| 提交结果                                                     | 执行用时 | 内存消耗 | 语言    | 提交时间         | 备注     |
| :----------------------------------------------------------- | :------- | :------- | :------ | :--------------- | :------- |
| [通过](https://leetcode-cn.com/submissions/detail/257676586/) | 76 ms    | 23.9 MB  | Python3 | 2022/01/12 21:06 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/257668473/) | 268 ms   | 27.5 MB  | Python3 | 2022/01/12 16:05 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/257664921/) | 56 ms    | 23.9 MB  | Python3 | 2022/01/12 15:58 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/257657027/) | N/A      | N/A      | Python3 | 2022/01/12 15:42 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/257651839/) | 60 ms    | 23.9 MB  | Python3 | 2022/01/12 15:31 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/257650963/) | 68 ms    | 23.8 MB  | Python3 | 2022/01/12 15:30 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/257637213/) | N/A      | N/A      | Python3 | 2022/01/12 15:02 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/257602270/) | N/A      | N/A      | Python3 | 2022/01/12 13:23 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/257601947/) | N/A      | N/A      | Python3 | 2022/01/12 13:22 | 添加备注 |
| [超出时间限制](https://leetcode-cn.com/submissions/detail/257601851/) | N/A      | N/A      | Python3 | 2022/01/12 13:22 | 添加备注 |