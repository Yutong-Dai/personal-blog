---
title: Heap
linktitle: Heap
toc: true
type: docs
date: "2020-12-05"
lastmod: "{{ .Lastmod }}"
draft: false
menu:
  DSAL:
    weight: 4
---

# Heap Basics

We consider the `minHeap` with `n` elements being stored. 

`minHeap`, is a complete binary tree, which can be stored in an array `A`. 

**Properties:**

1. Given the index of the element in the array `A`, the left child and right children of `A[i]` are `A[2i+1]` and `A[2i+2]` respectively. The parent of `A[i]` is `A[floor(i-1)/2]`.
2. (**Heap Property**)Excluding the root `A[0]`, `A[parent[i]] <= A[i]` for all $i>0$.

**Basic operations**

* `parent(i)`: return the parent of the node $i$.
* `left(i)`: return the left children of the node $i$.
* `right(i)`: return the right children of the node $i$.

* `insert(element)`: $O(\log(n))$. Put the inserted element at the end of the array. If it's larger than its parent, then there is nothing left to do. Otherwise, swap it with its parent. Repeat this process until either the inserted element becomes the first element of the array or find a parent which is smaller than the inserted element.

* `delete()`: $O(\log(n))$.  Place the root element in a variable to return later. Remove the last element in the deepest level and move it to the root. While the moved element has a value greater than at least one of its children, swap this value with the smaller-valued child.  Return the original root that was saved.


**heapify and build-heap**

* `heapify(A,i)`: Matain the **Heap Property** of a subtree rooted at `i`. Its inputs are an array `A` and an index `i` into the array. When `heapify(A,i)` is called, it is assumed that the binary trees rooted at `left(i)` and `right(i)` are `minHeaps`, but that `A[i]` may be larger than its children, thus violating the**Heap Property**. The function of `heapify(A,i)` is to let the value at `A[i]` "float down" in the heap so that the subtree rooted at index `i` becomes a heap. To achieve this, you just need to compare `A[i]` with `A[left(i)]` and `A[right(i)]` and swap when necessary. (Similart to `delete()` but nothing is deleted.) The complexity is $O(\texttt{height}(i))$, where $\texttt{height}(i)$ is the height of node `i` in the tree.

* `build-heap(L)`: Its input is an unsorted array `L` with size `n`. Then do the following.

  ```
    for i := floor(n/2) downto 1 
            do HEAPIFY(L, i); 
    end for 
  ```
  
  The last `floor(n/2)` elements of height 0, hence already are `minHeap` themselves. The total time comlexity is
  $$
    \sum_{h=1}^{\log_2(n)} \lceil \frac{n}{2^{h+1}}\rceil * O(\log_2(h)) = O(n).
  $$


# 215 数组中第k个最大元素

```
在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

示例 1:

输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
示例 2:

输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
说明:

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/kth-largest-element-in-an-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路

1. 利用前k个数构造一个大小为k的minHeap
2. 从第k+1个数开始将其与minHeap中的root相比较，如果比root大则移除root并插入该元素 （同时维持minHeap的性质）
遍历完成后，minHeap中为最大的k个数，且第k大的数在root

## 代码

```python
import heapq
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        minHeap = nums[:k]
        heapq.heapify(minHeap)
        for i in nums[k:]:
            if i > minHeap[0]:
                heapq.heappushpop(minHeap, i)
        return minHeap[0]
```

## 复杂度

1. 时间$O(k + (n-k)logk)$: 
    * 建大小为k的minHeap:  $O(k)$
    * 比较并(可能插入)n-k个元素: $O((n-k)log(k))$ 
2. 空间复杂度 $O(k)$

# 1046. 最后一块石头的重量

```
有一堆石头，每块石头的重量都是正整数。

每一回合，从中选出两块 最重的 石头，然后将它们一起粉碎。假设石头的重量分别为 x 和 y，且 x <= y。那么粉碎的可能结果如下：

如果 x == y，那么两块石头都会被完全粉碎；
如果 x != y，那么重量为 x 的石头将会完全粉碎，而重量为 y 的石头新重量为 y-x。
最后，最多只会剩下一块石头。返回此石头的重量。如果没有石头剩下，就返回 0。

 

示例：

输入：[2,7,4,1,8,1]
输出：1
解释：
先选出 7 和 8，得到 1，所以数组转换为 [2,4,1,1,1]，
再选出 2 和 4，得到 2，所以数组转换为 [2,1,1,1]，
接着是 2 和 1，得到 1，所以数组转换为 [1,1,1]，
最后选出 1 和 1，得到 0，最终数组转换为 [1]，这就是最后剩下那块石头的重量。
 

提示：

1 <= stones.length <= 30
1 <= stones[i] <= 1000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/last-stone-weight
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路

1.构建一个`maxHeap`
2.每次从`maxHeap`中`pop`两个出来(如果有元素的话)
3.如果`y-x>0` 则`push`进`maxHeap`直到`maxHeap`为空

## 代码

```python
import heapq
class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        if not stones:
            return 0
        maxHeap = [-i for i in stones]
        heapq.heapify(maxHeap)
        while len(maxHeap) > 1:
            y = -heapq.heappop(maxHeap)
            x = -heapq.heappop(maxHeap)
            if x != y:
                heapq.heappush(maxHeap, x-y)
        if not maxHeap:
            return 0
        else:
            return -maxHeap[0]
```

## 复杂度

* 时间复杂度：$O(nlog_2n)$
* 空间复杂度：$O(n)$

# 23. 合并k个升序链表

```
给你一个链表数组，每个链表都已经按升序排列。

请你将所有链表合并到一个升序链表中，返回合并后的链表。

 

示例 1：

输入：lists = [[1,4,5],[1,3,4],[2,6]]
输出：[1,1,2,3,4,4,5,6]
解释：链表数组如下：
[
  1->4->5,
  1->3->4,
  2->6
]
将它们合并到一个有序链表中得到。
1->1->2->3->4->4->5->6
示例 2：

输入：lists = []
输出：[]
示例 3：

输入：lists = [[]]
输出：[]
 

提示：

k == lists.length
0 <= k <= 10^4
0 <= lists[i].length <= 500
-10^4 <= lists[i][j] <= 10^4
lists[i] 按 升序 排列
lists[i].length 的总和不超过 10^4

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/merge-k-sorted-lists
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路一： 暴力合并k个链表

遍历`lists`里所有的链表，然后套用合并两个链表的模板。

### 代码

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        if not lists:
            return None
        n = len(lists)
        merged = lists[0]
        for i in range(1, n):
            tobeMerge = lists[i]
            l1 = merged
            l2 = tobeMerge
            ans = ListNode()
            cur = ans
            while l1 and l2:
                if l1.val <= l2.val:
                    cur.next = l1
                    l1 = l1.next
                else:
                    cur.next = l2
                    l2 = l2.next 
                cur = cur.next
            if l1 is None:
                cur.next = l2
            else:
                cur.next = l1
            merged = ans.next
        return merged
```
### 复杂度

* 时间复杂度: 假设`lists`里有`k`个链表，`n`为`k`个链表的最大长度。则时间复杂度为$O(k^2n)$
* 空间复杂度: $O(1)$

## 最小堆

### 思路
![image](https://user-images.githubusercontent.com/19240875/103142275-6a909680-46ce-11eb-9323-7478f1665fa6.png)

### 代码

```python
import heapq
# override default method for LitsNode class.
def __lt__(self, other):
    return  self.val < other.val
def __le__(self, other):
    return  self.val < other.val
ListNode.__lt__ = __lt__
ListNode.__le__ = __le__

class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        minHeap = []
        # 本来想用heapify但是存在[[],[]]输入。。。
        for node in lists:
            if node:
                heapq.heappush(minHeap, node)
        ans = ListNode()
        cur = ans
        while minHeap:
            curMin = heapq.heappop(minHeap)
            cur.next = curMin
            cur = cur.next
            if curMin.next:
                heapq.heappush(minHeap, curMin.next)
        return ans.next
```

### 复杂度

* 时间复杂度: 假设`lists`里有`k`个链表，`n`为`k`个链表的最大长度。则时间复杂度为$O(nk\log_2k)$
* 空间复杂度: $O(k)$ --- `minHeap`的大小
