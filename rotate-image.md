# rotate-image
This is the step-by-step solution to solve the following problem on Leetcode.

* Rotate Image - *Top Interview 150*
  * https://leetcode.com/problems/rotate-image

 To solve the problem, we need just an implementation.

The following python code is the one.

```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        
        # [i, j] -> i from bottom, j from left
        # [??, ??] = i from _right_, j from _bottom_
        # L[j, n-1-i] = L[i, j]
        # L[n-1-i, n-1-j] = L[j, n-1-i]
        # L[n-1-j, i] = L[n-1-i, n-1-j]
        # L[i, j] = L[n-1-j, i]

        n = len(matrix)

        if n % 2 == 0:
            wsize, hsize = n//2, n//2
        else:
            wsize, hsize = n//2, n//2+1
        
        for i in range(wsize):
            for j in range(hsize):
                matrix[j][n-1-i], matrix[n-1-i][n-1-j], \
                matrix[n-1-j][i], matrix[i][j] = \
                    matrix[i][j], matrix[j][n-1-i], \
                    matrix[n-1-i][n-1-j], matrix[n-1-j][i]
                
```
