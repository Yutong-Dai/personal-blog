---
title: 背包问题
linktitle: Knapsack
toc: true
type: docs
date: "2021-01-20"
lastmod: "{{ .Lastmod }}"
draft: false
menu:
  DSAL:
    weight: 14
---

# 416. 分割等和子集

```
给定一个只包含正整数的非空数组。是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

注意:

每个数组中的元素不会超过 100
数组的大小不会超过 200
示例 1:

输入: [1, 5, 11, 5]

输出: true

解释: 数组可以分割成 [1, 5, 5] 和 [11].
 

示例 2:

输入: [1, 2, 3, 5]

输出: false

解释: 数组不能分割成两个元素和相等的子集.
```

# 思路

1. 对edge cases 做判断：如果数组求和为奇数，则肯定不可能。如果为偶数，则将和的一半记为`target`。
2. 问题转换成是否能从`nums`选出至少一个元素使得选出的元素和为`target`。
3. 这个问题可以变成0-1背包为题: 从 `nums` 中选出物品，其中第`i`个物品的 `cost`和`value`都是`nums[i]`, `capacity`为`target`。

关于`0-1`背包问题的描述和求解可以参考这个[文档](https://github.com/tianyicui/pack/blob/master/V2.pdf).

## 代码

```python
import math
class Solution(object):
    def canPartition(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        def knapsack(capacity, values):
            n = len(values)
            dp = [0 for v in range(capacity+1)]
            for i in range(1, n+1):
                for v in range(capacity, values[i-1]-1, -1):
                    dp[v] = max(dp[v], dp[v-values[i-1]]+values[i-1])
            return dp[capacity] == capacity

        total = sum(nums)
        target = total // 2
        if (total - target * 2) != 0:
            return False
        return knapsack(target, nums)
```

## 复杂度

`n=len(nums), V = sum(nums)//2`

* 时间复杂度：$O(nV)$
* 空间复杂度：$O(V)$
 

# 494. 目标和

```
给定一个非负整数数组，a1, a2, ..., an, 和一个目标数，S。现在你有两个符号 + 和 -。
对于数组中的任意一个整数，你都可以从 + 或 -中选择一个符号添加在前面。

返回可以使最终数组和为目标数 S 的所有添加符号的方法数。


示例：

输入：nums: [1, 1, 1, 1, 1], S: 3
输出：5
解释：

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

一共有5种方法让最终目标和为3。
 

提示：

数组非空，且长度不会超过 20 。
初始的数组的和不会超过 1000 。
保证返回的最终结果能被 32 位整数存下。
```

## 思路

暴力法： 和寻找所有可能的子集一个套路。列举所有可能的子集，该子集里添加`+`，该子集的补集使用`-`。不出意外，超时了。

```python
class Solution(object):
    def findTargetSumWays(self, nums, S):
        """
        :type nums: List[int]
        :type S: int
        :rtype: int
        """
        n = len(nums)
        candicates = 1 << n
        ans = 0
        for c in range(candicates):
            temp = 0
            for rightShift in range(n):
                if c >> rightShift & 1:
                    temp += nums[rightShift]
                else:
                    temp -= nums[rightShift]
            if temp == S:
                ans += 1
        return ans
```

因为这里每个元素都要选，如何将其转化成背包问题呢。 稍微做下分析。

1. 假设`nums`中所有元素的和为 `totalSum`。假设添加正号的元素和为`P`, 添加负号的元素和为`N`。不难发现 `P-N=totalSum`  以及 `P+N = S`。 于是问题变成从 `nums`选物品使得和刚好为`(totalSum + S )/2`。
2. 排除一些边界情况`(totalSum + S )`为奇数, `totalSum<S`。
3. `dp[i,j]`表示 从前`i` 个元素中选和为`j`有多少种不同的选法。 `dp[0,0]`初始为0。
4. 迭代关系为 `dp[i,j]=dp[i-1,j] + dp[i-1, j-num[i]]`。
5. 对空间进行优化，用一维数组实现上述功能即可。

```python
class Solution(object):
    def findTargetSumWays(self, nums, S):
        """
        :type nums: List[int]
        :type S: int
        :rtype: int
        """
        totalSum = sum(nums)
        if S > totalSum:
            return 0
        target = (S + totalSum) >> 1
        if (S+totalSum) % 2 != 0:
            return 0
        # dp[j]: 和为j 的选法数量
        dp = [0] * (target + 1)
        dp[0] = 1
        for i in range(len(nums)):
            for j in range(target, nums[i] - 1, -1):
                dp[j] += dp[j-nums[i]]
        return dp[-1]  
```

## 复杂度

`V = sum(nums), n = len(nums)`
* 时间：$O(n*V)$
* 空间：$O(V)$


# 322. 零钱兑换

```
给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。

你可以认为每种硬币的数量是无限的。

 

示例 1：

输入：coins = [1, 2, 5], amount = 11
输出：3 
解释：11 = 5 + 5 + 1
示例 2：

输入：coins = [2], amount = 3
输出：-1
示例 3：

输入：coins = [1], amount = 0
输出：0
示例 4：

输入：coins = [1], amount = 1
输出：1
示例 5：

输入：coins = [1], amount = 2
输出：2
 

提示：

1 <= coins.length <= 12
1 <= coins[i] <= 231 - 1
0 <= amount <= 104
```

## 思路

因为是无限银币，可以强行将`coins` 数列中每个元素重复。其中`coins[i]` 的重复次数为 `amount // coins[i]`。
可惜，超时了。

```python
import numpy as np
class Solution(object):
    def coinChange(self, coins, amount):
        """
        :type coins: List[int]
        :type amount: int
        :rtype: int
        """
        pool = []
        for i in coins:
            pool += [i] * (amount // i)
        dp = [ np.inf ] * (amount + 1)
        dp[0] = 0
        for i in range(len(pool)):
            for j in range(amount, pool[i]-1, -1):
                dp[j] = min(dp[j], dp[j-pool[i]] + 1)
        if dp[amount] == np.inf:
            return -1
        return dp[amount]
```

利用动态规划的思想。

1. `dp[v]` 为 要凑够和为 `v` 最少需要硬币的数量。
2. 递推关系  `dp[v] = min {dp[v-coin[i]}`
3. 初始化 `dp[0] = infty`
4. 不难发现 `v-coin[i]`可以为负数，这时候只需要假设`dp[v-coin[i]` 为 `-infty`

```python
        
import numpy as np
class Solution(object):
    def coinChange(self, coins, amount):
        """
        :type coins: List[int]
        :type amount: int
        :rtype: int
        """
        dp = [ np.inf ] * (amount + 1)
        dp[0] = 0
        maxCoinValue = max(coins)
        numDifferentCoins = len(coins)
        for v in range(1, amount+1):
            temp = np.inf
            for i in range(numDifferentCoins):
                if v-coins[i] < 0:
                    continue
                if dp[v-coins[i]] < temp:
                    temp = dp[v-coins[i]]
            dp[v] = temp + 1
        if dp[amount] == np.inf:
            return -1
        return dp[amount]
```

## 复杂度分析

* 时间复杂度：O(amount*n)
* 空间复杂度：O(amount)

