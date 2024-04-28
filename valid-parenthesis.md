# valid-parenthesis
This is the step-by-step solution to solve the following problem on Leetcode.

* Valid Parenthesis - *Top Interview 150*
  * https://leetcode.com/problems/valid-parenthesis

To solve the problem, we need a stack. Note that this problem is extremely error-prone. We should check *every* of the followings to avoid common mistakes.

* Wrong close : `(]`, `][`
* More close : `]`
* Not closed : `(`

The following python code is the implementation.

```python
OPEN_CLOSE = {
    '(' : ')',
    '[' : ']',
    '{' : '}',
}

class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        for char in s:
            if char in OPEN_CLOSE:
                stack.append(char)
            else:
                if len(stack) == 0:
                    # more close
                    return False
                top = stack.pop()
                if OPEN_CLOSE[top] != char:
                    # wrong close
                    return False
        return len(stack) == 0 # not closed
```
