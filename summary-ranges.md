# summary-ranges
This is the step-by-step solution to solve the following problem on Leetcode.

* Summary Ranges - *Top Interview 150*
  * https://leetcode.com/problems/summary-ranges

To solve the problem, we need just a calm implementation.

Note that while summarizing the array, we pushes `+inf` at the end of the array. This is a simple but powerful trick to process the termination of the last-index easily. If the *interval* is still not closed at the end of the array, `+inf` forcefully closes it.

The following python code is the implementation.

```python
class Solution:
    def summaryRanges(self, nums: List[int]) -> List[str]:
        # base case
        if len(nums) == 0:
            return []
        if len(nums) == 1:
            return [str(nums[0])]
        
        stack = []
        start, end = nums[0], nums[0]
        nums = nums[1:] + [float("inf")] # sake of easy-termination

        for i in range(len(nums)):
            value = nums[i]
            if value == end + 1:
                end = value
            else: # +inf got in this trap
                stack.append((start, end))
                start, end = value, value
        
        # (start,end) tuple --convert--> "start->end" str
        result = []
        for start, end in stack:
            if start == end:
                result.append(f"{start}")
            else:
                result.append(f"{start}->{end}")

        return result
```
