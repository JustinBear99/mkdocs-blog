---
date:
    created: 2024-01-02
    updated: 2024-01-02

description: >
    Solution for Leet Code 2610. Convert an Array Into a 2D Array With Conditions

tags:
    - LeetCode

comments: true
---
# 2610. Convert an Array Into a 2D Array With Conditions

## Description

Redistribute the elements of an array to multiple sets.

## Code

```python
from collections import Counter
class Solution:
    def findMatrix(self, nums: List[int]) -> List[List[int]]:
        counter = Counter(nums)
        size = counter.most_common(1)[0][1]
        ret = [[] for _ in range(size)]
        for k, v in counter.items():
            for i in range(v):
                ret[i].append(k)
        return ret
```