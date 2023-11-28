---
date:
    created: 2023-11-06
    updated: 2023-11-28

description: >
	Solution for Leet Code 1845. Seat Reservation Manager

tags:
    - LeetCode

comments: true
---
# 1845. Seat Reservation Manager

## Description

From the [problem](https://leetcode.com/problems/seat-reservation-manager/?envType=daily-question&envId=2023-11-06) statement, the manager is apparently an application of priority queue. In Python, there is a common used priority queue implementation named [`heapq`](https://docs.python.org/3/library/heapq.html) that uses heap (binary tree) to implement.

## Heap

There have been a lot of tutorial on this data structure on the net, so I just leave some useful links here (maybe write an explanation of my own version in the future XD).

[wiki](https://en.wikipedia.org/wiki/Heap_(data_structure)) [g4g](https://www.geeksforgeeks.org/heap-data-structure/)

## Code

```python
class SeatManager:

    def __init__(self, n: int):
        self.pq = [ i for i in range(1, n + 1)]

    def reserve(self) -> int:
        return heapq.heappop(self.pq)

    def unreserve(self, seatNumber: int) -> None:
        heapq.heappush(self.pq, seatNumber)


# Your SeatManager object will be instantiated and called as such:
# obj = SeatManager(n)
# param_1 = obj.reserve()
# obj.unreserve(seatNumber)
```