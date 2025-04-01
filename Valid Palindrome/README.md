# Valid Palindrome

# Problem Statement
A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.
### Example
Input: s = "A man, a plan, a canal: Panama" Output: true
## Approach
I use 2 pointer technique here. Traverse the string and skip over non-alpha numeric characters. Compare the first character with the last one, if they do not match then return, do this until left pointer cross overs right pointer. 
### Time Complexity
- **O(n)**:where `n` is the length of the input string
### Space Complexity
- **O(1)**:We use only few extra variables.

## Solution Code
```C#
public class Solution {
    public bool IsPalindrome(string s) {
        int l = 0;
        int r = s.Length-1;
        while( l < r){
            if(!Char.IsLetterOrDigit(s, l)){        // take a look at this static method, it takes string and an index
                l++;
                continue; // can't I just use while instead of if statement? yes you can!  while (l < r && !Char.IsLetterOrDigit(s[l])) l++;
            }
            if(!Char.IsLetterOrDigit(s,r)){ // while (l < r && !Char.IsLetterOrDigit(s[l])) {
                r--;                       //       l++;            
                continue;                 //   }
            }
            if( Char.ToLower(s[l]) != Char.ToLower(s[r])){
                return false;
            }
            l++;
            r--;
        }
        return true;
    }
}