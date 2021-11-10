# Breadth-first search

An algorithm for traversing a tree data structure in search of a certain node. Can be applied to graph data structures by taking precautions against visiting the same node twice.

## Method

Initially, label the starting vertex as visited, then add it into a queue. This queue is used to keep track of which vertex comes next. From then on repeat the following process until the queue becomes empty. Dequeue a vertex from the queue and determine whether it is the target vertex. If not, enqueue all of its unvisited neighbors, labeling them as visited in the process. The algorithm traverses breadth-first, just as its name implies.

## Implementation

Python implementation of breadth-first search.

```python
from collections import deque

def bfs(adj_lists, v):
    # adj_lists = [[1, 2], [0, 4], [0, 4], [4], [1, 2, 3]]
    visited = [False] * len(adj_lists)
    visited[v] = True
    queue = deque()
    queue.append(v)
    visit_order = []
    while len(queue) > 0:
        v = queue.popleft()
        visit_order.append(v)
        for i in adj_lists[v]:
            if not visited[i]:
                visited[i] = True
                queue.append(i)
    return visit_order

```

## References

1. <https://en.wikipedia.org/wiki/Breadth-first_search>
