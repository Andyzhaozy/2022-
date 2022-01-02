## leetcode 1.2 每日一题

> #### [390. 消除游戏](https://leetcode-cn.com/problems/elimination-game/)
>
> 
>
> 列表 `arr` 由在范围 `[1, n]` 中的所有整数组成，并按严格递增排序。请你对 `arr` 应用下述算法：
>
> - 从左到右，删除第一个数字，然后每隔一个数字删除一个，直到到达列表末尾。
> - 重复上面的步骤，但这次是从右到左。也就是，删除最右侧的数字，然后剩下的数字每隔一个删除一个。
> - 不断重复这两步，从左到右和从右到左交替进行，直到只剩下一个数字。
>
> 给你整数 `n` ，返回 `arr` 最后剩下的数字。
>
>  
>
> **示例 1：**
>
> ```
> 输入：n = 9
> 输出：6
> 解释：
> arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
> arr = [2, 4, 6, 8]
> arr = [2, 6]
> arr = [6]
> ```
>
> **示例 2：**
>
> ```
> 输入：n = 1
> 输出：1
> ```
>
> 
>
> **提示：**
>
> - `1 <= n <= 109`





## 第一次尝试

~~~python
class Solution:
    def lastRemaining(self, n: int) -> int:
        count = 0
        lst = [i for i in range(1, n + 1)]
        while n > 0:
            if count < n:
                ele = lst.pop(count)
                count += 1
                n -= 1
            else:
                count = 0
                lst.reverse()
                ele = lst.pop(count)
                count += 1
                n -= 1
        return ele
~~~

结果超时



## 第二次尝试

```python
class Solution:
    def lastRemaining(self, n: int) -> int:
        head = 1
        step = 1
        left = True
        
   	    while n > 1:
            # 从左边开始移除 or（只有从左开始 数列总会为奇数）
            if left or n % 2 != 0:
                head += step
        
            step <<= 1 # 步长 * 2
            n >>= 1 # 总数 / 2
            left = not left #取反移除方向

        return head
```

可能是因为没有重新构建,有提高效率



## 第三次尝试

~~~python
class Solution:
    def lastRemaining(self, n: int) -> int:
        return 1 if n==1 else 2*(n//2+1-self.lastRemaining(n//2))

~~~

思路: 约瑟夫环

> 两种情况
>
> - 如果是偶数情况
>   - 原式子为 1    2    3    4    5    …    2k
>   - 踢出后从左往右 新式子 会变为 2    4   …    2k                ————   (1)
>   - 因为接下来要从右往左 所以重新排 且当前数量应该为  2k / 2 = k
>     - 所以是 k     k-1    …    1                                      ————  (2)
>   - 分析两个式子我们可以发现 对于 (1) 中的每一个元素 处以 2 加上对应位置的 (2) 元素 都可以得到 k + 1
>   - 所以我们可以得到 ***$f(2k) = 2(k + 1 - f(k))$*** 这个递归式子  			 
> - 如果是奇数情况
>   - 原式子为 1    2    3    4    5    …    2k    2k + 1
>   - 发现第一次踢出后 仍然和 偶数情况一样 为 2    4   …    2k
>   - 所以我们可以得到一样的递归式子 $f(2k) = 2(k + 1 - f(k))$

