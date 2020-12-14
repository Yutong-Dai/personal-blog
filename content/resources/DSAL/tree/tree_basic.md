---
title: Basics of tree data structure and algorithms
linktitle: tree-concepts-algorithm
toc: true
type: docs
date: "2020-08-16"
lastmod: "{{ .Lastmod }}"
draft: false
menu:
  DSAL:
    parent: Tree and Graph
    weight: 1
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

# Traverse Algorithms

## Pre-order
The pre-order traversal visit nodes in `root - left - right` order, where the the root appears in the first.

### recursion implementation

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        self.ans = []
        self.dfs(root)
        return self.ans
    def dfs(self, node):
        if not node: return
        self.ans.append(node.val)
        if node.left: self.dfs(node.left)
        if node.right: self.dfs(node.right)
```

### iterative implementation

```python
# iterative
# hint: using stack and add children using right-left order.
from collections import deque
class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if not root:
            return []
        stack = deque()
        stack.appendleft(root)
        ans = []
        while stack:
            node = stack.popleft()
            ans.append(node.val)
            if node.right: stack.appendleft(node.right)
            if node.left: stack.appendleft(node.left)
        return ans
```

## In-order

The in-order traversal visit nodes in `left-root-right` order, where the the root appears in the middle.
recursion implementation

### Recursion

```python
class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        self.ans = []
        self.dfs(root)
        return self.ans
    def dfs(self, node):
        if not node: return
        if node.left: self.dfs(node.left)
        self.ans.append(node.val)
        if node.right: self.dfs(node.right)
```
### iterative implementation

```python
from collections import deque        
class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if not root:
            return []
        self.stack = deque()
        ans = []
        while root or self.stack:            # need add root here
            while root:
                self.stack.appendleft(root)
                root = root.left
            node = self.stack.popleft()
            ans.append(node.val)
            root = node.right
        return ans 
```
**discussion: why the following code is wrong?**

```python
from collections import deque        
class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if not root:
            return []
        self.stack = deque()
        self.stack.appendleft(root)
        ans = []
        while root or self.stack:
            while root:
                if root.left: self.stack.appendleft(root.left)
                root = root.left
            node = self.stack.popleft()
            ans.append(node.val)
            root = node.right
        return ans
```

```
Hint: following edge cases would fail.
   1
    \
     2
    /
   3
```

When the node `1` is poped out of the stack. The stack is empty. But we still need to  explore its right child.

## Post-order

The post-order traversal visit nodes in `left-right-root` order, where the the root appears in the last.
### recursion implementation

```python
class Solution(object):
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        self.ans = []
        self.dfs(root)
        return self.ans
    def dfs(self, node):
        if not node:
            return []
        if node.left: self.dfs(node.left)
        if node.right: self.dfs(node.right)
        self.ans.append(node.val)
```

### iterative implementation
The idea is to hack the pre-order traversal, which visit nodes in `root-left-right` order. If we visit in the `root-right-left` order and reverse it, then we get `left-right-root` order.

```python
from collections import deque
class Solution(object):
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        while not root:
            return []
        ans = []
        stack = deque()
        stack.appendleft(root)
        while stack:
            # root-right-left order
            # reverse it; left-right-root
            node = stack.popleft()
            ans.append(node.val)
            if node.left: stack.appendleft(node.left)
            if node.right: stack.appendleft(node.right)
        return ans[::-1]
```

## Summary: templates

### recursion

### iterative 
[Reference](https://leetcode-solution-leetcode-pp.gitbook.io/leetcode-solution/thinkings/binary-tree-traversal#shuang-se-biao-ji-fa)

## Level-order

From left to right from  root to leaf.

```python
from collections import deque
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root:
            return []
        queue = deque()
        ans = []
        queue.append(root)
        while queue:
            node = queue.popleft()
            ans.append(node.val)
            if node.left: queue.append(node.left)
            if node.right: queue.append(node.right)
        return ans
```        

### Variant: level aware method

[Leet-code: 102](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

```
给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

 

示例：
二叉树：[3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]


来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/binary-tree-level-order-traversal
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```


The key is to create a variable to record number of nodes in current level.

```python
from collections import deque
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root:
            return []
        queue = deque()
        ans = []
        queue.append(root)
        while queue:
            temp = []
            num_nodes_in_current_level = len(queue)
            while num_nodes_in_current_level > 0:
                node = queue.popleft()
                temp.append(node.val)
                if node.left: queue.append(node.left)
                if node.right: queue.append(node.right)
                num_nodes_in_current_level -= 1
            # when reach this line, nodes in current level has been all explored
            ans.append(temp)
        return ans
```
