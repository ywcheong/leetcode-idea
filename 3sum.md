# 3sum
This is the step-by-step solution to solve the following problem on Leetcode.

* 3sum - *Top Interview 150*
  * https://leetcode.com/problems/3sum

To solve the problem, we need a two-pointer with hashing method.

At first sort the array, and record the last position (to be precise, the next of the last position) of the every adjacent elements. The following is an example.

```txt
1, 1, 2, 2, 2, 3, EOA
      ^        ^     ^
     [1:2]     [2:5] [3:6]
```

And select two element, `L[i]` and `L[j]`, then find `-(L[i]+L[j])` in the hash above.

The following python code is the implementation.

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        L = sorted(nums)
        result = []

        end_pos = dict()
        
        # hashing
        i = 0
        while i < len(L):
            value = L[i]
            while i < len(L) and value == L[i]:
                i += 1
            end_pos[value] = i

        i = 0
        while i < len(L):
            j = i + 1
            while j < len(L):
                required_value = -(L[i] + L[j])
                if required_value in end_pos:
                    k = end_pos[required_value]-1
                    if j < k:
                        result.append([L[i], L[j], L[k]])
                j = end_pos[L[j]]
            i = end_pos[L[i]]
        return result
```
