# Number of Islands

## Problem Statement
Given an `m x n` 2D binary grid grid which represents a map of `'1'`s (land) and `'0'`s (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

### Example
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1


## Approach
Key idea is to travel all the lands, check if the current land connected or is a part of island by exploring neighbors. Mark them as visited or water. Continue this process for all elements in the grid.

### Time Complexity
- **O(m x n)**: Each cell is visited once.
### Space Complexity
- **O(m x nx)**: Recursion stack size for DFS.

## Solution Code
```C#
public class Solution {
    public int NumIslands(char[][] grid) {
        int m = grid.Length;
        int n = grid[0].Length;
        int numsIsland = 0;
        int[][] directions = new int[][]{new int[]{0, 1}, new int[]{0, -1}, new int[]{1, 0}, new int[]{-1, 0}};
        for(int i =0 ;i < m; i++){
            for(int j = 0; j< n; j++){
                if(grid[i][j] == '1'){
                    numsIsland++;
                    DFS(i,j);
                }
            }
        }

        void DFS(int row, int col){
            if(row >= m || row < 0 || col >= n || col < 0 || grid[row][col] == '0'){
                return;
            }
            grid[row][col] = '0';
            foreach(var dir in directions){
                int newRow = row + dir[0];
                int newCol = col + dir[1];
                DFS(newRow, newCol);
            }
        }

        return numsIsland;
    }
}