---
date:
    created: 2023-11-22
    updated: 2023-11-28

description: >
    Solution for Leet Code 1424. Diagonal Traverse II

tags:
    - LeetCode

comments: true
---
# 1424. Diagonal Traverse II

## Description

Sort 2-d matrix with given [order](https://leetcode.com/problems/diagonal-traverse-ii/description/?envType=daily-question&envId=2023-11-22).

## Intuition

The attribute of this diagonal order is that the position (i, j) of the same diagonal has same `i + j` value. Hence, we can sort the matrix by `i + j`, `j` and then `i`. However, the built-in sorting function has time complexity of O(nlogn) which is pretty slow.

To manually sort the matrix, we can still use that attribute and create a bucket for holding those value with order. Thus, the time complexity will drop to O(n)

## Code

```python
class Solution:
    def findDiagonalOrder(self, nums: List[List[int]]) -> List[int]:
        ## 1. O(nlogn)
        # s = set()
        # for i in range(len(nums)):
        #     for j in range(len(nums[i])):
        #         s.add((i + j, j, i, nums[i][j]))
        # return [n[3] for n in sorted(s)]

        ## 2. O(n)
        s = []
        for i in range(len(nums)):
            for j in range(len(nums[i])):
                # add a container for holding diagonal sum equals to (i+j)
                if i + j >= len(s):
                    s.append([])
                s[i + j].append(nums[i][j])
        return [ n for r in s for n in r[::-1]] # remember to reverse r(row) since we put values reversely
```