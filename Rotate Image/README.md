# Rotate Image

# Problem Statement
You are given an `n x n` 2D `matrix` representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

### Example
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]] Output: [[7,4,1],[8,5,2],[9,6,3]]

## Approach
Most easiest approch it to apply transpose and reverse the columns. Transpose will convert rows to columns and then reversing the columns can be done by reversing the elements of each rows.
### Time Complexity
- **O(n*m)**: We go through every element in matrix.
### Space Complexity
- **O(1)**: We use extra space for 2 variables.

## Solution Code
```C#
public class Solution {
    public void Rotate(int[][] matrix) {

        transpose(matrix);
        reverseRows(matrix);
        void transpose(int[][] matrix){
            int n = matrix.Length;
            for(int i =0; i< n;i++){
                for(int j =i+1; j< n;j++){            // do the swapping for elements above diagonal (j<i)
                    int temp = matrix[i][j];
                    matrix[i][j] = matrix[j][i];
                    matrix[j][i] = temp;
                }
            }
        }

        void reverseRows(int[][] matrix){
            for(int i =0; i < matrix.Length; i++)
                Array.Reverse(matrix[i]);
        }
    }
}