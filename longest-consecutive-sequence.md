# longest-consecutive-sequence
This is the step-by-step solution to solve the following problem on Leetcode.

* Longest Consecutive Sequence - *Top Interview 150*
  * https://leetcode.com/problems/longest-consecutive-sequence

To solve the problem, we need a hashing to achieve the `O(n)` time complexity restriction.

We hash every element in  `nums` array. For every element `x` in `nums`, we tried to find `x+1`, `x-1` in the hashed table. This process continues until we cannot extend this interval anymore. During the process, if we find longest consecutive sequence, longer than anything before, we update the result to the found one.

The following python code is the implementation.

```python
def length(start, end):
    return end - start + 1

class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0
            
        hashmap = set()
        for x in nums:
            hashmap.add(x)

        result = nums[0], nums[0]
        for x in nums:
            # already consumed
            if x not in hashmap:
                continue

            hashmap.remove(x)
            start, end = x, x

            # extending in both way
            while start-1 in hashmap:
                start -= 1
                hashmap.remove(start)
            
            while end+1 in hashmap:
                end += 1
                hashmap.remove(end)

            if length(start, end) > length(*result):
                result = start, end
        
        return length(*result)
```
