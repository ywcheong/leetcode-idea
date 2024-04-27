# word-pattern
This is the step-by-step solution to solve the following problem on Leetcode.

* Word Pattern - *Top Interview 150*
  * https://leetcode.com/problems/word-pattern

To solve the problem, we need a hashing method. By utilizing `dict` data structure, we can easily get whether unmatching pattern exists, for example, `a:dog` and `a:cat`.

Note that by submitting the problem with only given examples, we cannot prove the code's feasibilty of BIJECTION, which means two-way corresponding. `a:dog` and `b:dog` is also a wrong case. Therefore you should check if two equivalent value has been used by using two different keys.

The following python code is the implementation.

```python
class Solution:
    def wordPattern(self, pattern: str, s: str) -> bool:
        pattern_map = dict()
        pattern_value_set = set()
        sliced_str = s.split()

        # No hope when two length is different
        if len(pattern) != len(sliced_str):
            return False

        for i in range(len(pattern)):
            pattern_key = pattern[i]
            pattern_value = sliced_str[i]

            if pattern_key not in pattern_map:
                # check a:dog + b:dog
                if pattern_value not in pattern_value_set:
                    pattern_map[pattern_key] = pattern_value
                    pattern_value_set.add(pattern_value)
                else:
                    return False
            elif pattern_map[pattern_key] != pattern_value:
                # check a:dog + a:cat
                return False

        return True
```