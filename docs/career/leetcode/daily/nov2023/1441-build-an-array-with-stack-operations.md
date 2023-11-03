---
date:
  created: 2023-11-03
  updated: 2023-11-03

tags:
    - LeetCode

comments: true
---

# 1441. Build an Array With Stack Operations

## Description

[Given](https://leetcode.com/problems/build-an-array-with-stack-operations/description/?envType=daily-question&envId=2023-11-03) a array with numbers range from **1** to **n**, return the operation list to form the array.

## Intuition

There are only two situation we faced with the `target` while growing the number stream **n**
1. n == target entry: **Push** into the operation list.
2. n != target entry: **Push** and then **Pop** since we don't need it. (could only be *less than*, so I use `while` loop)

## Code

```python
class Solution:
    def buildArray(self, target: List[int], n: int) -> List[str]:
        ans = []
        s = 1
        for t in target:
             # s always < n, don't bother to check
            while s < t:
                s += 1
                ans.append("Push")
                ans.append("Pop")
            s += 1
            ans.append("Push")
        return ans
```

## Complexity

The time complexity is $$O(m)$$ where m is the last entry of `target`.

The space complexity is $$O(m+n)$$ where m is the last entry of `target` and n is m minus the length of `target`.