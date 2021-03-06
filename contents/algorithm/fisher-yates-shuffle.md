# Fisher-Yates shuffle

An algorithm for providing random unbiased permutations of a finite sequence.

## Method

Initially, consider all elements to be unstruck. Choose one unstruck element, mark it as struck, then line it up with struck elements. Repeat this process until there are no more unstruck elements. Consequently, the order of struck elements becomes a random permutation.

The *i*<sup>th</sup> step introduces *n* - *i* + 1 possibilities, resulting in a series of multiplications from *n* to 1. This is in accordance with the fact that *n*! different permutations result from a sequence of *n* elements.

An alternative method is to start with an empty array, then subsequently insert elements from the original sequence. Each new element either pushes an occupying element, sending it to the end of the array, or simply appends itself. The advantage of this method is that new arrays can be obtained and shuffled simultaneously, without affecting the original sequence.

## Implementation

Python implementation of Fisher-Yates shuffle.

```python
from random import randrange

def shuffle(nums):
    for i in range(len(nums) - 1):
        j = randrange(i, len(nums))
        nums[i], nums[j] = nums[j], nums[i]

```

Python implementation of the alternative method.

```python
from random import randrange

def shuffle_alt(nums):
    new_nums = []
    for i in range(len(nums)):
        j = randrange(i + 1)
        if j != i:
            new_nums.append(new_nums[j])
            new_nums[j] = nums[i]
        else:
            new_nums.append(nums[i])
    return new_nums

```

## References

1. <https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle>
