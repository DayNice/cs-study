# Depth-first search

An algorithm for traversing a tree data structure in search of a certain node. Can be applied to graph data structures by taking precautions against visiting the same node twice.

## Method

This is a recursive method, initialized by giving it a starting vertex as argument. First, label the given vertex as visited. Then check whether it is the target vertex. If not, for each of its unvisited neighbors call this method recursively. Note that depending on graph structure, a pending unvisited neighbor might be labeled as visited during a previous recursive call. Thus, neighbors should be checked individually whether they are visited or not, just before their recursive call. The algorithm traverses depth-first, just as its name implies.

A non-recursive version can be implemented by using a stack data structure. Initially, add the starting vertex into a stack. This stack is used to keep track of which vertex comes next. From then on repeat the following process until the stack becomes empty. Pop a vertex from the stack and determine whether it has been visited. If not, label it as visited, determine whether it is the target vertex, then add all of its neighbors to the stack. This method is simliar to that of the breadth-first search, except that it uses a stack instead of a queue and that it delays checking whether a vertex has been visited until the vertex is popped.

## Implementation

Python implementation of depth-first search.

```python
def dfs(adj_lists, v):
    # adj_lists = [[1, 2], [0, 4], [0, 4], [4], [1, 2, 3]]
    visited = [False] * len(adj_lists)
    visit_order = []
    dfs_helper(adj_lists, visited, visit_order, v)
    return visit_order


def dfs_helper(adj_lists, visited, visit_order, v):
    visited[v] = True
    visit_order.append(v)
    for i in adj_lists[v]:
        if not visited[i]:
            dfs_helper(adj_lists, visited, visit_order, i)

```

Python non-recursive implementation of depth-first search.

```python
def dfs_alt(adj_lists, v):
    # adj_lists = [[1, 2], [0, 4], [0, 4], [4], [1, 2, 3]]
    visited = [False] * len(adj_lists)
    stack = []
    stack.append(v)
    visit_order = []
    while len(stack) > 0:
        v = stack.pop()
        if visited[v]:
            continue
        visited[v] = True
        visit_order.append(v)
        stack.extend(reversed(adj_lists[v]))
    return visit_order

```

## References

1. <https://en.wikipedia.org/wiki/Depth-first_search>
