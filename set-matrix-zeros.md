# set-matrix-zeros
This is the step-by-step solution to solve the following problem on Leetcode.

* Set Matrix Zeros - *Top Interview 150*
  * https://leetcode.com/problems/set-matrix-zeroes

To solve the problem, we need just an implementation which handles 2d-array. The following python code is the implementation.

```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        x_lim, y_lim = len(matrix), len(matrix[0])
        multiply_x = [1] * x_lim
        multiply_y = [1] * y_lim

        for x in range(x_lim):
            for y in range(y_lim):
                if matrix[x][y] == 0:
                    multiply_x[x], multiply_y[y] = 0, 0
            
        for x in range(x_lim):
            for y in range(y_lim):
                matrix[x][y] *= multiply_x[x] * multiply_y[y]
```
