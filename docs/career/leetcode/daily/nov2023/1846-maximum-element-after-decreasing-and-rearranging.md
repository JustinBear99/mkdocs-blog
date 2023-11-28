---
date:
    created: 2023-11-15
    updated: 2023-11-28

description: >
    Solution for Leet Code 1846. Maximum Element After Decreasing and Rearranging

tags:
    - LeetCode

comments: true
---
# 1846. Maximum Element After Decreasing and Rearranging

## Description

We are asked to find the maximum value from a array which will change after satisfying the rules required. Basically, after sorting the array, since the increment between elements is atmost 1, we just update the element and return the last element.

## Code

```python
class Solution:
    def maximumElementAfterDecrementingAndRearranging(self, arr: List[int]) -> int:
        arr.sort()
        # edge case
        if arr[0] != 1:
            return len(arr)
        for i in range(1, len(arr)):
            if arr[i] - arr[i - 1] > 1:
                arr[i] = arr[i - 1] + 1
        return arr[-1]
```