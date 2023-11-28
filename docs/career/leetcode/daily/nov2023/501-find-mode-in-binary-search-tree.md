---
date:
    created: 2023-11-01
    updated: 2023-11-28

description: >
    Solution for Leet Code 501. Find Mode in Binary Search Tree

tags:
    - LeetCode

comments: true
---
# 501. Find Mode in Binary Search Tree

## Description

The problem wants to find the most common appeared value of a BST. Since it's an easy problem, I'wll just traverse all nodes and record the value in a map. Then find the most common values (including values of same count).

## Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        ans = []
        ans_mode = 0
        self.modes = {}
        self.dfs(root)

        for key, value in self.modes.items():
            if value > ans_mode:
                ans = [key]
                ans_mode = value
            elif value == ans_mode:
                ans.append(key)
        return ans

    def dfs(self, node):
        if not node:
            return
        if node.val not in self.modes:
            self.modes[node.val] = 1
        else:
            self.modes[node.val] = self.modes[node.val] + 1
        self.dfs(node.left)
        self.dfs(node.right)
```