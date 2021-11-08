# Palindromic Number

## Introduction

For this problem, we're given a single number called `num`. We're tasked with deciding if that number is a palindrome or not. What distinguishes this problem from most other palindrome problems is that the input is an integer. Of course, we could cast the number to a string and compare chars `0, n-1`, `1,n-2`, etc. But what's the fun in that? We can actually do this without casting the number to another type.

## O(N) solution
The first two lines are quite trivial, once we understand the logical checks themselves. 

First of all, `-1` can never be a palindrome. Why is that? Well, there is no valid number which is the reverse of `-1`. We see that `1-` doesn't make any sense. The same goes for every negative number. That's the check we're performing in the first line.

Second of all, `10` can never be a palindrome. The pattern we have to observe here is that it's reverse `01` is never a valid integer. The general pattern is that, every number (greater than 0) that ends with `0` will never be a palindrome. That's the check we do in the second line.

Next up we want to be able to loop through all the digits in `num`. First, we need to declare two variables: `reverse` and `original`. Original is just a copy that we want to keep of `num`, because we'll end up modifying `num`. Secondly, we declare `reverse` to be zero. We'll add the digits, one by one from `num` to `reverse`.

### The while loop

Notice that we loop until `num` is no longer greater than zero. This means that once we've transported all the digits to `reverse` in reversed order we stop looping. What's going on in the loop?

First off, we read the least significant digit `lsd` from `num`. If we have the number `abcdefg`, where each letter represents some digit `0-9`, then `lsd` will be the same digit as `g`. This is what we call the least significant digit, which is actuallly the right most one.

What we do next is quite important: we multiply reverse by a factor of `10` and then add the digit. If reverse is equal to `gfe` and we have `lsd = d` then multiplying by `10` gives `gfe0` and adding `d` finally gives us `gfed`.

Lastly, we divide num by 10 (integer division). This effectively removes the `lsd` from `num`.

After the loop completes, we can check if `original == reverse`. If they're the same number, then `num` is (by definition) a palindrome

```py
def number_palindrome(self, num: int) -> bool:
    if num < 0: return False
    if num % 10 == 0 and num > 0: return False

    reverse = 0
    original = num

    while num > 0:
        lsd = num % 10
        reverse = 10 * reverse + lsd
        num //= 10
        
    return original == reverse
```
        