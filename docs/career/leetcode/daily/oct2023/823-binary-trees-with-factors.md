---
date:
    created: 2023-10-26
    updated: 2023-11-28

description: >
	Solution for Leet Code 823. Binary Trees with Factors

tags:
    - LeetCode

comments: true
---

# 823. Binary Trees with Factors

## Description

The [problem](https://leetcode.com/problems/binary-trees-with-factors/description/?envType=daily-question&envId=2023-10-26]) wants us to find the number of possible binary trees that the value of each node equals to the product of its child nodes (both child nodes exist).

## Intuition

Since every node (except leaf) can be one of the child nodes of another node, we can use dynamic programming to sum up the combination from small tree to big tree. For the example1 in the link, 

1. Sort the given array in ascending order.
2. Initialize map to store available pair count for every unique node.
3. Loop over possible combination from small to big tree.

## Code

```python
class Solution:
    def numFactoredBinaryTrees(self, arr: List[int]) -> int:
        # step 1
        arr.sort()
        # step 2
        dp = {x: 1 for x in arr}
        # step 3: loop over every combination, O(n^2)
        for i in arr:
            for j in arr:
                # neglect impossible factor
                if j > i ** 0.5:
                    break
                # look for valid factor
                if i % j == 0 and i // j in arr:
                    if i // j == j:
                        # e.g. 4 / 2 = 2, then dp[4] will have dp[2]^2 more composition since the left and right child can be dp[2]
                        dp[i] += dp[j] * dp[j]
                    else:
                        # <* 2> because we can swap left and right
                        dp[i] += dp[j] * dp[i // j] * 2
        return sum(dp.values()) % (10 ** 9 + 7)

```