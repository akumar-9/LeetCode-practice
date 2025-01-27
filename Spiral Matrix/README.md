# Spiral Matrix

# Problem Statement
Given an `m` x `n` matrix, return all elements of the matrix in spiral order.

### Example
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]] Output: [1,2,3,6,9,8,7,4,5]

## Approach
I traverse in spiral by limiting the movement i.e. setting up boundaries. Move from left to right across the top boundary. Then, top to bottom across right boundary, then right to left across bottom boundary and then bottom to top across left boundary. After each traversal, update the boundary.

### Time Complexity
- **O(n*m)**: We go through every element in matrix.
### Space Complexity
- **O(1)**: We use extra space only for output list.

## Solution Code
```C#
public class Solution {
    public IList<int> SpiralOrder(int[][] matrix) {
        int n = matrix.Length;
        int m = matrix[0].Length;
        List<int> result = new List<int>();
        int top = 0, bottom = n - 1, left = 0, right = m-1;

        while(top <= bottom && left <= right){

            for(int i = left; i <= right; i++){
                result.Add(matrix[top][i]);
            }
            top++;

            for(int i = top; i<= bottom; i++){
                result.Add(matrix[i][right]);
            }
            right--;

            if(top<= bottom){       // check if the boundaries are still valid, because you did top++
                for(int i = right; i >= left; i--){
                    result.Add(matrix[bottom][i]);
                }
                bottom--;
            }

            if(left<=right){    // check if the boundaries are still valid, because you did right--
                for(int i = bottom; i >= top; i--){
                    result.Add(matrix[i][left]);
                }
                left++;
            }

        }
        return result;
    }
}