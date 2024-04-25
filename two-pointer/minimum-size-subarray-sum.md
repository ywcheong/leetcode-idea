# minimum-size-subarray-sum
To solve the problem, we need a two-pointer method with a greedy algorithm. Starting from the suboptimal solution, `nums[0:x]`, we can think simple if-else algorithm:

* We have a solution `nums[start:end]`...
* Check if it is the new shortest subarray...
* DECIDE if we can drop out the `start`, and it still makes the solution.
  * **YES** : drop out the `start -> start+1`
  * **NO** : extend the `end -> end+1`
* Repeat until we can neither drop nor extend...

The following python code is the implementation.

```python
def get_length(start_pos, end_pos):
    return end_pos - start_pos + 1

class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        start_pos, end_pos, total_sum = 0, 0, nums[0]
        min_length = 987654321 # == inf

        # find one easy but wrong solution
        while end_pos != len(nums)-1 and total_sum < target:
            end_pos += 1
            total_sum += nums[end_pos]

        if total_sum < target:
                return 0

        while True:
            # choose one of the following action:
            # action 1. increasing start_pos (if possible)
            # action 2. increasing end_pos (if failed, terminate loop)

            min_length = min(min_length,get_length(start_pos, end_pos))

            if target <= total_sum - nums[start_pos]:
                total_sum -= nums[start_pos]
                start_pos += 1
                continue
            
            if end_pos < len(nums) - 1:
                end_pos += 1
                total_sum += nums[end_pos]
                continue
            else:
                return min_length
```
