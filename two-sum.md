# two-sum
This is the step-by-step solution to solve the following problem on Leetcode.

* Two Sum - *Top Interview 150*
  * https://leetcode.com/problems/two-sum

To solve the problem, we need a hashing method here. By hashing using `value : index` pair, we can easily found the searching value's index. By utilizing this hashmap, for every element `x` we could find `target - x` in `O(1)` time. Total time complexity is `O(n)` while `n == len(nums)`.

The following python code is the implementation.

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # hashing <value : value's index>   
        get_index = dict()
        for i in range(len(nums)):
            # get_index always contains LAST FOUND INDEX
            get_index[nums[i]] = i
        
        # for every element `x`, check if `target-x` exists
        for i in range(len(nums)):
            goal = target - nums[i]
            if goal in get_index:
                j = get_index[goal]
                if i == j:
                    # duplicative element
                    # (ex) twoSum([2, 1, 3],4) -> [0,0] (wrong) [1,2] (correct)
                    continue
                return [i, j]
```
