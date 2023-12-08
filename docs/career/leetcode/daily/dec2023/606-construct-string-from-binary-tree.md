---
date:
    created: 2023-12-08
    updated: 2023-12-08

description: >
    Solution for Leet Code 606. Construct String from Binary Tree

tags:
    - LeetCode

comments: true
---
# 606. Construct String from Binary Tree

## Description

Find the string form of given binary tree with preorder traversal.

## Code

DFS and remember to add empty parenthesis, `()`, for *null left subtree* while *right subtree not null*.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def tree2str(self, root: Optional[TreeNode]) -> str:
        ret = []
        if root:
            ret.append(str(root.val))
        else:
            return ""
        
        if root.left or root.right:
            ret.append("(")
            ret.append(self.tree2str(root.left))
            ret.append(")")
        if root.right:
            ret.append("(")
            ret.append(self.tree2str(root.right))
            ret.append(")")
        return "".join(ret)
```