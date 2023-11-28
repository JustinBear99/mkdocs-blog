---
date:
    created: 2023-11-04
    updated: 2023-11-28

description: >
	Solution for Leet Code 1503. Last Moment Before All Ants Fall Out of a Plank

tags:
    - LeetCode

comments: true
---

# 1503. Last Moment Before All Ants Fall Out of a Plank

## Description

[There](https://leetcode.com/problems/last-moment-before-all-ants-fall-out-of-a-plank/) are two lines of ants moving on the same line. As they met each other, they switch the direction and keep moving avoiding each other.

## Intuition

The movement of ants is actually very simple. It doesn't matter when they meet since the result is the same as they **avoid** each other. So, we can treat them like the right-goers are on the one line and the left-goers are on the another.

1. The time for `left` to finish is `max(left)`
2. And the time for `right` to finish is `n - min(right)`
3. Since we can treat them on two independent lines, the answer is the `max()` of the above.

## Code

```python
class Solution:
    def getLastMoment(self, n: int, left: List[int], right: List[int]) -> int:
        # add default value for empty list
        return max(max(left, default=0), (n - min(right, default=n)))
```