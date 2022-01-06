

#**1.6 每日一题**

#### [71. 简化路径](https://leetcode-cn.com/problems/simplify-path/)

难度中等407收藏分享切换为英文接收动态反馈

给你一个字符串 `path` ，表示指向某一文件或目录的 Unix 风格 **绝对路径** （以 `'/'` 开头），请你将其转化为更加简洁的规范路径。

在 Unix 风格的文件系统中，一个点（`.`）表示当前目录本身；此外，两个点 （`..`） 表示将目录切换到上一级（指向父目录）；两者都可以是复杂相对路径的组成部分。任意多个连续的斜杠（即，`'//'`）都被视为单个斜杠 `'/'` 。 对于此问题，任何其他格式的点（例如，`'...'`）均被视为文件/目录名称。

请注意，返回的 **规范路径** 必须遵循下述格式：

- 始终以斜杠 `'/'` 开头。
- 两个目录名之间必须只有一个斜杠 `'/'` 。
- 最后一个目录名（如果存在）**不能** 以 `'/'` 结尾。
- 此外，路径仅包含从根目录到目标文件或目录的路径上的目录（即，不含 `'.'` 或 `'..'`）。

返回简化后得到的 **规范路径** 。

 

**示例 1：**

```
输入：path = "/home/"
输出："/home"
解释：注意，最后一个目录名后面没有斜杠。 
```

**示例 2：**

```
输入：path = "/../"
输出："/"
解释：从根目录向上一级是不可行的，因为根目录是你可以到达的最高级。
```

**示例 3：**

```
输入：path = "/home//foo/"
输出："/home/foo"
解释：在规范路径中，多个连续斜杠需要用一个斜杠替换。
```

**示例 4：**

```
输入：path = "/a/./b/../../c/"
输出："/c"
```

 

**提示：**

- `1 <= path.length <= 3000`
- `path` 由英文字母，数字，`'.'`，`'/'` 或 `'_'` 组成。
- `path` 是一个有效的 Unix 风格绝对路径。

## 第一次尝试

**46 / 256** 个通过测试用例

状态：*解答错误*

提交时间：**1 小时前**

最后执行的输入：

"/a/../../b/../c//.//"

------

#### 提交的代码： 1 小时前

语言： python3



添加备注

编辑代码

```python
class Solution:
    def simplifyPath(self, path: str) -> str:
        result = path.strip().split("/")
        final = ""
        print(result)
        for i in range(1, len(result)-1):
            if result[i] == '':
                continue
            else:
                final += '/'
            if result[i] == '.':
                final = final[:-1]
                continue
            elif result[i] == '..':
                print(final)
                index = len(final) - 2
                if index < 0:
                    if final == "/":
                        return "/"
                    return final[:index + 1]
                print(index)
                while index > 0 and final[index] != '/':
                    index -= 1
                final = final[:index]
                print(final)
            else:
                final += result[i]
        return final
                
```

一开始尝试用 str 去完成, 好像这个思路需要考虑的边界条件比较多, 但是想的东西还是不太周全, 缝缝补补还是有一些没有考虑到的地方, 死在了第 146 个例子.



## 第二次尝试

~~~python
class Solution:
    def simplifyPath(self, path: str) -> str:
        names = path.split("/")
        print(names)
        result = []
        for i in names:
            if i == "..":
                if result:
                    result.pop()
            elif i and i != '.':
                result.append(i)
        print(result)
        return "/" + "/".join(result)
~~~

执行用时：28 ms, 在所有 Python3 提交中击败了93.29%的用户

内存消耗：15.1 MB, 在所有 Python3 提交中击败了12.28%的用户

通过测试用例：256 / 256



| 提交结果                                                     | 执行用时 | 内存消耗 | 语言    | 提交时间         | 备注     |
| :----------------------------------------------------------- | :------- | :------- | :------ | :--------------- | :------- |
| [通过](https://leetcode-cn.com/submissions/detail/255725922/) | 28 ms    | 15.1 MB  | Python3 | 2022/01/06 21:29 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/255725854/) | 32 ms    | 15.3 MB  | Python3 | 2022/01/06 21:27 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/255725804/) | 36 ms    | 15.2 MB  | Python3 | 2022/01/06 21:27 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/255725776/) | 36 ms    | 15.1 MB  | Python3 | 2022/01/06 21:27 | 添加备注 |
| [通过](https://leetcode-cn.com/submissions/detail/255721727/) | 28 ms    | 15.2 MB  | Python3 | 2022/01/06 21:16 | 添加备注 |
| [解答错误](https://leetcode-cn.com/submissions/detail/255695948/) | N/A      | N/A      | Python3 | 2022/01/06 20:11 | 添加备注 |

果然虽然这题不是特别难, 但是看了题解之后发现的确 list 是一个更好的思路,可以更简单的解决一些边界条件,还是要开阔自己的思路啊. 加油!!!

顺便复习了下.join()函数

## 描述

Python join() 方法用于将序列中的元素以指定的字符连接生成一个新的字符串。

## 语法

join()方法语法：

```
str.join(sequence)
```

## 参数

- sequence -- 要连接的元素序列。

## 返回值

返回通过指定字符连接序列中元素后生成的新字符串。

## 实例

以下实例展示了join()的使用方法：

## 实例(Python 2.0+)

\#!/usr/bin/python # -*- coding: UTF-8 -*-  str = "-"; seq = ("a", "b", "c"); # 字符串序列 print str.join( seq );

以上实例输出结果如下：

```python
a-b-c
```

哈哈哈,还有学到东西的一天!!