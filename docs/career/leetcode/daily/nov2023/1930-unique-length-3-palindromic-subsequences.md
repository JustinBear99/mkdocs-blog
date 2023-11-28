---
date:
    created: 2023-11-14
    updated: 2023-11-28

description: >
    Solution for Leet Code 1930. Unique Length-3 Palindromic Subsequences

tags:
    - LeetCode

comments: true
---
# 1930. Unique Length-3 Palindromic Subsequences

## Description

The name of [question](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/?envType=daily-question&envId=2023-11-14) is already pretty clear so I don't repeat again.

At the start of this question, I always start with the most intuitive approach. Therefore, I tried to for loop each character of `s` and make set intersection for the left substring and right substring. However, this will lead to time complexity of `O(n^2)` and the submission will be TLE.

## Intuition

Refers to [lee215's solution](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/solutions/1330178/python-straight-forward-solution/?envType=daily-question&envId=2023-11-14), this question can easily be linear time since the number of lowercase characters is limited.

1. For loop `a` to `z` to find the first index of that character from left and right.
2. Find the unique characters in between those indexes and sum to `ans`

This approach simply reverse the order of finding palindrome and the middle character which is clever. 😆

##

```python
class Solution:
    def countPalindromicSubsequence(self, s: str) -> int:
        ## TLE O(n**2)
        # ans = set()
        # for i in range(1, len(s) - 1):
        #     right = s[:i]
        #     mid = s[i]
        #     left = s[i+1:]
        #     for inter in set(right).intersection(left):
        #         if (inter, mid) not in ans:
        #             ans.add((inter, mid))

        # return len(ans)

        ans = 0
        for c in string.ascii_lowercase:
            i, j = s.find(c), s.rfind(c)
            if i > -1:
                ans += len(set(s[i + 1: j]))
        return ans
```