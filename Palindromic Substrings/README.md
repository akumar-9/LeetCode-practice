# Palindromic Substrings

# Problem Statement
Given a string `s`, return the number of palindromic substrings in it.
### Example
Input: s = "abc" Output: 3
## Approach
I use dynamic programming here. An element dp[i,j] in the dp table tells if the substring s[i,j] is palindrome or not. Key idea is a substring s[i,j] is palindrome if s[i] == s[j] and the inner substring s[i+1,j-1] is also a valid substring.
### Time Complexity
- **O(n^2)**:where `n` is the length of the input string
### Space Complexity
- **O(n^2)**:DP Tale size is nxn. For space optimization I use only prev row.

## Solution Code
```C#
public class Solution {
    public int CountSubstrings(string s) {
        int n = s.Length;
        bool[,] dp = new bool[n,n];
        int count = 0;

        for(int length = 1; length <= n; length++){
            for(int i = 0; i + length <= n; i++){
                int j = i + length - 1;
                if(s[i]==s[j] && (length<= 2|| dp[i+1,j-1])){
                    dp[i,j] = true;
                    count++;
                }
            }
        }
        return count;
    }
}