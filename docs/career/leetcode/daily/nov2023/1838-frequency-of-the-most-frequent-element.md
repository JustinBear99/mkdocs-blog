---
date:
  created: 2023-11-18
  updated: 2023-11-18

tags:
    - LeetCode

comments: true
---
# 1838. Frequency of the Most Frequent Element

## Description

We are given `k` quota to increase the elements in `nums` to maximize the number of any value.

## Intuition

1. Sort the array since we can only *add* value to the elements and only the smaller element should be considered added for larger element.
2. Use two poninters (sliding window) to determine how many elements can be increased and be equal to the larger element.
3. Also, use prefix sum to prevent repetitive summation.

## Code

```python
class Solution:
    def maxFrequency(self, nums: List[int], k: int) -> int:
        nums.sort()
        n = len(nums)
        psum = [0] * (n + 1)
        i, j = 0, 0
        ans = 0
        while j < n:
            psum[j] = psum[j - 1] + nums[j]
            if (nums[j] * (j - i + 1)) - (psum[j] - psum[i - 1]) <= k:
                ans = max(ans, j - i + 1)
                j += 1
            else:
                i += 1
        return ans
```