# Word Search II

# Problem Statement
Given an` m x n `board of characters and a list of strings `words`, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

### Example
Input: board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]

## Approach
I use a trie here. First insert all the words in the word list to the trie. Then I check traverse the board to find if a character is the starting point of any of the words in word list. I can do this by doing a check of board[i][j] with children of trie's root. If a match is found, I explore all direction and check if it is the endOfWord. If true add to the result list. Also, to avoid revisiting mark the visited char on board with a `#` symbol.   
### Time Complexity
- **O(w * l + m * n * 4^L)**: O(W * L) (W = words, L = word length) for insertion, O(M * N * 4^L) for backtracking search.
### Space Complexity
- **O(W * L)**: Trie insertion is O(W * L) and O(L) for backtracking recursive stack.

## Solution Code
```C#
public class Solution {
    List<string> result = new List<string>();


    public TrieNode root = new TrieNode();
    
    public class TrieNode{
        public Dictionary<char, TrieNode> children;
        public string endWord;

        public TrieNode(){
            children = new Dictionary<char, TrieNode>();
        }
    }

    public void Insert(string word){
        TrieNode cur = root;
        foreach(char c in word){
            if(!cur.children.ContainsKey(c)){
                cur.children[c] = new TrieNode();
            }
            cur = cur.children[c];
        }
        cur.endWord = word;
    }

    public IList<string> FindWords(char[][] board, string[] words) {
        int n = board.Length;
        int m = board[0].Length;

        foreach(string word in words){
            Insert(word);
        }

        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(root.children.ContainsKey(board[i][j])){
                    Backtrack(i,j,root,board);
                }
            }
        }
        return result;

        void Backtrack(int row, int col, TrieNode root, char[][] board){
            char temp = board[row][col];
            TrieNode curNode = root.children[temp];

            if(curNode!= null && curNode.endWord!= null){
                result.Add(curNode.endWord);
                curNode.endWord = null;
            }

            board[row][col] = '#';

            int[][] directions = new int[][]{new int[]{0,1}, new int[]{0,-1}, new int[]{1,0}, new int[]{-1,0}};

            foreach(var dir in directions){
                int newRow = row + dir[0];
                int newCol = col + dir[1];

                if(newRow >= 0 && newRow < board.Length && newCol >= 0 && newCol < board[0].Length){
                    if(curNode.children.ContainsKey(board[newRow][newCol])){
                        Backtrack(newRow, newCol, curNode, board);
                    }
                }
            }

            board[row][col] = temp;
        }
    }
}