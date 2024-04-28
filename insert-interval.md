# insert-interval
This is the step-by-step solution to solve the following problem on Leetcode.

* Insert Interval - *Top Interview 150*
  * https://leetcode.com/problems/insert-interval

To solve the problem, we need some simple mathematics with array handling. To determine if two intervals $(a1, b1), (a2, b2)$ are overlapping, we can use the expression follow.

```
(a1, b1) ~ (a2, b2) overlaps if and only if
(b2 - s1) * (s2 - e1) <= 0
```

To proof the statement above, we need a case-by-case approach so skip it in here. To merge the array which overlaps, we can use `merge_interval` function at the top of the implementation. Check the following python code to see the function.

```python
from typing import List

def is_overlap(interval1, interval2):
    start1, end1 = interval1
    start2, end2 = interval2
    return (end2 - start1) * (start2 - end1) <= 0

def merge_interval(interval1, interval2):
    start1, end1 = interval1
    start2, end2 = interval2
    return [min(start1, start2), max(end1, end2)]

class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        pos, result = 0, []
        overlapped = False
        while pos < len(intervals):
            if is_overlap(intervals[pos], newInterval):
                # overlapping occured -> merge until stop overlapping
                overlapped = True
                while pos < len(intervals) and is_overlap(intervals[pos], newInterval):
                    newInterval = merge_interval(intervals[pos], newInterval)
                    pos += 1
                result.append(newInterval)
            else:
                result.append(intervals[pos])
                pos += 1

        if overlapped:
            return result
        
        # never overlapped -> need to add while keeping its order
        result = []
        pushed = False
        for i in range(len(intervals)):
            oldInterval = intervals[i]
            if not pushed and newInterval[0] < oldInterval[0]:
                pushed = True
                result.append(newInterval)
            result.append(oldInterval)
        if not pushed:
            result.append(newInterval)

        return result
```
