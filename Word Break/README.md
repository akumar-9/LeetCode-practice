# Word Break

## Problem Statement
Given a string `s` and a dictionary of strings `wordDict`, return true if `s` can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.
### Example
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true

## Approach
I used Dynamic Programming here. In the boolean dp array, the element dp[i] tells whether the substring S[0..to..i] can be segmented(word break sub problem). For each index i, we will check all possible substring S[j..i-1] where j ranges from 0 to i-1. If dp[j] is true (means substring s[0..j] can be segmented) and the remaining substring s[j..i-1] exsists in dictionary, means that the whole string can be segmented. Just think of it as breaking a string into 2 sub problems, left half should be word-breakable and the right half should be a valid word in dictionary, then the larger problem is word-breakable.

### Time Complexity
- **O(n^2)**: Outer loop runs for n times, inner loop runs for n times.
### Space Complexity
- **O(n)**: We use dp array of size n+1 extra space.

## Solution Code
```C#
public class Solution {
    public bool WordBreak(string s, IList<string> wordDict) {
        int n = s.Length;
        bool[] dp = new bool[n + 1];
        dp[0] = true; //empty string is alway segmentable
        for(int i = 1; i<n+1; i++){
            for(int j = 0; j<i;j++){
                if(dp[j] && wordDict.Contains(s.Substring(j,i-j)) ){
                    dp[i] = true;
                    break; // break if we already know s[0..i-1]can be segmented i.e. dp[i]==true, there's no point continuing loop
                }
            }
        }
        return dp[n];
    }
}