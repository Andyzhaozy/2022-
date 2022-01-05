

#**1.5 每日一题**

#### [1576. 替换所有的问号](https://leetcode-cn.com/problems/replace-all-s-to-avoid-consecutive-repeating-characters/)

难度简单73收藏分享切换为英文接收动态反馈

给你一个仅包含小写英文字母和 `'?'` 字符的字符串 `s`，请你将所有的 `'?'` 转换为若干小写字母，使最终的字符串不包含任何 **连续重复** 的字符。

注意：你 **不能** 修改非 `'?'` 字符。

题目测试用例保证 **除** `'?'` 字符 **之外**，不存在连续重复的字符。

在完成所有转换（可能无需转换）后返回最终的字符串。如果有多个解决方案，请返回其中任何一个。可以证明，在给定的约束条件下，答案总是存在的。

 

**示例 1：**

```
输入：s = "?zs"
输出："azs"
解释：该示例共有 25 种解决方案，从 "azs" 到 "yzs" 都是符合题目要求的。只有 "z" 是无效的修改，因为字符串 "zzs" 中有连续重复的两个 'z' 。
```

**示例 2：**

```
输入：s = "ubv?w"
输出："ubvaw"
解释：该示例共有 24 种解决方案，只有替换成 "v" 和 "w" 不符合题目要求。因为 "ubvvw" 和 "ubvww" 都包含连续重复的字符。
```

**示例 3：**

```
输入：s = "j?qg??b"
输出："jaqgacb"
```

**示例 4：**

```
输入：s = "??yw?ipkj?"
输出："acywaipkja"
```

 

**提示：**

- `1 <= s.length <= 100`
- `s` 仅包含小写英文字母和 `'?'` 字符





## 第一次尝试

~~~python
class Solution:
    def modifyString(self, s: str) -> str:
        length = len(s)
        s = "?" + s + "?" 
        insert = 97
        result = "?"
        for i in range(1, length + 1):
            if s[i] == '?':
                while (chr(insert) == result[i - 1] or chr(insert) == s[i + 1]):
                    insert += 1
                    if insert > 122:
                        insert = 97
                result += chr(insert)
            else:
                result += s[i]
        return result[1:]

~~~

哎, 简单题也写错了三四次, 还是要仔细啊





执行结果：

通过

显示详情

执行用时：32 ms, 在所有 Python3 提交中击败了77.95%的用户

内存消耗：15 MB, 在所有 Python3 提交中击败了46.67%的用户

通过测试用例：776 / 776

炫耀一下:

写题解，分享我的解题思路

| 提交结果                                                     | 执行用时 | 内存消耗 | 语言    | 提交时间         | 备注     |
| :----------------------------------------------------------- | :------- | :------- | :------ | :--------------- | :------- |
| [通过](https://leetcode-cn.com/submissions/detail/255190457/) | 32 ms    | 15 MB    | Python3 | 2022/01/05 14:50 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/255189945/) | N/A      | N/A      | Python3 | 2022/01/05 14:46 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/255188391/) | N/A      | N/A      | Python3 | 2022/01/05 14:43 | 添加备注 |