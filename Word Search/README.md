# Word Search

# Problem Statement
Given an `m x n` grid of characters `board` and a string `word`, return `true` if `word` exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

### Example
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED" Output: true
## Approach
Begin by finding the first character that matches, from there start DFS. If a cell matches with current character, mark it visited so as to avoid duplicates , explore all 4 directions. If you reach the length of the string then return true. Don't forget to restore the visited cell if the current path is not viable. 
### Time Complexity
- **O(n* m * 4^L)**: m x n board traversal. 4^L for exploring up to L levels deep (length of the word). Worst case: Checking all possibilities.
### Space Complexity
- **O(L)**: Recursive call stack takes O(L) (length of word).

## Solution Code
```C#
public class Solution {
    public bool Exist(char[][] board, string word) {
        int m = board.Length;
        int n = board[0].Length;

        for(int i = 0; i < m; i++){
            for(int j = 0; j<n; j++){
                if(board[i][j] == word[0] && dfs(0, i, j)){
                    return true;
                }
            }
        }

        bool dfs(int index, int row, int col){
            if(index == word.Length)
                return true;

            if(row >= m || row < 0 || col >= n || col < 0 || board[row][col] != word[index] )
                return false;

            char temp = board[row][col];
            board[row][col] = '#';          // so that we don't revisit this character 

            bool found = dfs(index+1, row, col + 1) || 
                   dfs(index+1, row, col -1)  ||
                   dfs(index+1, row + 1, col) ||
                   dfs(index+1, row - 1, col);
            
            board[row][col]= temp;      // restore the cell because we are moving to a different path
            return found;
        }

        return false;   
    }
}