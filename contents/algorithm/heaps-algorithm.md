# Heap's algorithm

An algorithm for generating all possible permutations of *n* objects. It minimizes the number of swaps between elements.

## Method

This is a recursive method initially called with *k* = *n*. It calls itself *k* times with *k* - 1 as the argument, once with the sequence unaltered and then *k* - 1 times with the *k*<sup>th</sup> element exchanged with previous elements. The rule is that at the *i*<sup>th</sup> step of the remaining *k* - 1 calls, the *k*<sup>th</sup> element is swapped with the *i*<sup>th</sup> element if *k* is even, or with the first element otherwise. For the special case where *k* = 1 return the sequence as is.

## Implementation

Python implementation of Heap's algorithm.
```python
def generate_permutation(array, k):
    if k == 1:
        yield list(array)
    else:
        yield from generate_permutation(array, k - 1)
        for i in range(k - 1):
            if k % 2 == 0:
                array[i], array[k - 1] = array[k - 1], array[i]
            else:
                array[0], array[k - 1] = array[k - 1], array[0]
            yield from generate_permutation(array, k - 1)

```

Python implementation in non-recursive format.
```python
def generate_permutation_alt(array):
    yield array
    c = [0] * len(array)
    i = 1
    while i < len(array):
        if c[i] < i:
            if i % 2 == 0:
                array[0], array[i] = array[i], array[0]
            else:
                array[c[i]], array[i] = array[i], array[c[i]]
            yield array
            c[i] += 1
            i = 1
        else:
            c[i] = 0
            i += 1

```

## References

1. <https://en.wikipedia.org/wiki/Heap%27s_algorithm>
