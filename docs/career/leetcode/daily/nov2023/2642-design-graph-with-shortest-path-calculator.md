---
date:
    created: 2023-11-07
    updated: 2023-11-07

description: >
    Solution for Leet Code 2642. Design Graph With Shortest Path Calculator

tags:
    - LeetCode

comments: true
---
# 2642. Design Graph With Shortest Path Calculator

## Description

Classic shortest path question of applying Dijikstra's algorithm. Just be careful that the graph could be cyclic. A pretty good chance to review the graph related datqa strucure and algorithm. Here, we will use graph, priority queue, BFS, cache and dijikstra's.

I recommand to watch [neetcode's videos playlist for graph](https://www.youtube.com/playlist?list=PLot-Xpze53ldBT_7QA8NVot219jFNr_GI). Pretty helpful for beginner to learn and experienced to review, clear and clean.

## Code

```python
class Graph:

    def __init__(self, n: int, edges: List[List[int]]):
        self.n = n
        self.table = {i: set() for i in range(n)}
        for edge in edges:
            self.table[edge[0]].add((edge[2], edge[1]))

    def addEdge(self, edge: List[int]) -> None:
        self.table[edge[0]].add((edge[2], edge[1]))

    def shortestPath(self, node1: int, node2: int) -> int:
        heap = [(0, node1)]
        # stored visited node to prevent falling to cycle
        visited = set()
        # dijikstra's algo
        while heap:
            cur_path, cur_node = heapq.heappop(heap)
            if cur_node in visited:
                continue
            elif cur_node == node2:
                return cur_path
            visited.add(cur_node)

            for nei_path, nei_node in self.table[cur_node]:
                if nei_node not in visited:
                    heapq.heappush(heap, (cur_path + nei_path, nei_node))

        return -1

# Your Graph object will be instantiated and called as such:
# obj = Graph(n, edges)
# obj.addEdge(edge)
# param_2 = obj.shortestPath(node1,node2)
```