---
date:
  created: 2023-11-21
  updated: 2023-11-21

tags:
    - LeetCode

comments: true
---
# 1814. Count Nice Pairs in an Array

## Description

We are asked to find the number of pairs `(a, b)` such that `a + reverse(b) = reverse(a) + b` where `reverse()` reverses the integer by its string representation.

## Intuition

Slightly change the equation `a + reverse(b) == reverse(a) + b` to `a - reverse(a) = b - reverse(b)` so then we can simply make a hash table to store the count by the difference (n - reverse(n)).

Be aware of the edge cases for `reverse()` and remember to `/2` for duplicated pairs.

## Code

```python
class Solution:
    def countNicePairs(self, nums: List[int]) -> int:
        rev_nums = [ self.reverse(num) for num in nums]
        table = {}
        for i in range(len(nums)):
            diff = nums[i] - rev_nums[i]
            if diff not in table:
                table[diff] = 0
            table[diff] += 1
        ans = 0
        for val in table.values():
            if val > 1:
                ans += int(val * (val - 1) / 2)
        return ans % (10 ** 9 + 7)
        
    def reverse(self, num):
        s = []
        while num >= 10:
            q = num % 10
            num = num // 10
            s.append(q)
        if num > 0:
            s.append(num)

        i = 0
        rev = 0
        while s:
            rev += (10 ** i) * s.pop()
            i += 1
        return int(rev)
```