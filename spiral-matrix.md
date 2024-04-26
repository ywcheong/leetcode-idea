# spiral-matrix
This is the step-by-step solution to solve the following problem on Leetcode.

* Spiral Matrix - *Top Interview 150*
  * https://leetcode.com/problems/spiral-matrix

 To solve the problem, we need just an implementation.

The following python code is the one.

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        # 0     ->      1
        # ^  move_type  v
        # 3     <-      2

        # 0 : on bottom, left to right
        # 1 : on right, bottom to top
        # 2 : on top, right to left
        # 3 : on left, top to bottom

        height, width = len(matrix), len(matrix[0])
        move_type = 0
        bottom, top = 0, height-1
        left, right = 0, width-1
        result = []

        while left <= right and bottom <= top:
            if move_type == 0:
                for i in range(left, right+1):
                    result.append(matrix[bottom][i])
                bottom += 1
            elif move_type == 1:
                for i in range(bottom, top+1):
                    result.append(matrix[i][right])
                right -= 1
            elif move_type == 2:
                for i in range(right, left-1, -1):
                    result.append(matrix[top][i])
                top -= 1
            else:
                for i in range(top, bottom-1, -1):
                    result.append(matrix[i][left])
                left += 1
            move_type = (move_type + 1) % 4

        return result
```
