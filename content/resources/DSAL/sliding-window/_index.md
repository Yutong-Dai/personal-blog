---
title: 滑动窗口
linktitle: sliding-window
toc: true
type: docs
date: "2020-12-14"
lastmod: "{{ .Lastmod }}"
draft: false
menu:
  DSAL:
    weight: 14
---

# 1456.定长子串中元音的最大数目

```
给你字符串 s 和整数 k 。

请返回字符串 s 中长度为 k 的单个子字符串中可能包含的最大元音字母数。

英文中的 元音字母 为（a, e, i, o, u）。

 

示例 1：

输入：s = "abciiidef", k = 3
输出：3
解释：子字符串 "iii" 包含 3 个元音字母。
示例 2：

输入：s = "aeiou", k = 2
输出：2
解释：任意长度为 2 的子字符串都包含 2 个元音字母。
示例 3：

输入：s = "leetcode", k = 3
输出：2
解释："lee"、"eet" 和 "ode" 都包含 2 个元音字母。
示例 4：

输入：s = "rhythms", k = 4
输出：0
解释：字符串 s 中不含任何元音字母。
示例 5：

输入：s = "tryhard", k = 4
输出：1
 

提示：

1 <= s.length <= 10^5
s 由小写英文字母组成
1 <= k <= s.length

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路

滑动窗口。
1. 首先检查前 `k`字符里有多少个元音字母。记录为`ans`
2. 建立 `l`, `r`左右指针，每次将`l`和`r`增加1，直到越界。同时可以只关心增加的字符(`r`右移动)和移除的字符(`l`左移动)是否是元音(用hashTable)便可得到到当前窗口中元音字母个数。最后和`ans`比较取较大的即可。


## 代码

```python
class Solution:
    def maxVowels(self, s: str, k: int) -> int:
        vowel = set(['a', 'e', 'i', 'o', 'u'])
        r, l = k-1, 0
        n = len(s)
        ans = 0
        for i in range(l, r+1):
            if s[i] in vowel:
                ans += 1
        last_window = ans
        while r < n:
            l += 1
            r += 1
            current_window = last_window
            if s[l-1] in vowel: current_window -= 1
            if r < n and s[r] in vowel: current_window += + 1
            ans = max(ans, current_window)
            last_window = current_window
        return ans
```

## 复杂度

* 时间复杂度：$O(n)$
* 空间复杂度：$O(1)$


# 1423. 可获得的最大点数

```
几张卡牌 排成一行，每张卡牌都有一个对应的点数。点数由整数数组 cardPoints 给出。

每次行动，你可以从行的开头或者末尾拿一张卡牌，最终你必须正好拿 k 张卡牌。

你的点数就是你拿到手中的所有卡牌的点数之和。

给你一个整数数组 cardPoints 和整数 k，请你返回可以获得的最大点数。

 

示例 1：

输入：cardPoints = [1,2,3,4,5,6,1], k = 3
输出：12
解释：第一次行动，不管拿哪张牌，你的点数总是 1 。但是，先拿最右边的卡牌将会最大化你的可获得点数。最优策略是拿右边的三张牌，最终点数为 1 + 6 + 5 = 12 。
示例 2：

输入：cardPoints = [2,2,2], k = 2
输出：4
解释：无论你拿起哪两张卡牌，可获得的点数总是 4 。
示例 3：

输入：cardPoints = [9,7,7,9,7,7,9], k = 7
输出：55
解释：你必须拿起所有卡牌，可以获得的点数为所有卡牌的点数之和。
示例 4：

输入：cardPoints = [1,1000,1], k = 1
输出：1
解释：你无法拿到中间那张卡牌，所以可以获得的最大点数为 1 。 
示例 5：

输入：cardPoints = [1,79,80,1,1,1,200,1], k = 3
输出：202
 

提示：

1 <= cardPoints.length <= 10^5
1 <= cardPoints[i] <= 10^4
1 <= k <= cardPoints.length
```

## 思路

1. 假设卡片是首位相连的。
2. 找到一个窗口大小是k的滑动窗口，使得窗口内数字和最大。

为了满足抽卡的规则, 初始化`left=0, right=k-1`。然后不停将`left`向左滑动`left = n-i`， `i`是滑动的次数。
根据题意，最多可以滑动`k` 次。

## 代码

```
class Solution:
    def maxScore(self, cardPoints: List[int], k: int) -> int:
        n = len(cardPoints)
        windowSum = 0
        for i in range(k):
            windowSum += cardPoints[i]
        ans = windowSum
        for i in range(k):
            windowSum = windowSum-cardPoints[k-1-i] + cardPoints[n-1-i]
            ans = max(windowSum, ans)
        return ans
```        
        
        
# 768. 最多能完成排序的块 II

```
这个问题和“最多能完成排序的块”相似，但给定数组中的元素可以重复，输入数组最大长度为2000，其中的元素最大为10**8。

arr是一个可能包含重复元素的整数数组，我们将这个数组分割成几个“块”，并将这些块分别进行排序。之后再连接起来，使得连接的结果和按升序排序后的原数组相同。

我们最多能将数组分成多少块？

示例 1:

输入: arr = [5,4,3,2,1]
输出: 1
解释:
将数组分成2块或者更多块，都无法得到所需的结果。
例如，分成 [5, 4], [3, 2, 1] 的结果是 [4, 5, 1, 2, 3]，这不是有序的数组。 
示例 2:

输入: arr = [2,1,3,4,4]
输出: 4
解释:
我们可以把它分成两块，例如 [2, 1], [3, 4, 4]。
然而，分成 [2, 1], [3], [4], [4] 可以得到最多的块数。 
注意:

arr的长度在[1, 2000]之间。
arr[i]的大小在[0, 10**8]之间。
```

## 思路

1. 根据题意不难发现，我们分割成的块需要满足：第`k-1`一块的的最大元素小于等于第`k`块最小的元素。
2. 存下每块最大元素，并统计存下元素个数，则为答案。

如何统计第`k`块的最大元素？ 利用单调栈的思想，稍微做点变形。遍历数组，

1. 如果当前元素`element`大于等于栈顶元素，则直接入栈。
2. 如果当前元素`element`小于栈顶元素，则记录下栈顶元素`topMax`（当前栈的最大元素）并将其推出。持续推出栈顶元素，直到`element`不小于当前栈顶元素，重新将`topMax`入栈。

[单调栈](https://lucifer.ren/blog/2020/11/03/monotone-stack/).

## 代码

```python
class Solution:
    def maxChunksToSorted(self, arr: List[int]) -> int:
        monotoneStack = [arr[0]]
        for i in range(1,len(arr)):
            element = arr[i]
            if element >= monotoneStack[-1]:
                monotoneStack.append(element)
            else:
                topMax = monotoneStack[-1]
                while monotoneStack and element < monotoneStack[-1]:
                    monotoneStack.pop(-1)
                monotoneStack.append(topMax)
        return len(monotoneStack)
```

复杂度分析

* 时间复杂度：$O(n)$
* 空间复杂度：$O(n)$        
