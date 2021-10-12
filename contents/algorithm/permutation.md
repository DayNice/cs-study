# Permutation

A document about generating permutations in lexicographic order.

## Method

Given a sequence of elements, we can find the next permutation in lexicographic ordering by using the following steps. First, find the rightmost element smaller than its following neighbor and mark its index as *k*. This ensures that all elements after *k* are ordered in a decreasing manner. Next, from the sequence following *k* find the smallest element larger than the element at *k*, then swap their positions. Finally, reverse the sequence following *k* so that it is ordered in an increasing manner.

## Implementation

Python implementation for generating the next permutation in lexicographic ordering.

```python
def next_permutation(nums):
    k = len(nums) - 2
    while k >= 0 and nums[k] >= nums[k + 1]:
        k -= 1
    if k < 0:
        return
    i = len(nums) - 1
    while nums[i] <= nums[k]:
        i -= 1
    nums[k], nums[i] = nums[i], nums[k]
    nums[k + 1:] = reversed(nums[k + 1:])

```

## References

1. <https://en.wikipedia.org/wiki/Permutation>
1. <https://docs.python.org/ko/3/library/itertools.html#itertools.permutations>
