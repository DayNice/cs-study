# Lexicographic Permutation

A document about generating permutations in lexicographic order.

## Method

Given a sequence of comparable elements, it is evident that the smallest lexicographic permutation is obtained by sorting the elements in ascending order. In contrast the biggest permutation is obtained by sorting elements in descending order. Thus, the algorithm for finding lexicographic permutations is the process of converting an ascending sequence into a descending one.

To find the next lexicographic permutation in line we have to search for the rightmost slice that has reached its biggest permutation, reset it into its smallest permutation, then increase the weight of the index prior the slice by swapping elements. In other words, find the largest descending slice connected to the end of the current sequence. Reverse it to obtain ascending order. Then pick the element prior the slice and swap positions with the smallest element larger than it within the slice. Doing so does not break the ascending order, while increasing weight of the index prior the slice. As a result the next lexicographic permutation is obtained.

The whole set of permutations can be generated by recursively increasing weight of indexes starting from the end. The process of finding the smallest element larger than the element prior the slice can be simplified, as the position to be swapped is guaranteed to increase by one every cycle.

## Implementation

Python implementation for generating the next lexicographic permutation in line.

```python
def next_permutation(nums):
    k = len(nums) - 2
    while k >= 0 and nums[k] >= nums[k + 1]:
        k -= 1
    if k < 0:
        return
    nums[k + 1:] = reversed(nums[k + 1:])
    i = k + 1
    while nums[i] <= nums[k]:
        i += 1
    nums[k], nums[i] = nums[i], nums[k]

```

Python implementation for finding whole set of permutations in lexicographic order.
```python
def get_permutations(nums):
    n = len(nums)
    nums = sorted(nums)
    yield list(nums)
    # cycles are consumed from right to left
    cycles = list(range(n, 0, -1))
    while n:
        for i in range(n)[::-1]:
            # cycle consumed, swapping position increased by one
            cycles[i] -= 1
            if cycles[i] == 0:
                # reset to smallest permutation
                nums[i:] = nums[i + 1:] + nums[i:i + 1]
                # cycle restored by consuming upper cycle
                cycles[i] = n - i
            else:
                j = cycles[i]
                nums[i], nums[-j] = nums[-j], nums[i]
                yield list(nums)
                break
        else:
            # case all cycles are consumed
            return

```

## References

1. <https://en.wikipedia.org/wiki/Permutation>
1. <https://docs.python.org/3/library/itertools.html#itertools.permutations>