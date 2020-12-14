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
