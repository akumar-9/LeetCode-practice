# Set Matrix Zeroes

# Problem Statement
Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's.

You must do it in place.

### Example
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]] Output: [[1,0,1],[0,0,0],[1,0,1]]

## Approach
Most straight forward approach would be mark the rows and colums that needs to be set zeroes. Then traverse the matrix and update rows and columsn. We can use two arrays to keep track of the rows and columns to be zeroed. In a space optimized approach, we can use the 0th row and 0th column instead. The edge case will be to check if the 0th row and col need to be also zeroed. Check that using two bools.
### Time Complexity
- **O(n*m)**: We go through every element in matrix.
### Space Complexity
- **O(1)**: We use extra space for 2 variables.

## Solution Code
```C#
public class Solution {
    public void SetZeroes(int[][] matrix) {
        int n = matrix.Length;
        int m = matrix[0].Length;
        bool isFirstRowZero = false;
        bool isFirstColZero = false;

        for(int i = 0; i< m; i++){
            if(matrix[0][i] == 0){
                isFirstRowZero = true;          // check if the row needs to be set zero
                break;
            }
        }

        for(int j = 0; j<n; j++){
            if(matrix[j][0] == 0){
                isFirstColZero = true;      // check if the col needs to be set zero
                break;
            }
        }

        for(int i = 1; i<n; i++){
            for(int j = 1; j<m; j++){
                if(matrix[i][j] == 0){
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;       // marking the corresponding row and col to mark zero
                }
            }
        }

        for(int i = 1; i<n; i++){
            for(int j = 1; j<m; j++){
                if( matrix[0][j] == 0|| matrix[i][0] == 0){     // check if this row or col needs to be zeroed.
                    matrix[i][j] = 0;       
                }
            }
        }
        
        if(isFirstRowZero){
            for(int i = 0; i< m; i++){
                matrix[0][i] = 0 ;             // edge case where zero is present is 0th row
            }
        }

        if(isFirstColZero){
            for(int i = 0; i< n; i++){
                matrix[i][0] = 0;                //edge case
            }
        }
    }
}