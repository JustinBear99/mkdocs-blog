---
date:
    created: 2023-11-24
    updated: 2023-11-28

description: >
	Solution for Leet Code 1561. Maximum Number of Coins You Can Get

tags:
    - LeetCode

comments: true
---
# 1561. Maximum Number of Coins You Can Get

## Description

We are given array `piles` of length *3n* and asked to find the maximum sum from selecting piles followed by the [rules](https://leetcode.com/problems/maximum-number-of-coins-you-can-get/description/?envType=daily-question&envId=2023-11-24).

## Intuition

Simply a sorting question. After sorted reversely (from large to small), the array looks like

```
 L M L M L M L M S S S S 
|------2/3------|--1/3--|
```

Now, we just need to sum up all `M` values

## Code

```python
class Solution:
    def maxCoins(self, piles: List[int]) -> int:
        piles.sort(reverse=True)
        return sum([ piles[i] for i in range(1, int(len(piles) * 2 / 3), 2)])
```