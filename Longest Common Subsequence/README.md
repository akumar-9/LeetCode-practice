# Longest Common Subsequence

## Problem Statement
Given two strings text1 and text2, return the length of their longest common subsequence. If there is no common subsequence, return 0.

A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

For example, "ace" is a subsequence of "abcde".
A common subsequence of two strings is a subsequence that is common to both strings.

### Example
Input: text1 = "abcde", text2 = "ace" 
Output: 3  

## Approach
I use dynamic programming here. In the 2d dp array, an element `dp[i][j]` represents the length of LCS first `i` characters of `text1` and first `j` characters of `text2`. At each step, we compare characters `text1[i]` and `text2[j]`. If the characters match, then the LCS of first `i` characters of `text1` and first `j` characters of `text2` will be 1 more than the LCS of first `i-1` characters of `text1` and first `j-1` characters of `text2`. If the characters don't match, then simply choose maximum LCS length excluding the current character from either strings. 
### Space Optimization
If I visualize it, dp[i-1][j-1] means we move diagonally to top left, dp[i-1][j] means we move to previous row, d[i][j-1] means we move to the previous element in the current row. If you notice we only need two 1-d arrays at anytime. So use these instead of (m+1) x (n+1) matrix.
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
    public int LongestCommonSubsequence(string text1, string text2) {
        int n = text1.Length;
        int m = text2.Length;
        int[,] dp = new int[n+1,m+1];
        for(int i = 1; i < n+1; i++){
            for(int j = 1; j < m+1; j++){
                if(text1[i-1] == text2[j-1] ){
                    dp[i,j] = dp[i-1,j-1] + 1;
                }
                else{
                    dp[i,j] = Math.Max(dp[i-1,j], dp[i,j-1]);
                }
            }
        }
        return dp[n,m];
    }
}
```
### Space Optimized
```C#
public class Solution {
    public int LongestCommonSubsequence(string text1, string text2) {
        int n = text1.Length;
        int m = text2.Length;
        int[] currRow = new int[m+1];
        int[] prevRow = new int[m+1];
        for(int i = 1; i < n+1; i++){
            for(int j = 1; j < m+1; j++){
                if(text1[i-1] == text2[j-1] ){
                    currRow[j] = prevRow[j-1] + 1;
                }
                else{
                    currRow[j] = Math.Max(prevRow[j], currRow[j-1]);
                }
            }
            var temp = prevRow;  //swap the prev and curr
            prevRow = currRow;
            currRow = temp;
        }
        return prevRow[m];
    }
}

