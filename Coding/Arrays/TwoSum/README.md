# Two sum

## Introduction
Given an array of numbers `nums` and a `target`, return the indices of two numbers in `nums` that sum to `target`.

TwoSum is a quintessential coding puzzle and one all CS students applying for tech jobs should be familiar with. There are many variants to this problem including `ThreeSum`, `FourSum`, etc. There are also many flavors for `TwoSum` where you might have to return all possible pairs of indices of numbers that sum to target. You might even have to handle the case where no two numbers in `nums` sum to `target`.

However, in this case we're going to assume that only a single pair exists.

## Brute Force

The simplest, brute force solution runs in O(N^2). We need to do a lested for loop, and when we find two numbers that sum up to `target` we return their indices.

```py
def two_sum(nums, target):

    # declare variable for length of nums
    N = len(nums)

    # we iterate for every num
    for i in range(N):

        # search all other numbers for a complement
        for j in range(M):

            # see if we have a match
            if nums[i] + nums[j] == target:
                #return index
                return [i, j]

```

## Linear time solution

We can implement a linear time solution. How do we do that? We can store the numbers we've seen along with each numbers index in a dictionary. When we see a new `num` in `numbers`, we can quickly calculate `num`'s `complement`. The `complement` is the other number needed to make the sum equal to `target`. We know that we need `num + complement = target`. We can subtract `num` from both sides to get `complement = target - num`. Here's the trick: if the `complement` is in our dictionary, then we've found our pair! If we haven't seen the complement before we store `num` along with its index in case it might be the complement for another number down the line.

This runs in O(N) time and O(N) space.

```py
def two_sum(nums, target):

    # store a dictionary mapping (num -> index) 
    # of the nums seen so far
    seen = {}
    
    # iterate through all numbers
    for idx, num in enumerate(nums):

        # calculate complement needed
        complement = target - num

        # have we seen this complement before
        if complement in seen:
            # return indices
            return [idx, seen[complement]]

        # if we don't find the complement, store num for later
        # by mapping it to its index
        seen[num] = idx
```