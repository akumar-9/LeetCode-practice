# Longest Palindromic Substring

# Problem Statement
Given a string `s`, return the longest palindromic substring in s.
### Example
Input: s = "babad" Output: "bab"
## Approach
I use dynamic programming here. An element dp[i,j] in the dp table tells if the substring s[i,j] is palindrome or not. Key idea is a substring s[i,j] is palindrome if s[i] == s[j] and the inner substring s[i+1,j-1] is also a valid substring.
### Time Complexity
- **O(n^2)**:where `n` is the length of the input string
### Space Complexity
- **O(n^2)**:DP Tale size is nxn. For space optimization I use only prev row.

## Solution Code
```C#
public class Solution {
    public string LongestPalindrome(string s) {
        int n = s.Length;
        int len = 0, start = 0, end = 0;
        bool[,] dp = new bool[n,n];
        
        for(int i =0; i < n; i++){  //for palindrome of length 1
            dp[i,i] = true;
            start = i;
            len=1;
        }
        
        for(int i = 0; i+1 < n; i++){//for palindrome of length 2
            if(s[i] == s[i+1]){
                dp[i,i+1] = true;
                len = 2;
                start = i;
            }
        }
        
        for(int k = 2; k < n; k++){//for palindrome of length 3 and above
            for(int i=0; i +k < n ; i++){
                int j=i+k;
                if(s[i] == s[j] && dp[i+1,j-1]){
                    dp[i,j] = true;
                    if(j-i+1 > len){
                        len = j-i+1;
                        start = i;
                    }
                }
                
            }
        }
        return s.Substring(start,len); 
    }
}