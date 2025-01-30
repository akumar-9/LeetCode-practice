# Longest Substring Without Repeating Characters

# Problem Statement
Given a string` s`, find the length of the longest substring without repeating characters.

### Example
Input: s = "abcabcbb" Output: 3

## Approach
I use two pointer technique here. Expand the window(r++) until a duplicate character is found, shrink the window(l++) until there are no duplicates. Keep track of maximum window size.
### Time Complexity
- **O(n)**:We traverse the string once with a sliding window.
### Space Complexity
- **O(min(n,m))**: The size of the set depends on the number of unique characters (or the length of the string).

## Solution Code
```C#
public class Solution {
    public int LengthOfLongestSubstring(string s) {
        int n = s.Length;

        if(n == 0)  return 0;

        int l = 0;
        int maxLength = int.MinValue;
        HashSet<char> chars = new HashSet<char>();
        
        for(int r = 0; r < n; r++){
            while(chars.Contains(s[r])){
                chars.Remove(s[l]);
                l++;
            }
            chars.Add(s[r]);
            maxLength = Math.Max(maxLength, r-l+1);
        }
        return maxLength;
    }
}