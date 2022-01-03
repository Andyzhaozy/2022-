# leetcode 1.3 每日一题

#### [1185. 一周中的第几天](https://leetcode-cn.com/problems/day-of-the-week/)

难度简单71收藏分享切换为英文接收动态反馈

给你一个日期，请你设计一个算法来判断它是对应一周中的哪一天。

输入为三个整数：`day`、`month` 和 `year`，分别表示日、月、年。

您返回的结果必须是这几个值中的一个 `{"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"}`。

 

**示例 1：**

```
输入：day = 31, month = 8, year = 2019
输出："Saturday"
```

**示例 2：**

```
输入：day = 18, month = 7, year = 1999
输出："Sunday"
```

**示例 3：**

```
输入：day = 15, month = 8, year = 1993
输出："Sunday"
```

 

**提示：**

- 给出的日期一定是在 `1971` 到 `2100` 年之间的有效日期。





## 第一次尝试

查日历可以得知1970.12.31 日是周四

~~~python
class Solution:
    def dayOfTheWeek(self, day: int, month: int, year: int) -> str:
        total_days = 0
        months = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
        for i in range(1971, year):
            if (i % 4 == 0 and i % 100 != 0) or i % 400 == 0: ## 判断是否是闰年
                total_days += 366
            else:
                total_days += 365
        for i in range(1, month):
            if i == 2 and ((year % 4 == 0 and year % 100 != 0) or year % 400 == 0):
                total_days += 29
            else:
                total_days += months[i-1]
        total_days += day - 1
        result = ["Friday", "Saturday", "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday"]
        return result[total_days % 7]
~~~



执行用时：28 ms, 在所有 Python3 提交中击败了89.88%的用户

内存消耗：15.1 MB, 在所有 Python3 提交中击败了17.49%的用户

通过测试用例：43 / 43

比较傻的方法, 模拟日期



额外思路 ———— 蔡勒公式



