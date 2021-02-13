# 1091. Shortest Path in Binary Matrix

In an N by N square grid, each cell is either empty (0) or blocked (1).

A *clear path from top-left to bottom-right* has length `k` if and only if it is composed of cells `C_1, C_2, ..., C_k` such that:

- Adjacent cells `C_i` and `C_{i+1}` are connected 8-directionally (ie., they are different and share an edge or corner)
- `C_1` is at location `(0, 0)` (ie. has value `grid[0][0]`)
- `C_k` is at location `(N-1, N-1)` (ie. has value `grid[N-1][N-1]`)
- If `C_i` is located at `(r, c)`, then `grid[r][c]` is empty (ie. `grid[r][c] == 0`).

Return the length of the shortest such clear path from top-left to bottom-right.  If such a path does not exist, return -1.

**Example 1:**

```
Input: [[0,1],[1,0]]
Output: 2

```

![https://assets.leetcode.com/uploads/2019/08/04/example1_1.png](https://assets.leetcode.com/uploads/2019/08/04/example1_1.png)

![https://assets.leetcode.com/uploads/2019/08/04/example1_2.png](https://assets.leetcode.com/uploads/2019/08/04/example1_2.png)

**Example 2:**

```
Input: [[0,0,0],[1,1,0],[1,1,0]]
Output: 4

```

![https://assets.leetcode.com/uploads/2019/08/04/example2_1.png](https://assets.leetcode.com/uploads/2019/08/04/example2_1.png)

![https://assets.leetcode.com/uploads/2019/08/04/example2_2.png](https://assets.leetcode.com/uploads/2019/08/04/example2_2.png)

**Note:**

1. `1 <= grid.length == grid[0].length <= 100`
2. `grid[r][c]` is `0` or `1`

python solution:

```python
class Solution:
    def shortestPathBinaryMatrix(self, grid: List[List[int]]) -> int:
        N = len(grid)
        q = [(0, 0)]
        if grid[0][0] or grid[N-1][N-1]:
            return -1
        step = 0
        visited = set()
        while q:
            level_q = set(q[:])
            q = []
            step += 1
            for node in level_q:
                visited.add(node)
                i, j = node
                if node == (N-1, N-1):
                    return step
                for r, c in [(i-1, j-1), (i-1, j), (i-1, j+1), \
                             (i, j-1), (i, j+1), \
                             (i+1, j-1), (i+1, j), (i+1, j+1)]:
                    if 0 <= r < N and 0 <= c < N and not grid[r][c] and\
                       (r, c) not in visited and (r, c) not in level_q:
                        q.append((r, c))
        return -1
```

T.C. O(node numbers) S.C. O(N)  N as len(grid)