# minimun-window-substring
This is the step-by-step solution to solve the following problem on Leetcode.

* Minimun Window Substring - *Top Interview 150*
  * https://leetcode.com/problems/minimun-window-substring

To solve the problem, we need two-pointer method and an auxilary counting class with hashing. 

To elaborate in details, the auxilary class records `t`. We can push and pop a character into the class, and it can determine if the pushed elements can cover the given `t`.

With this class, we could use two-pointer method. Rules are:
* **Shrink left**, if the pushed-elements still covers `t`, to reduce its length
* **Extend right** if cannot, to obtain more characters.
* **Terminate** if cannot.

By using this rule, we are guaranteed to get an answer. The following python code is the implementation.

```python
def pick(s1, s2):
    if len(s1) < len(s2):
        return s1
    return s2

class Counter:
    def __init__(self, target):
        self.chars = dict()
        for c in target:
            self.force_pop(c)
    
    def push(self, c):
        if c in self.chars:
            self.chars[c] += 1
            return True
        return False

    def pop(self, c):
        if c in self.chars:
            self.chars[c] -= 1
            return True
        return False

    def force_pop(self, c):
        if c in self.chars:
            self.chars[c] -= 1
        else:
            self.chars[c] = -1

    def is_popable(self, c):
        if c not in self.chars:
            return True
        if self.chars[c] > 0:
            return True
        return False

    def is_feasible(self):
        for c in self.chars:
            if self.chars[c] < 0:
                return False
        return True

    def __str__(self):
        return str(self.chars)

class Solution:
    def minWindow(self, s: str, t: str) -> str:
        counter = Counter(t)
        start, end = 0, 0
        min_substr = s
        
        # adding phase;
        while end < len(s):
            if counter.push(s[end]):
                if counter.is_feasible():
                    end += 1
                    break
            end += 1

        if not counter.is_feasible():
            return ""
        
        min_substr = pick(s, s[start:end])
        
        # moving phase;
        while True:
            if counter.is_popable(s[start]):
                # action 1 : shrink left
                counter.pop(s[start])
                start += 1
                min_substr = pick(min_substr, s[start:end])
            elif end < len(s):
                # action 2. extend right
                counter.push(s[end])
                end += 1
            else:
                break
        
        return min_substr
```
