# **1.10 每日一题**

#### [306. 累加数](https://leetcode-cn.com/problems/additive-number/)

难度中等274收藏分享切换为英文接收动态反馈

**累加数** 是一个字符串，组成它的数字可以形成累加序列。

一个有效的 **累加序列** 必须 **至少** 包含 3 个数。除了最开始的两个数以外，字符串中的其他数都等于它之前两个数相加的和。

给你一个只包含数字 `'0'-'9'` 的字符串，编写一个算法来判断给定输入是否是 **累加数** 。如果是，返回 `true` ；否则，返回 `false` 。

**说明：**累加序列里的数 **不会** 以 0 开头，所以不会出现 `1, 2, 03` 或者 `1, 02, 3` 的情况。

 

**示例 1：**

```
输入："112358"
输出：true 
解释：累加序列为: 1, 1, 2, 3, 5, 8 。1 + 1 = 2, 1 + 2 = 3, 2 + 3 = 5, 3 + 5 = 8
```

**示例 2：**

```
输入："199100199"
输出：true 
解释：累加序列为: 1, 99, 100, 199。1 + 99 = 100, 99 + 100 = 199
```

 

**提示：**

- `1 <= num.length <= 35`
- `num` 仅由数字（`0` - `9`）组成

 

**进阶：**你计划如何处理由过大的整数输入导致的溢出?





## 第一次尝试

~~~python
class Solution:
    def isAdditiveNumber(self, num: str) -> bool:
        ## 先找到开头合法的
        if len(num) < 3:
            return False
        else:
            first = 1
            second = 1
            result = int(num[:first]) + int(num[first:first+second])
            third = int(num[first+second : first+second+len(str(result))])
            while first < len(num) - 1:
                if result == third:
                    final = ""
                    final += num[:first+second]
                    last = int(num[first:first+second])
                    curr = int(num[first+second : first+second+len(str(result))])
                    while len(final) < len(num):
                        final += str(curr)
                        last,curr = curr, last + curr
                    if num == final:
                        return True
                second += 1
                if second >= len(num) - 1 or num[first:first+second].startswith('0'):
                    first += 1
                    second = 1
                if num[0].startswith('0') and first > 1:
                    return False
                result = int(num[ : first]) + int(num[first : first + second])
                if first + second >= len(num):
                    first += 1
                    second = 1
                    if first >= len(num):
                        return False
                    result = int(num[ : first]) + int(num[first : first + second])
                if first + second >= len(num):
                    return False
                third = int(num[first + second : first + second + len(str(result))])
            return False
~~~

思路没有问题,但是很多细节就是没有考虑到.整整一下午才写出来.

不过写出 Mid 题,还是蛮有成就感的

添加备注

执行用时：28 ms, 在所有 Python3 提交中击败了94.63%的用户

内存消耗：14.8 MB, 在所有 Python3 提交中击败了87.58%的用户

通过测试用例：42 / 42

炫耀一下:











写题解，分享我的解题思路

| 提交结果                                                     | 执行用时 | 内存消耗 | 语言    | 提交时间         | 备注     |
| :----------------------------------------------------------- | :------- | :------- | :------ | :--------------- | :------- |
| [通过](https://leetcode-cn.com/submissions/detail/256985826/) | 28 ms    | 14.8 MB  | Python3 | 2022/01/10 22:09 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/256985755/) | N/A      | N/A      | Python3 | 2022/01/10 17:44 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/256984117/) | 40 ms    | 15 MB    | Python3 | 2022/01/10 17:44 | 添加备注 |
| [执行出错](https://leetcode-cn.com/submissions/detail/256983536/) | N/A      | N/A      | Python3 | 2022/01/10 17:42 | 添加备注 |
| [执行出错](https://leetcode-cn.com/submissions/detail/256982501/) | N/A      | N/A      | Python3 | 2022/01/10 17:39 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/256979831/) | N/A      | N/A      | Python3 | 2022/01/10 17:32 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/256978823/) | N/A      | N/A      | Python3 | 2022/01/10 17:30 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/256978436/) | N/A      | N/A      | Python3 | 2022/01/10 17:29 | 添加备注 |
| [执行出错](https://leetcode-cn.com/submissions/detail/256975263/) | N/A      | N/A      | Python3 | 2022/01/10 17:21 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/256974083/) | N/A      | N/A      | Python3 | 2022/01/10 17:18 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/256973526/) | N/A      | N/A      | Python3 | 2022/01/10 17:17 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/256951260/) | 40 ms    | 15.2 MB  | Python3 | 2022/01/10 16:29 | 添加备注 |
| [执行出错](https://leetcode-cn.com/submissions/detail/256951179/) | N/A      | N/A      | Python3 | 2022/01/10 16:29 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/256949610/) | N/A      | N/A      | Python3 | 2022/01/10 16:26 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/256948242/) | N/A      | N/A      | Python3 | 2022/01/10 16:23 | 添加备注 |
| [超出时间限制](https://leetcode-cn.com/submissions/detail/256879535/) | N/A      | N/A      | Python3 | 2022/01/10 13:35 | 添加备注 |
| [执行出错](https://leetcode-cn.com/submissions/detail/256878840/) | N/A      | N/A      | Python3 | 2022/01/10 13:33 | 添加备注 |
| [执行出错](https://leetcode-cn.com/submissions/detail/256878476/) | N/A      | N/A      | Python3 | 2022/01/10 13:32 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/256873874/) | N/A      | N/A      | Python3 | 2022/01/10 13:10 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/256873431/) | N/A      | N/A      | Python3 | 2022/01/10 13:08 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/187361182/) | 40 ms    | 15 MB    | Python3 | 2021/06/17 10:02 | 添加备注 |

对了,好像还有整数溢出没有考虑到.