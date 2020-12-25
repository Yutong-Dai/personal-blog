---
title: Union Find 并查集
linktitle: Union Find
toc: true
type: docs
date: "2020-12-14"
lastmod: "{{ .Lastmod }}"
draft: false
menu:
  DSAL:
    weight: 13
---

# 并查集的数据结构

[参考](https://github.com/leetcode-pp/91alg-2/blob/master/lecture/advanced-union-find-set.md).

```python
class UF:
    def __init__(self, n:int):
        """
        n: 图中有多少个node
        """
        # 初始化: 每个node是自己的根节点
        self.parent = [i for i in range(n)]
        # 初始化: 以自己为根节点的tree的size都是1
        self.size = [1] * n
        # 初始化: 连通图的个数
        self.count = n
    def find(self, node:int):
        while node != self.parent[node]:
            # 路径压缩
            self.parent[node] = self.parent[self.parent[node]]
            node = self.parent[node]
        return node
    def union(self, p:int, q:int):
        pRoot = self.find(p)
        qRoot = self.find(q)
        if pRoot != qRoot:
            # 小树挂在大树上
            if self.size[pRoot] >= self.size[qRoot]:
                self.parent[qRoot] = pRoot
                self.size[pRoot] += self.size[qRoot]
                self.size[qRoot] = None
            else:
                self.parent[pRoot] = qRoot
                self.size[qRoot] += self.size[pRoot]
                self.size[pRoot] = None
            self.count -= 1
      def connected(self, p:int, q:int):
          return self.find(p) == self.find(q)
```

应用:
  1. 确定无向图的连通分量


#  题目

```
班上有 N 名学生。其中有些人是朋友，有些则不是。他们的友谊具有是传递性。如果已知 A 是 B 的朋友，B 是 C 的朋友，那么我们可以认为 A 也是 C 的朋友。所谓的朋友圈，是指所有朋友的集合。

给定一个 N * N 的矩阵 M，表示班级中学生之间的朋友关系。如果M[i][j] = 1，表示已知第 i 个和 j 个学生互为朋友关系，否则为不知道。你必须输出所有学生中的已知的朋友圈总数。

 

示例 1：

输入：
[[1,1,0],
 [1,1,0],
 [0,0,1]]
输出：2 
解释：已知学生 0 和学生 1 互为朋友，他们在一个朋友圈。
第2个学生自己在一个朋友圈。所以返回 2 。
示例 2：

输入：
[[1,1,0],
 [1,1,1],
 [0,1,1]]
输出：1
解释：已知学生 0 和学生 1 互为朋友，学生 1 和学生 2 互为朋友，所以学生 0 和学生 2 也是朋友，所以他们三个在一个朋友圈，返回 1 。
 

提示：

1 <= N <= 200
M[i][i] == 1
M[i][j] == M[j][i]


来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/friend-circles
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路一： 并查集

消化模板中

![IMG_0273](https://user-images.githubusercontent.com/19240875/102106672-d9ccd780-3dfe-11eb-8579-767fe45178f7.jpg)


### 代码

```python
class UF:
    def __init__(self, n:int):
        """
        n: 图中有多少个node
        """
        # 初始化: 每个node是自己的根节点
        self.parent = [i for i in range(n)]
        # 初始化: 以自己为根节点的tree的size都是1
        self.size = [1] * n
        # 初始化: 连通图的个数
        self.count = n
    def find(self, node:int):
        while node != self.parent[node]:
            # 路径压缩
            self.parent[node] = self.parent[self.parent[node]]
            node = self.parent[node]
        return node
    def union(self, p:int, q:int):
        pRoot = self.find(p)
        qRoot = self.find(q)
        if pRoot != qRoot:
            # 小树挂在大树上
            if self.size[pRoot] >= self.size[qRoot]:
                self.parent[qRoot] = pRoot
                self.size[pRoot] += self.size[qRoot]
                self.size[qRoot] = None
            else:
                self.parent[pRoot] = qRoot
                self.size[qRoot] += self.size[pRoot]
                self.size[pRoot] = None
            self.count -= 1

class Solution:
    def findCircleNum(self, M: List[List[int]]) -> int:
        n = len(M)
        uf = UF(n)
        if n == 0:
            return 0
        for i in range(n):
            for j in range(i+1,n):
                if M[i][j] == 1:
                    uf.union(i, j)
        return uf.count
```

### 复杂度:

* 时间：$O(n^2)$
* 空间：$O(n)$

## 思路二: 无向图的搜索

### BFS

```python
M = [[1, 0, 0, 0, 0, 1], [0, 1, 1, 0, 1, 0], [0, 1, 1, 1, 0, 0], [0, 0, 1, 1, 0, 0], [0, 1, 0, 0, 1, 0], [1, 0, 0, 0 ,0, 1]]
class Solution:
    def findCircleNum(self, M):
        num_of_students = len(M)
        visited = [0] * num_of_students
        count = 0
        queue = []
        for i in range(num_of_students):
            print("Explore node {}".format(i))
            if visited[i]:
                print("node {} is visited".format(i))
                continue
            else:
                print("node {} is unexplored".format(i))
                queue.append(i)
                print("add node {} to queue | queue:{}".format(i, queue))
                visited[i] = 1
                print("mark node {} as visited".format(i))
            while queue:
                next_node_index = queue.pop(0)
                print("node to be explored:{}".format(next_node_index))
                for j in range(i, num_of_students):
                    if M[next_node_index][j] == 1 and visited[j] != 1:
                        print("node:{} and node:{} are connected!".format(next_node_index, j))
                        queue.append(j)
                        print("add node {} to queue | queue:{}".format(j, queue))
                        visited[j] = 1
                        print("mark node {} as visited".format(j))
            count += 1
            print("====")
        return count 
s = Solution()
s.findCircleNum(M)
```

# 1319. 连通网络的操作次数

```
用以太网线缆将 n 台计算机连接成一个网络，计算机的编号从 0 到 n-1。线缆用 connections 表示，其中 connections[i] = [a, b] 连接了计算机 a 和 b。

网络中的任何一台计算机都可以通过网络直接或者间接访问同一个网络中其他任意一台计算机。

给你这个计算机网络的初始布线 connections，你可以拔开任意两台直连计算机之间的线缆，并用它连接一对未直连的计算机。请你计算并返回使所有计算机都连通所需的最少操作次数。如果不可能，则返回 -1 。 

用以太网线缆将 n 台计算机连接成一个网络，计算机的编号从 0 到 n-1。线缆用 connections 表示，其中 connections[i] = [a, b] 连接了计算机 a 和 b。

网络中的任何一台计算机都可以通过网络直接或者间接访问同一个网络中其他任意一台计算机。

给你这个计算机网络的初始布线 connections，你可以拔开任意两台直连计算机之间的线缆，并用它连接一对未直连的计算机。请你计算并返回使所有计算机都连通所需的最少操作次数。如果不可能，则返回 -1 。 

示例 1：



输入：n = 4, connections = [[0,1],[0,2],[1,2]]
输出：1
解释：拔下计算机 1 和 2 之间的线缆，并将它插到计算机 1 和 3 上。
示例 2：



输入：n = 6, connections = [[0,1],[0,2],[0,3],[1,2],[1,3]]
输出：2
示例 3：

输入：n = 6, connections = [[0,1],[0,2],[0,3],[1,2]]
输出：-1
解释：线缆数量不足。
示例 4：

输入：n = 5, connections = [[0,1],[0,2],[3,4],[2,3]]
输出：0

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/number-of-operations-to-make-network-connected
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 思路

思考如下几个问题:

1. 什么时候无法把所有节点连接起来？当`connections`中给定的边的数量`len(connections)`少于无向图中的节点数量`n`时，一定无法构建一个连通图。当 `len(connections)`>`n`时， 我们一定知道可以通过移动某些边使得整个无向图连通。

2. 我们需要多少次操作呢？考虑有`n`个孤立的节点，我们只需要操作`n-1`次，即可构建一个连通的无向图。同理，如果我们有`k`个连通集，则只需要`k-1`次操作。所有问题变成找一个无向图连通集的个数`m`。然后返回答案`m-1`。

## 代码

```python
class UF:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.size = [1 for i in range(n)]
        self.count = n
    def find(self, p):
        while p != self.parent[p]:
            p = self.parent[p]
            # compression
            self.parent[p] = self.parent[self.parent[p]]
        return p
    def union(self, p, q):
        p_root = self.find(p)
        q_root = self.find(q)
        if p_root == q_root:
            return
        else:
            if self.size[p_root] >= self.size[q_root]:
                self.parent[q_root] = p_root
                self.size[p_root] += self.size[q_root]
                self.size[q_root] = None
            else:
                self.parent[p_root] = q_root
                self.size[q_root] += self.size[p_root]
                self.size[p_root] = None
            self.count -= 1
            
class Solution:
    def makeConnected(self, n: int, connections: List[List[int]]) -> int:
        nEdges = len(connections)
        # 线缆不足
        if nEdges < n - 1:
            return -1
        # 建立并查集
        uf = UF(n)
        for edge in connections:
            p, q = edge[0], edge[1]
            uf.union(p, q)
        return  uf.count - 1
```

## 复杂度

* 空间: $O(n)$ ----> n: 节点数
* 时间: $O(n+m\alpha(n))$   ---> m: 边的数量 \alpha(n) inverse Ackermann function. 每次find的cost 是$O(\alpha(n))$,几乎是一个常数。
