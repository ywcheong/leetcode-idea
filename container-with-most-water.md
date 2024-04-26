# container-with-most-water
This is the step-by-step solution to solve the following problem on Leetcode.

* Container with Most Water - *Top Interview 150*
  * https://leetcode.com/problems/container-with-most-water

To solve the problem, we need a two-pointer method.

We start from the full-width tank, with `start, end = 0, len(height) - 1`. By shrinking both ways, but by applying shorter-shrink-first greedy rule, we can obtain the correct result. This terminates when `start < end` assertion is broken.

The following python code is the implementation.

```python
def getArea(height, start, end):
    return min(height[start], height[end]) * (end - start)

class Solution:
    def maxArea(self, height: List[int]) -> int:
        start, end = 0, len(height) - 1
        result = getArea(height, start, end)

        # two actions in choice
        # 1. shrink start (+1)
        # 2. shrink end (-1)
        # terminate if both failed
        while start < end:
            if height[start] < height[end]:
                start += 1
            else:
                end -= 1
            result = max(result, getArea(height, start, end))
        return result
```
