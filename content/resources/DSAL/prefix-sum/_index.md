---
title: Prefix Sum
linktitle: Prefix Sum
toc: true
type: docs
date: "2020-12-09"
lastmod: "{{ .Lastmod }}"
draft: false
menu:
  DSAL:
    weight: 11
---

# 560. 和为k的子数组

```
给定一个整数数组和一个整数 k，你需要找到该数组中和为 k 的连续的子数组的个数。

示例 1 :

输入:nums = [1,1,1], k = 2
输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。
说明 :

数组的长度为 [1, 20,000]。
数组中元素的范围是 [-1000, 1000] ，且整数 k 的范围是 [-1e7, 1e7]。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/subarray-sum-equals-k
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路

最直观的想法便是给定了 `start`与`end` ，对子数组`num[start:end]`里的元素求和。如果和为`k`则说明找到一组符合条件的子数组。但是这样的复杂度为$O(n^3)$。

### 初次优化

观察到 

```python
sum(num[start-1:end]) + num[start] = sum(num[start:end])
```
我们可以固定住`end` 然后让 `start`从 `end`开始递减到0，对在这个循环过程中得到子列和与`k`比较并统计符合条件的子列数量。

这样的话时间复杂度为$O(n^2)$. 可惜Python的版本会超时。

```python
class Solution(object):
    def subarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        total = 0
        if not nums:
            return total
        n = len(nums)
        for end in range(n):
            tempSum = 0
            for start in range(end, -1, -1):
                tempSum += nums[start]
                if tempSum == k:
                    total += 1
        return total
```

## 再次优化

假设我们有个数列`cumSum`其中`cumsum[i]`是`num`中前`i`个数的和，比如

```
cumSum[0] = num[0]
cumSum[1] = num[0] + num[1] 
....

更加紧凑的我们有

cumSum[0] = num[0]
cumSum[i] = num[i] + cumSum[i-1], i >= 1
```

对于满足的条件的子列(从`start`开始，到`end`结束 )，那么我们有 

```
k = sum(num[start:end]) = cumSum[end]  - cumSum[start-1]  --->

cumSum[start-1]  = cumSum[end]  -  k 
```
本质就是寻找 从`0` 到 `end` 有多少个 index `i` 使得 `cumSum[i] ` 为`k`。
之前的方法是用循环，这里考虑用哈希表`dic`。在建立`cumSum`这个数组的时候，我们
可以以 `cumSum[i] `为key 以 `cumSum[i] `出现的频次为value。
那么对于以`end`结束的子列，满足条件的子列有`dic[cumSum[end]  -  k ]`。

最后两个小细节：

1. 边界情况。`num[end]` 直接为`k`。我们在初始化哈希表时，需要加入一个 以`0`为key 以 `1`为value的key-value pair。
2. 我们不需要维护一个数组`cumSum[i] ` 而是用一个变量就够了。

```python
from collections import defaultdict
class Solution(object):
    def subarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        if not nums:
            return 0
        total = 0
        n = len(nums)
        cumSum = 0
        cumSumFreq = defaultdict()
        # 边界条件：什么都不选的时候 cumulative sum 为 0
        cumSumFreq[0] = 1
        for start in range(n):
            cumSum += nums[start]
            total += cumSumFreq.get(cumSum - k, 0)
            # 更新字典必须在求和之后
            cumSumFreq[cumSum] = cumSumFreq.get(cumSum, 0) + 1
        return total
```

时间复杂度： $O(n)$
空间复杂度： $O(n)$
