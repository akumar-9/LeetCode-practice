# Unique Paths

## Problem Statement
There is a robot on an m x n grid. The robot is initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.

Given the two integers m and n, return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The test cases are generated so that the answer will be less than or equal to 2 * 109.

### Example
Input: m = 3, n = 7
Output: 28

## Approach
I use dynamic programming here. In the 2d dp array, an element `dp[i][j]` represents the number of uniques paths to reach the cell grid[i][j]. Since the only possible moves are right and down, you can reach dp[i][j], from dp[i][j-1] or dp[i-1][j]. So sum them. 
### Space Optimization
If I visualize it,dp[i-1][j] means we move to previous row, dp[i][j-1] means we move to the previous element in the current row. We only need two 1-d arrays at anytime. So use these 1d arrays instead of (m+1) x (n+1) matrix.
### Time Complexity
- **O(n*m)**:We traverse the dp array once. Even in the space optimized approach, we still have to go through n row and m columns.
### Space Complexity
- **O(n*m)**: We use a 2d dp array of size (m+1) x (n+1).
#### Space Optimized
- **O(m)**: We use two 1-d array of size m+1.

## Solution Code
### Approach
```C#
public class Solution {
    public int UniquePaths(int m, int n) {
        int[,] dp = new int[m+1,n+1];
        dp[1,1] = 1;
        for(int i = 1; i < m+1; i++){
            for(int j = 1; j< n+1;j++){
                if(i==1&& j==1)
                    continue;
                dp[i,j] = dp[i-1,j] + dp[i,j-1];
            }
        }
        return dp[m,n];
    }
}
```
### Space Optimized
```C#
public class Solution {
public class Solution {
    public int UniquePaths(int m, int n) {
        int[] currRow = new int[n+1];
        int[] prevRow = new int[n+1];
        for(int i = 1; i < m+1; i++){
            for(int j = 1; j< n+1;j++){
                if(i==1&& j==1)
                    currRow[j]=1;
                else
                    currRow[j] = prevRow[j] + currRow[j-1];
                int[] temp = prevRow;
                prevRow = currRow;
                currRow = prevRow;
            }
        }
        return prevRow[n];
    }
}
}

