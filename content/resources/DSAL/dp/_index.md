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

# 837. 新21点

```
爱丽丝参与一个大致基于纸牌游戏 “21点” 规则的游戏，描述如下：

爱丽丝以 0 分开始，并在她的得分少于 K 分时抽取数字。 抽取时，她从 [1, W] 的范围中随机获得一个整数作为分数进行累计，其中 W 是整数。 每次抽取都是独立的，其结果具有相同的概率。

当爱丽丝获得不少于 K 分时，她就停止抽取数字。 爱丽丝的分数不超过 N 的概率是多少？

 

示例 1：

输入：N = 10, K = 1, W = 10
输出：1.00000
说明：爱丽丝得到一张卡，然后停止。
示例 2：

输入：N = 6, K = 1, W = 10
输出：0.60000
说明：爱丽丝得到一张卡，然后停止。
在 W = 10 的 6 种可能下，她的得分不超过 N = 6 分。
示例 3：

输入：N = 21, K = 17, W = 10
输出：0.73278
 

提示：

0 <= K <= N <= 10000
1 <= W <= 10000
如果答案与正确答案的误差不超过 10^-5，则该答案将被视为正确答案通过。
此问题的判断限制时间已经减少。


来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/new-21-game
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

# 思路

参考[这里](https://leetcode-cn.com/problems/new-21-game/solution/zen-yang-de-dao-guan-fang-ti-jie-zhong-de-zhuang-t/).

# 代码

```python
class Solution:
    def new21Game(self, N: int, K: int, W: int) -> float:
        if K == 0:
            return 1
        dp = [0] * ((K-1+W) + 1)
        for j in range(K, min(N, K-1+W)+1): dp[j] = 1
        dp[K-1] = min(N-K+1, W) / W
        for s in range(K-1, 0, -1):
            dp[s-1] = dp[s] + (dp[s] - dp[s+W]) / W
        return dp[0]
```

# 复杂度

* 时间复杂度: $O(K+W)$
* 空间复杂度: $O(K+W)$


# 438. 找到字符串中所有字母异位词

```
给定一个字符串 s 和一个非空字符串 p，找到 s 中所有是 p 的字母异位词的子串，返回这些子串的起始索引。

字符串只包含小写英文字母，并且字符串 s 和 p 的长度都不超过 20100。

说明：

字母异位词指字母相同，但排列不同的字符串。
不考虑答案输出的顺序。
示例 1:

输入:
s: "cbaebabacd" p: "abc"

输出:
[0, 6]

解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的字母异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的字母异位词。
 示例 2:

输入:
s: "abab" p: "ab"

输出:
[0, 1, 2]

解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的字母异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的字母异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的字母异位词。


来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-all-anagrams-in-a-string
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路

刚开始做想到用一个`set`来记录`p`中的字母，然后利用滑动窗口记录当前窗口中元素与set的匹配情况。后来发现测试案例中有 `p=‘aa’`这种带重复字母的情况。所以变成用一个长度为26的`list`来记录`p`中每个元素出现的频率，然后再开一个长度为26的`list` 来记录`s`中当前窗口字母的频次，如果两个`list`一样，则找到一个符合条件的`字母异位词`。

## 代码

```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        n, size = len(s), len(p)
        ans = []
        if n < size: return ans
        p_array = [0] * 26
        s_array = [0] * 26

        for i in range(size):
            p_array[ord(p[i]) - ord('a')] += 1
            s_array[ord(s[i]) - ord('a')] += 1
        if s_array == p_array:
            ans.append(0)
        l = 0
        while l < n-size:
            l += 1
            r = l + size - 1
            s_array[ord(s[l-1]) - ord('a')] -= 1
            s_array[ord(s[r]) - ord('a')] += 1
            if s_array == p_array:
                ans.append(l)
        return ans
```

## 复杂度分析

* 时间复杂度：$O(n)$, `n`为`s`的长度;
* 空间复杂度：$O(1)$

## 代码的改进

仔细看代码，发现比较两个数组`s_array == p_array`可以优化。具体来说

1. 初始一个 `debit`的`list`。遍历`p`中的字符，并在`debit`中该字符对应的位置减去1，表示“负债”情况。
2. 每次跟新窗口的时候，如果移除的字母当前对应的`debit`小于等于0，则说明该字母出现在`p`中; 对增加的字母也可同理。

```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        n, size = len(s), len(p)
        ans = []
        if n < size: return ans
        debit = [0] * 26
        for char in p:
            # 初始负债情况
            debit[ord(char) - ord('a')] -= 1
        l = 0
        lack = size
        for i in range(size):
            idx = ord(s[i]) - ord('a')
            # 给正确的地方充值
            if debit[idx] < 0:
                lack -= 1
            debit[idx] += 1
        # 负债为0，当前窗口的字母和p中字母匹配上了
        if lack == 0: ans.append(l)
        while l < n-size:
            l += 1
            r = l + size - 1
            rm_idx = ord(s[l-1]) - ord('a')
            add_idx = ord(s[r]) - ord('a')
            # 给正确的地方扣钱
            if debit[rm_idx] <= 0:
                lack += 1
            debit[rm_idx] -= 1
            debit[add_idx] += 1
            # 给正确的地方充值
            if debit[add_idx] <= 0:
                lack -= 1
            if lack == 0:
                ans.append(l)
        return ans
```
