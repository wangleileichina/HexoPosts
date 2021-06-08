---
title: UnionFindSet
date: 2021-06-05 18:16:06
tags:
  - UnionFind
---


```python
from collections import defaultdict

class UnionFind:
    def __init__(self, n, nums):
        self.nums = nums
        self.parent = defaultdict(int)
        self.size = defaultdict(int)
        for i in range(len(self.nums)):
            self.parent[i] = i
            self.size[i] = 1

    def find(self, x):
        # 查找根节点，即当前元素所属的集合
        r = x
        if r != self.parent[r]:
            r = self.parent[r]
        return r

    def union(x, y, size):
        x_root = self.find(x)
        y_root = self.find(y)
        if x_root != y_root:
            if size[x_root] > size[y_root]:
                self.parent[y_root] = x_root
                self.size[x_root] += self.size[y_root]
            else:
                self.parent[x_root] = y_root
                self.size[y_root] += self.size[x_root]
```



```python
from collections import defaultdict


# 查根
def find(x, parent):
    r = x
    while r != parent[r]:
        r = parent[r]
    return r


def union(x, y, parent,size):
    x_root = find(x, parent)
    y_root = find(y, parent)
    # 将x作为根节点
    if x_root != y_root:
        if size[x_root] > size[y_root]:
            parent[y_root] = x_root
            size[x_root] += size[y_root]
        else:
            parent[x_root] = y_root
            size[y_root] += size[x_root]


class Solution(object):
    def findCircleNum(self, M):
        """
        :type M: List[List[int]]
        :rtype: int
        """
        parent = defaultdict(int)
        size = defaultdict(int)
        ans = set()
        if not M:
            return 0
        for i in range(len(M)):
            parent[i] = i
            size[i] = 1
        for i in range(len(M)):
            for j in range(i, len(M[0])):
                if M[i][j] == 1:
                    union(i, j, parent,size)

        for i in parent:
            ans.add(find(i, parent))

        return len(ans)

a = Solution()
print(a.findCircleNum([[1, 1, 0], [1, 1, 0], [0, 0, 1]]))
```