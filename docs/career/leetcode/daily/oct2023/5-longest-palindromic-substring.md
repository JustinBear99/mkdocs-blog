---
date:
  created: 2023-10-27
  updated: 2023-11-28

description: >
  Solution for Leet Code 5. Longest Palindromic Substring

tags:
  - LeetCode

comments: true
---
# 5. Longest Palindromic Substring

## Description

The [problem](https://leetcode.com/problems/longest-palindromic-substring/?envType=daily-question&envId=2023-10-27) statement is clear while the only thing we need to notice is that the substring here is *contiguous* (some other questions may not limit to).

## Intuition

1. Loop over every charactor as the middle of a palindrome.
2. Find the length of the palindromic substring and compare it with current longest one.

## Code

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        # initilize return ans and index of char
        self.cur_max = s[0]
        i = 0
        while i < len(s):
            # two pointers point to the left and right char
            l, r = i, i
            self.findWithin(s, l, r)
            # if the pivot are two same chars, e.g. cbbc, find again
            if i + 1 < len(s) and s[i] == s[i + 1]:
                r += 1
                self.findWithin(s, l, r)
            i += 1        
        return self.cur_max

    def findWithin(self, s, l, r):
        while l >= 0 and r < len(s) and s[l] == s[r]:
            l -= 1
            r += 1
        # After leaving while loop, we actually need (l + 1) to (r - 1) substring
        # so check (r - 1) - (l + 1) + 1 > length of current max
        if r - l - 1 > len(self.cur_max):
            self.cur_max = s[l + 1: r]
```