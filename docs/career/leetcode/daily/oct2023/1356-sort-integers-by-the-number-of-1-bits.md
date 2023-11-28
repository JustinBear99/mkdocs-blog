---
date:
  created: 2023-10-30
  updated: 2023-11-28

description: >
	Solution for Leet Code 1356. Sort Integers by The Number of 1 Bits

tags:
    - LeetCode

comments: true
---

# 1356. Sort Integers by The Number of 1 Bits

## Description

[Sort](https://leetcode.com/problems/sort-integers-by-the-number-of-1-bits/description/?envType=daily-question&envId=2023-10-30) the given array by the count of 1 of its binary representation, if the counts of numbers are the same, sort with the value ascending.

## Code

```python
class Solution:
    def sortByBits(self, arr: List[int]) -> List[int]:
        return sorted(arr, key=lambda x : [bin(x).count('1'), x])s
```