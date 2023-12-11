---
date:
    created: 2023-12-11
    updated: 2023-12-11

description: >
    Solution for Leet Code 1287. Element Appearing More Than 25% In Sorted Array

tags:
    - LeetCode

comments: true
---
# 1287. Element Appearing More Than 25% In Sorted Array

## Description

Count and find the most frequent one

## Code

```python
class Solution:
    def findSpecialInteger(self, arr: List[int]) -> int:
        table = {}
        for num in arr:
            if num not in table:
                table[num] = 0
            table[num] += 1
        target = math.ceil(len(arr) / 4)
        ans, count = -1, 0
        for k, v in table.items():
            if v > count:
                count = v
                ans = k
        return ans
```