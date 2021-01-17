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
