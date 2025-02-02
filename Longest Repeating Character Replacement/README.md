# Longest Repeating Character Replacement

# Problem Statement
You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.
### Example
Input: s = "ABAB", k = 2 Output: 4

## Approach
I use two pointer technique here. Track the most frequent character within the window. If the no. of characters that need to be replaced exceeds `k`, shrink the window from the left. Keep track of maximum window size.
### Time Complexity
- **O(n)**:We traverse the string once with a sliding window.
### Space Complexity
- **O(1)**: We store character frequencies for up to 26 characters (constant space).

## Solution Code
```C#
public class Solution {
    public int CharacterReplacement(string s, int k) {
        int n = s.Length;
        int l = 0, maxLength = int.MinValue, maxFreq = int.MinValue;
        Dictionary<char, int> freq = new Dictionary<char, int>();

        for(int r = 0; r < n; r++){
            freq[s[r]] = freq.ContainsKey(s[r]) ? ++freq[s[r]] : 1;

            maxFreq = Math.Max(maxFreq, freq[s[r]]);        // Keep track of highest Frequency ever

            while( r-l+1 - maxFreq > k){                    // once the window is valid, shrink it
                freq[s[l]]--;
                l++;
            }

            maxLength = Math.Max(maxLength, r-l+1);         // track the max length of valid window
        }

        return maxLength;
    }
}