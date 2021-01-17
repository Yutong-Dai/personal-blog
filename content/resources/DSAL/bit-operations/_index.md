---
title: Bit operations
linktitle: Bit operations
toc: true
type: docs
date: "2020-12-05"
lastmod: "{{ .Lastmod }}"
draft: false
menu:
  DSAL:
    weight: 10
---

# 268. 丢失的数字

```
给定一个包含 [0, n] 中 n 个数的数组 nums ，找出 [0, n] 这个范围内没有出现在数组中的那个数。

 

进阶：

你能否实现线性时间复杂度、仅使用额外常数空间的算法解决此问题?
 

示例 1：

输入：nums = [3,0,1]
输出：2
解释：n = 3，因为有 3 个数字，所以所有的数字都在范围 [0,3] 内。2 是丢失的数字，因为它没有出现在 nums 中。
示例 2：

输入：nums = [0,1]
输出：2
解释：n = 2，因为有 2 个数字，所以所有的数字都在范围 [0,2] 内。2 是丢失的数字，因为它没有出现在 nums 中。
示例 3：

输入：nums = [9,6,4,2,3,5,7,0,1]
输出：8
解释：n = 9，因为有 9 个数字，所以所有的数字都在范围 [0,9] 内。8 是丢失的数字，因为它没有出现在 nums 中。
示例 4：

输入：nums = [0]
输出：1
解释：n = 1，因为有 1 个数字，所以所有的数字都在范围 [0,1] 内。1 是丢失的数字，因为它没有出现在 nums 中。
 

提示：

n == nums.length
1 <= n <= 104
0 <= nums[i] <= n
nums 中的所有数字都 独一无二


来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/missing-number
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路1: 数学加减法

对`[0,n]`求和 然后减去`sum(numse)` 即为答案

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        n = len(nums) 
        return int(n * (n+1) / 2) - sum(nums)
```

* 时间复杂度：$O(n)$
* 空间复杂度：$O(1)$

## 思路2: 异或`XOR`运算

用到的异或运算法则：
1. `a ^ a = 0`
2. `a^b^c=a^c^b`
3. `a ^ b ^ c = a ^ (b ^ c) = (a ^ b) ^ c`

考虑

```
nums = [0,2,3]
index = [0,1,2,3]

1 = (0^0)^1^(2^2)^(3^3) = (0^2^3) ^ (0^1^2^3) 
```

因此便有如下代码

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        n = len(nums)
        ans = n
        for i in range(n):
            ans ^= (i^nums[i])
        return ans
```
* 时间复杂度：$O(n)$
* 空间复杂度：$O(1)$

# 面试题 01.01. 判定字符是否唯一

```
实现一个算法，确定一个字符串 s 的所有字符是否全都不同。

示例 1：

输入: s = "leetcode"
输出: false 
示例 2：

输入: s = "abc"
输出: true
限制：

0 <= len(s) <= 100
如果你不使用额外的数据结构，会很加分。
```

## 思路

基本思路如下

1. 创建一个长度为26的array并初始为全0值，a-z 各自对应 0-25. 
2. 遍历`astr`，对当前字符`char`在array中对应位置的元素加1。
3. 在遍历过程中，如果array中有位置出现2，则说明出现了重复的值。否则无重复。

如果我们用`0`表示一个字符尚未出现，`1`表示字符已经出现了，则上述操作可以全部使用 `位运算`完成。

* `创建一个长度为26的array并初始为全0值`:  创建一个变量`seen`, 并初始为0。
* `对当前字符char在array中对应位置的元素加1`： 计算当前字符`char`与`a`的距离为`d`, 利用 `seen | 1<<(d+1)`。
* `如果array中有位置出现2`:  计算当前字符`char`与`a`的距离为`d`, 利用 `seen & 1<<(d+1) `。

## 代码

```python
class Solution:
    def isUnique(self, astr: str) -> bool:
        seen = 0
        origin = ord('a')
        for char in astr:
            d = ord(char) - origin + 1
            temp = 1 << d
            # 如果 返回 True, 则说明 char 已经出现过了
            if seen & temp == temp:
                return False
            # 标记 char 为被发现
            seen = seen | temp
        return True
```

# 复杂度分析：
* 时间复杂度：$O(n)$
* 空间复杂度：$O(1)$


# leetcode 78: 子集

题目描述
```
给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

示例:

输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/subsets
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路

数学上来说，每个元素存在选和不选两个可能性，所以一共有2^n种结果，其中n是`nums` 元素中的个数。
问题变成了枚举[0, 2^n-1]的二进制表达。举个例子
```
nums = [3,2,1]  ---> 8 = 2^3 中可能

每种可能对应的二进制表示如下

1.   000   []
2.   001   [1]
3.   010   [2]
4.   011   [1,2]
5.   100   [3]
6.   101   [1,3]
7.   110   [1,2]
8.   111   [1,2,3]
```
但是如何用计算机语言来，尤其是利用位运算来枚举上述所有情况呢。因为对这个不熟，参考了[这里](https://leetcode-cn.com/problems/subsets/solution/hui-su-wei-yun-suan-di-gui-deng-gong-4chong-fang-s/)的处理方式。

举个例子

```
110
从右往左(0-indexed)在第1和第2位置出现了1. 如何用位运算找到呢？
每次向右移动n个bit然后和 1 做 “并” 运算，便可知道第n位是否为1。
举个例子

将110向右移动0个bit: 110>>0 ---> 110. 110 & 001 ---> 0: 说明第0位不为1
将110向右移动1个bit: 110>>1 ---> 011.  011 & 001 ---> 1: 说明第1位为1
将110向右移动2个bit: 110>>2 ---> 001.  001 & 001 ---> 1: 说明第2位为1
```

## 代码

```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        n = len(nums)
        numElements =  1 << n
        ans = [0] * numElements
        for mask in range(numElements):
            # 寻找 mask 的二进制表达中 1出现的位置
            # 因为我们一共有n个数字在nums中， 所以2^n
            # 有n个bits。 从而最左位数最多能向右移动n-1次
            temp = []
            for rightShift in range(n):
                # 从右往左数，mask的第rightShift位刚好是1
                if (mask >> rightShift) & 1 == 1:
                    temp.append(nums[rightShift])
            ans[mask] = temp
        return ans
```

## 复杂度

* 时间：$O(n2^n)$ 
    * `for mask in range(numElements)`: $2^n$
    *  ` for rightShift in range(n):`: $n$
* 空间: 不算返回数组是 $O(n)$
