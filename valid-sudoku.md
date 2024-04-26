# valid-sudoku
This is the step-by-step solution to solve the following problem on Leetcode.

* Valid Sudoku - *Top Interview 150*
  * https://leetcode.com/problems/valid-sudoku

 To solve the problem, we need just a brute-force checking.

For each row, column, and block, we create a set. We attempt to verify if each number on the board is already taken by other numbers in the same set. 

The following python code is the implementation.

```python
def push(zero, value):
    if value in zero:
        raise Exception()
    zero.add(value)

class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        horz_zeros = [set() for _ in range(9)]
        vert_zeros = [set() for _ in range(9)]
        cell_zeros = [
            [set(), set(), set()],
            [set(), set(), set()],
            [set(), set(), set()]
        ]

        try:
            for w in range(9):
                for h in range(9):
                    value = board[w][h]
                    if value == ".":
                        continue
                    value = int(value) - 1
                    push(horz_zeros[h], value)
                    push(vert_zeros[w], value)
                    push(cell_zeros[w//3][h//3], value)
            
            return True
        except Exception as e:
            return False
        return True
```
