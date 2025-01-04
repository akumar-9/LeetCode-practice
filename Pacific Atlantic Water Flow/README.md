# Pacific Atlantic Water Flow


## Problem Statement
There is an `m x n` rectangular island that borders both the Pacific Ocean and Atlantic Ocean. The Pacific Ocean touches the island's left and top edges, and the Atlantic Ocean touches the island's right and bottom edges.

The island is partitioned into a grid of square cells. You are given an `m x n` integer matrix `heights` where `heights[r][c]` represents the height above sea level of the cell at coordinate `(r, c)`.

The island receives a lot of rain, and the rain water can flow to neighboring cells directly north, south, east, and west if the neighboring cell's height is less than or equal to the current cell's height. Water can flow from any cell adjacent to an ocean into the ocean.

Return a 2D list of grid coordinates result where `result[i] = [ri, ci]` denotes that rain water can flow from cell `(ri, ci)` to both the Pacific and Atlantic oceans.



### Example
Input: heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]

## Approach
I use DFS here. I maintain a two visited matrices that keeps track of the cells that can reach pacific and atlantic. If a cell can reach both pacific and atlantic then add to the results list. In DFS, calculate all possible directions up, down, left, right and check if the water can flow uphill (yeah! you are doing the reverse), if yes then repeat this for its neighbors.

### Time Complexity
- **O(m x n)**: Each cell is visited once.
### Space Complexity
- **O(m x nx)**: Recursion stack size for DFS.

## Solution Code
```C#
public class Solution {
    public IList<IList<int>> PacificAtlantic(int[][] heights) {
        int m = heights.Length;
        int n = heights[0].Length;

        bool[,] pReachable = new bool[m,n]; // pacific reachable 
        bool[,] aReachable = new bool[m,n]; // atlantic reachable

        int[][] directions = new int[][] {new int []{-1,0}, new int []{1,0}, new int []{0,-1}, new int []{0,1}};    // top, down, left, right

        List<IList<int>> results = new List<IList<int>>();

        void dfs(int row, int col, bool[,] reachable){
            reachable[row, col] = true;
            foreach(var dir in directions){
                int newRow = row + dir[0];
                int newCol = col + dir[1];

                if(newRow >= 0 && newRow < m && 
                   newCol >= 0 && newCol < n &&
                   !reachable[newRow, newCol] &&    // check if not visited already else get stuck in recursion
                   heights[newRow][newCol] >= heights[row][col]){
                    dfs(newRow, newCol, reachable);
                   }
            }
        }

        for(int i = 0; i<m; i++) dfs(i, 0, pReachable); // left and top edges are pacific reachable
        for(int i = 0; i<n; i++) dfs(0, i, pReachable);

        for(int i =0; i<m; i++) dfs(i, n-1, aReachable); // right and botton edges are pacific reachable
        for(int i =0; i<n; i++) dfs(m-1, i, aReachable);

        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(pReachable[i,j] && aReachable[i,j])  // if both are reachable then add to results
                    results.Add(new List<int> {i,j});
            }
        }
        return results;
    }
}