# game-of-life
This is the step-by-step solution to solve the following problem on Leetcode.

* Game of Life - *Top Interview 150*
  * https://leetcode.com/problems/game-of-life

To solve the problem, we need to implement a traditional state-updating simulation.

The following python code is the implementation.

```python
DX_DY = (
    (-1, -1),
    (-1, 0),
    (-1, 1),
    (0, -1),
    (0, 1),
    (1, -1),
    (1, 0),
    (1, 1)
)

def next_state(is_lived, adj_count):
    if is_lived == 0 and adj_count == 3:
        return 1
    elif is_lived == 1 and 2 <= adj_count <= 3:
        return 1
    return 0

def is_valid_pos(size, pos):
    x_lim, y_lim = size
    x, y = pos
    return 0 <= x < x_lim and 0 <= y < y_lim

class Solution:
    def gameOfLife(self, board: List[List[int]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        
        x_lim, y_lim = len(board), len(board[0])
        board_copy = [[board[x][y] for y in range(y_lim)] for x in range(x_lim)]

        for x in range(x_lim):
            for y in range(y_lim):
                board[x][y] = 0
                for dx, dy in DX_DY:
                    if is_valid_pos((x_lim, y_lim), (x+dx, y+dy)):
                        board[x][y] += board_copy[x+dx][y+dy]

        for x in range(x_lim):
            for y in range(y_lim):
                board[x][y] = next_state(board_copy[x][y], board[x][y])
```
