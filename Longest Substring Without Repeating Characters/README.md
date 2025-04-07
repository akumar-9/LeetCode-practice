# Longest Substring Without Repeating Characters

# Problem Statement
Given a string` s`, find the length of the longest substring without repeating characters.

### Example
Input: s = "abcabcbb" Output: 3

## Approach 1
I use two pointer technique here. Expand the window(r++) until a duplicate character is found, shrink the window(l++) until there are no duplicates. Keep track of maximum window size.
## Approach 2
I use the same two pointer technique, but rather than shrinking the window one at a time, I will move the 'l' pointer to where the duplicate character occurs.
### Time Complexity
### Approach 1
- **O(n)**:We traverse the string once with a sliding window.
### Approach 2
- **O(n)**:We traverse the string once with a sliding window.
### Space Complexity
### Approach 1
- **O(min(n,m))**: The size of the set depends on the number of unique characters (or the length of the string).
### Approach 2
- **O(min(n,m))**: The size of the set depends on the number of unique characters (or the length of the string).

## Solution Code
```C#
//Approach 1
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

// Approach 2

public class Solution {
    public int LengthOfLongestSubstring(string s) {
        int l = 0;
        int r = 0;
        int maxLength = 0;
        Dictionary<char, int> charMap = new Dictionary<char, int>();
        while(r < s.Length){
            if(charMap.ContainsKey(s[r]) && charMap[s[r]] >= l){    // the make sure you don't expand the window to the left side
                l = charMap[s[r]] + 1;
            }
            charMap[s[r]] = r;
            maxLength = Math.Max(r-l+1, maxLength);
            r++;
        }
        return maxLength;
    }
}