---
title: 动态规划
linktitle: dynamic programming
toc: true
type: docs
date: "2020-12-14"
lastmod: "{{ .Lastmod }}"
draft: false
menu:
  DSAL:
    weight: 14
---

# 435. 无重叠区间

```
给定一个区间的集合，找到需要移除区间的最小数量，使剩余区间互不重叠。

注意:

可以认为区间的终点总是大于它的起点。
区间 [1,2] 和 [2,3] 的边界相互“接触”，但没有相互重叠。
示例 1:

输入: [ [1,2], [2,3], [3,4], [1,3] ]

输出: 1

解释: 移除 [1,3] 后，剩下的区间没有重叠。
示例 2:

输入: [ [1,2], [1,2], [1,2] ]

输出: 2

解释: 你需要移除两个 [1,2] 来使剩下的区间没有重叠。
示例 3:

输入: [ [1,2], [2,3] ]

输出: 0

解释: 你不需要移除任何区间，因为它们已经是无重叠的了。


来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/non-overlapping-intervals
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路

考虑如下一组输入

```
[[1, 100], [11, 22], [1, 11], [2, 12]]
```

最长无重叠的区间是

```
nonOverlap = [[1, 11], [11, 22]]

或者

nonOverlap = [[2, 12], [11, 22]]
```

一个重要的观察: `nonOverlap[i][1] <= nonOverlap[i+1][0]`, 即两个相邻的区间，前一个区间的右端点小于等于后一个区间的左端点。所以先考虑对输入的`intervals`中的区间按照右端点的大小进行升序排列。

接下来构建动态规划的叠加公式，我们有两种选择。下面考虑第一种

**选项一**: `dp[i]`表示 `intervals[0], ... , intervals[i]`中含有 `intervals[i]`最长不重叠区间。该情况下的迭代公式为


$$
dp[i] = \max_{0\leq j \leq i-1}(dp[j]) + 1 \qquad \text{s.t. } dp[i][0] >= dp[j][1]
$$


**代码**

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        if not intervals or len(intervals) == 1:
            return 0
        # sort by the ending time
        intervals = sorted(intervals, key=lambda t: t[1])
        n = len(intervals)
        dp = [1] * n
        for i in range(1, n):
            for j in range(i):
                if intervals[j][1] <= intervals[i][0]:
                    dp[i] = max(dp[i], dp[j] + 1)
        return n - max(dp)
```

这种做法不能通过，会超时。我们可不可优化一下呢？ 下面考虑第二种选项。


**选项二**: `dp[i]`表示 `intervals[0], ... , intervals[i]`中最长不重叠区间(即不一定含有`intervals[i]`)。这种定义的好处可以保证`dp`是一个单调不减的序列。
该情况下的迭代公式为


$$
dp[i] = dp[j_*] + 1 \qquad \text{s.t. }  j_*=\arg\max\{(j| dp[i][0] >= dp[j][1], 0\leq j \leq i-1)\}.
$$

这个迭代公式的好处在于,可以提前剪枝（虽然没有改变时间复杂度）。

**代码**

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        if not intervals or len(intervals) == 1:
            return 0
        # sort by the ending time
        intervals = sorted(intervals, key=lambda t: t[1])
        n = len(intervals)
        dp = [1] * n
        for i in range(1, n):
            for j in range(i-1, -1, -1):
                if intervals[j][1] <= intervals[i][0]:
                    dp[i] = max(dp[i], dp[j] + 1)
                    # 提前剪枝
                    break
            dp[i] = max(dp[i], dp[i-1])
        return n - max(dp)
```

**复杂度:**

* 时间: $O(n^2)$
* 空间: $O(n)$
