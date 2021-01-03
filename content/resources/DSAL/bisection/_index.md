---
title: 二分法
linktitle: bisection
toc: true
type: docs
date: "2021-01-03"
lastmod: "{{ .Lastmod }}"
draft: false
menu:
  DSAL:
    weight: 15
---

# 162. 寻找峰值

## 题目

```
峰值元素是指其值大于左右相邻值的元素。

给定一个输入数组 nums，其中 nums[i] ≠ nums[i+1]，找到峰值元素并返回其索引。

数组可能包含多个峰值，在这种情况下，返回任何一个峰值所在位置即可。

你可以假设 nums[-1] = nums[n] = -∞。

示例 1:

输入: nums = [1,2,3,1]
输出: 2
解释: 3 是峰值元素，你的函数应该返回其索引 2。
示例 2:

输入: nums = [1,2,1,3,5,6,4]
输出: 1 或 5 
解释: 你的函数可以返回索引 1，其峰值元素为 2；
     或者返回索引 5， 其峰值元素为 6。
说明:

你的解法应该是 O(logN) 时间复杂度的。



来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-peak-element
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路

题目要求是 O(logN) 时间复杂度自然就只有二分了。注意到题目的假设 ` nums[-1] = nums[n] = -∞`，因此即使是单调增／减的序列，峰值也是一定存在的。

既然使用二分法，自然还是套路的不停地跟新`left`, `right`以及`mid`。关键在于，当 `nums` 不是有序的情况下，如何每次排除一半的数据？下面就分三种情况讨论。

1. `nums`是单调增。比较`nums[mid]`和`nums[mid+1]`。因为`nums`是单调增，因此`nums[mid]<nums[mid+1]`。这表明了`nums[mid]`一定不可能是峰值。于是搜索区间可以变成`[mid+1, right]`。 重复操作，我们知道搜索一定会在`nums`最后一个数停止。

2. `nums`是单调减。比较`nums[mid]`和`nums[mid+1]`。因为`nums`是单调减，因此`nums[mid]>nums[mid+1]`。这表明了`nums[mid+1]`一定不可能是峰值。于是搜索区间可以变成`[left, mid]`。 重复操作，我们知道搜索一定会在`nums`第一个数停止。**注意比较此处的搜索区间是 `[left, mid]` 不同于 单调增时的 `[mid+1, right]`**， 原因在于我们不能排除`nums[mid]`为峰值的可能性(当我们不知道`nums`是单调减的)。

3. `nums`不是单调的。这个时候就是把1和2的思路结合一下。先找到`mid`比较下`nums[mid]`和`nums[mid+1]`。如果`nums[mid]<nums[mid+1]`，则搜索区间可以变成`[mid+1, right]`；如果 `nums[mid]>nums[mid+1]`，则搜索区间是 `[left, mid]`。

## 代码

```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        n = len(nums)
        if n == 0:
            return 0
        left, right = 0, n - 1
        while left < right:
            mid = (left + right) >> 1
            if nums[mid] < nums[mid + 1]:
                left = mid + 1
            else:
                right = mid
        return left
```

## 复杂度
* 时间：$O(\log_2 n)$
* 空间：$O(1)$

# 5643 将数组分成三个子数组的方案数

## 题目

```
我们称一个分割整数数组的方案是 好的 ，当它满足：

数组被分成三个 非空 连续子数组，从左至右分别命名为 left ， mid ， right 。
left 中元素和小于等于 mid 中元素和，mid 中元素和小于等于 right 中元素和。
给你一个 非负 整数数组 nums ，请你返回 好的 分割 nums 方案数目。由于答案可能会很大，请你将结果对 109 + 7 取余后返回。

 

示例 1：

输入：nums = [1,1,1]
输出：1
解释：唯一一种好的分割方案是将 nums 分成 [1] [1] [1] 。
示例 2：

输入：nums = [1,2,2,2,5,0]
输出：3
解释：nums 总共有 3 种好的分割方案：
[1] [2] [2,2,5,0]
[1] [2,2] [2,5,0]
[1,2] [2,2] [5,0]
示例 3：

输入：nums = [3,2,1]
输出：0
解释：没有好的分割方案。
 

提示：

3 <= nums.length <= 10^5
0 <= nums[i] <= 10^4

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/ways-to-split-array-into-three-subarrays
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路

前缀和 + 二分法。 

1. 首先说为何想到要用前缀和？
    * 如果给定一个划分，我们如何判断它是不是一个`好的`划分？我们只需要把`left`, `mid`， `right` 中的元素全部加起来，然后比较大小即可。
    * 为了避免重复的加法，我们想到了前缀和。具体来说，只要给定了一种划分（划分用索引的形式的表达，`cut1`和`cut2`, 表示分别在`nums[cut1]` `nums[cut2]`处截断）， 我们便知道了`left=sum(nums[0 : cut1]` (包含`cut1`), `mid=sum(nums[cut1+1:cut2])`， `right=sum(nums[cut2+1:n])`。
    *  接下来只需要用一个双循环去遍历所有可能的`cut1`和`cut2`，我们便可以找到所有`好的`划分。最后利用一些剪枝的技巧， 当`sum(nums[cut1+1:cut2]) >  sum(nums[cut2+1:end])`时我们可以终止内层循环。代码如下。
    
```python
class Solution:
    def waysToSplit(self, nums: List[int]) -> int:
        n = len(nums)
        if n < 3:
            return 0
        ans = 0
        # get cumulative sum
        for i in range(1, len(nums)):
            nums[i] += nums[i-1]
        last = n - 1
        for first in range(n-2):
            for second in range(first+1, n-1):
                cumsum_mid = nums[second] - nums[first]
                cumsum_right = nums[last] - nums[second]
                if cumsum_mid >= nums[first] and cumsum_right >= cumsum_mid:
                    ans += 1
                # prune
                if cumsum_right < cumsum_mid:
                    break
        return ans % (1000000007)
```

2. 为何使用二分法?
    * 上述算法的时间复杂度为$O(n^2)$, 而数据量`len(nums)=1e5`。根据lucifer的复杂度表，我们需要一个$O(n\log_2n)$的算法。
    * 优化什么？ 如果我们可以把内层循环变成一个$O(\log_2 n)$的算法，那就大功告成。我们内层循环本质是, 当给定`cut1`的时候, 寻找第二个截断`cut2`使得 `sum(nums[0 : cut1] <= sum(nums[cut1+1:cut2]) <= sum(nums[cut2+1:n])`。
    * 怎么优化？用二分法来进行优化。首先构造一个`cumsum`来表示`nums`的前缀和。其中`cum[i]=sum(nums[:i])`。注意到 `cumsum`是单调不减的 (**意味着`nums`可能有重复的元素!!**)， 因此我们需要找到 *最左边的*`cut2` 和 *最右边的*`cut2`, 即找到` [cut1+1, n-1)`中最小和最大的元素使得`sum(nums[0 : cut1] <= sum(nums[cut1+1:cut2]) <= sum(nums[cut2+1:end])`成立。 (**注意是左开右闭**，我也是提交后错了才意识到。因为cut2 不能在最后一个元素处，否则`right`是一个空数组。考虑[0,0,0,0]这样输入。)
    * （再加点细节）比如我们要找到*最右边的*`cut2`。我们则需要从 `[cut1+1, n-1]`中寻找最大满足条件的值。假设`l`, `r`, `mid`为二分搜索时的三个指针。我们可以定义`cumsum_left = cumsum[cut1], cumsum_mid = cumsum[mid] - cumsum_left, cumsum_right=cumsum[n] - cumsum_mid`。然后有如下四种情况进行讨论

```
cumsum_mid >= cumsum_left and cumsum_right >= cumsum_mid
此时我们找到一个合格的cut2，作为备选。并将 l 指向 mid+1,来寻找潜在更大的cut2

cumsum_mid < cumsum_left  and cumsum_right >= cumsum_mid
此时的cut2太小了，我们需要增加 l 到 mid + 1，来获得更大的 cumsum_mid
           
cumsum_mid >= cumsum_left and cumsum_right < cumsum_mid
此时的cut2太大了，我们需要减小 r 到 mid - 1，来获得更大的 cumsum_right

cumsum_mid < cumsum_left and cumsum_right < cumsum_mid
不存在可行的cut2，直接剪枝了。因为此时需要同时增大cumsum_mid  和 cumsum_right
```


## 代码

```python
class Solution:
    def waysToSplit(self, nums: List[int]) -> int:
        self.n = len(nums)
        if self.n < 3:
            return 0
        ans = 0
        # get cumulative sum
        for i in range(1, self.n):
            nums[i] += nums[i-1]
        self.cumsum = nums
        for left in range(self.n-2):
            cumsum_left = nums[left]
            if cumsum_left * 3 > self.cumsum[-1]:
                break
            rightMostCut = self.right_find(left+1, cumsum_left)
            leftMostCut = self.left_find(left+1, cumsum_left)
            if rightMostCut != -1:
                ans += rightMostCut - leftMostCut + 1
        return ans % (1000000007)
    def right_find(self, start, cumsum_left):
        l, r = start, self.n - 1
        ans = -1
        while l <= r:
            mid = (l+r) >> 1
            cumsum_mid = self.cumsum[mid] - cumsum_left
            cumsum_right = self.cumsum[-1] - self.cumsum[mid]
            # find a qualified cut
            if cumsum_mid >= cumsum_left and cumsum_right >= cumsum_mid:
                l = mid + 1
                ans = mid
            # need to increase the cumsum_mid
            elif cumsum_mid < cumsum_left and cumsum_right >= cumsum_mid:
                l = mid + 1
            # need to decrease the cumsum_mid
            elif cumsum_mid >= cumsum_left and cumsum_right < cumsum_mid:
                r = mid - 1
            # no answer
            else:
                break
        return min(ans, self.n-2)
    def left_find(self, start, cumsum_left):
        l, r = start, self.n - 1
        ans = -1
        while l <= r:
            mid = (l+r) >> 1
            cumsum_mid = self.cumsum[mid] - cumsum_left
            cumsum_right = self.cumsum[-1] - self.cumsum[mid]
            # find a qualified cut
            if cumsum_mid >= cumsum_left and cumsum_right >= cumsum_mid:
                r = mid - 1
                ans = mid
            # need to increase the cumsum_mid
            elif cumsum_mid < cumsum_left and cumsum_right >= cumsum_mid:
                l = mid + 1
            # need to decrease the cumsum_mid
            elif cumsum_mid >= cumsum_left and cumsum_right < cumsum_mid:
                r = mid - 1
            # no answer
            else:
                break
        return ans
```

## 复杂度

* 时间复杂度：$O(n\log_2n)$
* 空间复杂度：$O(n)$

