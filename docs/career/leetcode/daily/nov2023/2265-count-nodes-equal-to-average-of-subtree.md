---
date:
    created: 2023-11-02
    updated: 2023-11-28

description: >
    Solution for Leet Code 2265. Count Nodes Equal to Average of Subtree

tags:
    - LeetCode

comments: true
---

# 2265. Count Nodes Equal to Average of Subtree

## Description

[Problem](https://leetcode.com/problems/count-nodes-equal-to-average-of-subtree/description/?envType=daily-question&envId=2023-11-02) statement:

Given the `root` of a binary tree, return **the number of nodes** where the value of the node is equal to the **average** of the values in its **subtree**.

Note that the average of n elements is the sum of the n elements divided by n and *rounded down* to the nearest integer.

## Intuition

Since the problem wants to find something with respect to the root node of all subtree, we use dfs to find the values we need.

1. See from the root node, we need the sum and the number of node from both its left and right subtree in order to calculate the average of the root node.
2. Therefore the return values of dfs function are the sum and the numbers of nodes (count).
3. Dfs from root and store answer in a private variable.

## Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def averageOfSubtree(self, root: Optional[TreeNode]) -> int:
        self.ans = 0
        if root:
            self.dfs(root)

        return self.ans
        
    def dfs(self, node):
        s = node.val
        count = 1
        # get the sum and the count from left and right subtree
        if node.left:
            sub_s, sub_count = self.dfs(node.left)
            s += sub_s
            count += sub_count
        if node.right:
            sub_s, sub_count = self.dfs(node.right)
            s += sub_s
            count += sub_count
        # check if the value of the node equals to the average
        if node.val == int(s / count):
            self.ans += 1
        return s, count
```