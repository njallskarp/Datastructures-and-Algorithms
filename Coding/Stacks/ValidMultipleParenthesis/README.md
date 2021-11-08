# Valid Multiple Parenthesis

## Introduction

Given a string `s` that has three types of parenthesis `{}`, `[]`, and `()` determine if the parenthesis are valid. We can assume that the only characters in the string are one of those six.

## O(N) solution

It is important to note that this problem is fundamentally different than the same problem with just a single type of parenthesis. However, what's alike is that we can never have more closing parenthesis than open ones and in the end we must have closed all open parenthesis.

What's different is that we can not have anything of the sorts `(]`. It is okay to have interleaved different types but we need to close them in the same order that they were open.

To do that, we need a stack. On this stack we will store all open parenthesis. We will iterate for each `char` in `s`. Whenever we see an opening parenthesis, we add it to the `stack`. If the `char` is a closing parenthesis, we can check if the stack is empty. If the stack is empthy then we have no open parenthesis to close with the current `char` and return `False` immediately. If, however the stack is not empty, we `.pop()` the top off the stack. If the popped element is **not** opening equivalent of `char` then we return `False`. If it is, however then we live to see another `char`.

```py
def is_valid(self, s: str) -> bool:
        
    stack = []
    
    open_to_close = {
        '{': '}',
        '[': ']',
        '(': ')'
    }
    
    for char in s:
        if char in ['(', '{', "["]:
            stack.append(char)
        elif char in [')', '}', ']'] and not stack:
            return False
        elif open_to_close[stack.pop()] != char:
            return False
        
    return len(stack) == 0

```