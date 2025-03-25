# Valid Sudoku

# Problem Statement
Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits 1-9 without repetition.
2. Each column must contain the digits 1-9 without repetition.
3. Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.


### Example
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true

## Approach 1
Most straightforward approach is doing all the checks i.e no duplicate in rows, cols or 3x3 grid. I can do this using a single HashSet and clear it after checking each row, col and grid. 
## Approach 2
I can optimize the approach by going through the entire board once, at each element, store its representation in hashset,something like row0-2, col0-2, grid0-2 which means that number 2 is present in row0, col0 or grid0 respectively. If I come across a representations that is already in the hashset, then I can just say invalid sudoku board.    
## Approach 3
The most optimized approach I can come with is an extension of previous approach, that is in one pass, I want to store the representation of each element in arrays. I can use bits for this representation. I use 3 arrays of length 9 namely, row, col and grid. Each element of these array will tell me if a number 1-9 is present in it or not. Like if row[0] has a value say 0000 0001 0001, this would mean that number 1 and 5 are present in row0. How do I check if an element is already present ? I will first represent the number in bits like if the number on board is 9, my bit representation would be setting the bit at 9th position, so 0001 0000 0000. Now I will AND it with the bits in row[0], for check if 9 is present in row0.  If the AND results in 0, then it means that 9 was not present. But if the result is not zero, then it means that the 9th bit was already set in row[0] and that this is a duplicate.
### Time Complexity
- **O(1)**: Approach 1 takes 3 passess on the board. Approach 2 takes 1 pass. Approach 3 takes 1 pass.
### Space Complexity
- **O(1)**: Approach 1 reuses that Hashset and atmost contains 81 elements. Approach 2 uses hashest that atmost contains 3*81 representation. Approach uses only 27 integers(9 rows, 9 cols, and 9 grids)

## Solution Code
```C#
// Approach 1
public class Solution {
    public bool IsValidSudoku(char[][] board) {
        // each row must not contain duplicate or 
        HashSet<char> seen = new HashSet<char>();
        for(int i = 0; i < 9; i++){
            for(int j = 0; j < 9; j++){
                if(seen.Contains(board[i][j]))  
                    return false;
                if(board[i][j] != '.')  
                    seen.Add(board[i][j]);
            }
            seen.Clear();
        }

        // each column must not contain duplicate
        for(int i = 0; i < 9; i++){
            for(int j = 0; j < 9; j++){
                if(seen.Contains(board[j][i]))  
                    return false;
                if(board[j][i] != '.')
                    seen.Add(board[j][i]);
            }
            seen.Clear();
        }

        // sub grids must not contain duplicates
        for(int k = 0; k < 9; k = k + 3){
            for(int l = 0; l < 9; l = l +3){
                for(int i = k; i < k+3; i++){
                    for(int j = l; j < l+3; j++){
                        if(seen.Contains(board[i][j]))  
                            return false;
                        if(board[i][j] != '.')
                            seen.Add(board[i][j]);
                    }
                }
                seen.Clear();

            }
        }
        return true;            
    }
}


// Approach 2
public class Solution {
    public bool IsValidSudoku(char[][] board) {
        HashSet<string> seen = new HashSet<string>();
        for(int row = 0; row < 9; row++){
            for(int col = 0; col < 9; col++){
                
                char curr = board[row][col];
                if(curr == '.')  continue;
                string rowKey = $"row{row}-{curr}";
                string colKey = $"col{col}-{curr}";
                string gridKey = $"grid{3*(row/3) + col/3}-{curr}";  //grid0, grid1 .. 

                if(seen.Contains(rowKey) || seen.Contains(colKey) || seen.Contains(gridKey)){
                    return false;
                }
                seen.Add(rowKey);
                seen.Add(colKey);
                seen.Add(gridKey);
            }
        }
        return true;
    }
}


// Approach 3
public class Solution {
    public bool IsValidSudoku(char[][] board) {
        int[] rows = new int[9];
        int[] cols = new int[9];
        int[] grid = new int[9];

        for(int i = 0; i< 9; i++){
            for(int j = 0; j< 9 ; j++){
                char curr = board[i][j];
                if(curr == '.') continue;
                int num = curr - '1';
                int mask = 1 << num;

                if( (rows[i] & mask) != 0 ||
                    (cols[j] & mask )!= 0 ||
                    (grid[3*(i/3) + j/3] & mask) != 0 ){
                    return false;
                }

                rows[i] |= mask;
                cols[j] |= mask;
                grid[3*(i/3) + j/3] |= mask;
            }
        }
        return true;
    }
}