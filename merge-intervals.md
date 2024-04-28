# merge-intervals
This is the step-by-step solution to solve the following problem on Leetcode.

* Merge Intervals - *Top Interview 150*
  * https://leetcode.com/problems/merge-intervals

To solve the problem, we need a two-pointer approach with custom sort.

First step is sorting the arrays with its starting position, `key(start, end) == start`. By using two-pointers method, first pointer indicates the merge-starting interval and second pointer indicates the absorbed-interval. Second pointer moves until it fails to merge its interval. After fail of the attempt, the big-merged interval is pushed into the result stack and first pointer moves to the position of the second pointer. This process repeats until the first pointer reaches the end of the array.

The following python code is the implementation.

```python
def sort_key(element):
    # start, end = element
    return element[0]

class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]: 
        # sort the intervals, with key of `start`
        sorted_segments = sorted(intervals, key=sort_key)
        
        pos, result = 0, []
        while pos < len(sorted_segments):
            start, end = sorted_segments[pos]
            merge_pos = pos + 1
            while merge_pos < len(sorted_segments):
                # attempt to merge_somehow(pos, merge_pos)
                merge_start, merge_end = sorted_segments[merge_pos]
                # my max reach is smaller than next stop
                if end < merge_start:
                    break
                end = max(merge_end, end)
                merge_pos += 1
            
            # push merged segment into result
            result.append([start, end])

            # next start point = failed-to-merge point
            pos = merge_pos

        return result
```
