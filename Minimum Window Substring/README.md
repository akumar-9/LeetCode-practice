# Minimum Window Substring

# Problem Statement
Given two strings `s` and `t` of lengths `m` and `n` respectively, return the minimum window 
substring of `s` such that every character in `t` (including duplicates) is included in the window. If there is no such substring, return the empty string `""`.
The testcases will be generated such that the answer is unique.

### Example
Input: s = "ADOBECODEBANC", t = "ABC" Output: "BANC"
## Approach
I maintain sliding window to track a valid substring of s that contains all characters of t. Start shrinking the valid substring until it is no more valid. Keep track of the length and also the start index for the substring. 
### Time Complexity
- **O(n + m)**:We traverse s once with the sliding window and update the frequency maps in constant time. n = length of s, m = length of t
### Space Complexity
- **O(m+n)**: We use frequency maps to track characters in t and the current window.


## Solution Code
```C#
public class Solution {
    public string MinWindow(string s, string t) {

        if (s.Length == 0 || t.Length == 0) 
            return "";

        int l = 0, formed = 0, start = 0, minLength = int.MaxValue;
        Dictionary<char, int> windowMap = new Dictionary<char, int>();
        Dictionary<char, int> tmap = new Dictionary<char, int>();

        foreach (char c in t) {
            tmap[c] = tmap.ContainsKey(c) ? ++tmap[c] : 1;
        }
        int required = tmap.Count;


        for(int r = 0; r < s.Length; r++){
            char c = s[r];
            windowMap[c] = windowMap.ContainsKey(c) ? ++windowMap[c] : 1;

            if(tmap.ContainsKey(c) && windowMap[c] == tmap[c]){
                formed++;
            }

            while(l <= r && formed == required){
                windowMap[s[l]]--;
                if(tmap.ContainsKey(s[l]) && windowMap[s[l]] < tmap[s[l]]){
                    formed--;
                }               
                if(r-l+1 < minLength){
                    minLength = r-l+1;
                    start = l;
                }
                l++;
            }

        }

        return minLength == int.MaxValue ? "" : s.Substring(start, minLength);
    }
}
