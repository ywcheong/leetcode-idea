# remove-duplicates-from-sorted-array
This is the step-by-step solution to solve the following problem in Leetcode.

* Remove Duplicates from Sorted Array - *Top interview 150*
  * https://leetcode.com/problems/remove-duplicates-from-sorted-array/

 To solve the problem, we need a two-pointer method. Since the given array is monotonically increasing array, we would not meet any identical element in any two non-adjacent position.
 
 By acquiring an idea from this preperty, we can think that we could scan the whole array, using `read_pos`, and ignoring all the duplicative elements until:
 * Reaching the end of the array : `next_read_pos < len(nums)`
 * Reaching non-duplicative elements : `nums[read_pos] == nums[next_read_pos]`

 After that, we can write this scanned element to the writing pointer, `write_pos`.

The following python code is the implementation.

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        # using a two-pointer method
        read_pos, write_pos = 0, 0

        while read_pos < len(nums):
            next_read_pos = read_pos

            # increase the reading position
            # until meet inequivalent element
            while next_read_pos < len(nums) and nums[read_pos] == nums[next_read_pos]:
                next_read_pos += 1
            
            # override the original array
            nums[write_pos] = nums[read_pos]
            
            # move the pointer
            write_pos += 1
            read_pos = next_read_pos
        
        # increment of the writing position is equal to k
        return write_pos
```
