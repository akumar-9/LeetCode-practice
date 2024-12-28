# Decode ways

## Problem Statement
You have intercepted a secret message encoded as a string of numbers. The message is decoded via the following mapping:

"1" -> 'A'  "2" -> 'B'  "25" -> 'Y'  "26" -> 'Z'
However, while decoding the message, you realize that there are many different ways you can decode the message because some codes are contained in other codes ("2" and "5" vs "25").

For example, "11106" can be decoded into:

"AAJF" with the grouping (1, 1, 10, 6)
"KJF" with the grouping (11, 10, 6)
The grouping (1, 11, 06) is invalid because "06" is not a valid code (only "6" is valid).
Note: there may be strings that are impossible to decode.

Given a string s containing only digits, return the number of ways to decode it. If the entire string cannot be decoded in any valid way, return 0. The test cases are generated so that the answer fits in a 32-bit integer.

### Example
Input: s = "12"
Output: 2

## Approach
I use dynamic programming here. In the dp array, dp[i] denotes the number of ways to decode the substring s[0..i]. The number of ways of decoding s[0..i] depends on the number of ways of decoding s[0..i-1] and s[0..i-2]. At each step, check if the current character is valid or not(i.e. check if != 0). Also check if the current character and previous character make a valid 2-digit(i.e. in range [10,26]). If yes then add the number of ways to decode both single digit and double digit.
### Space Optimization
If I visualize it, I only need need to keep track of number of ways of decoding i.e dp[i-1] and dp[i-2]. So use two variables instead of an array.
### Time Complexity
- **O(n)**:We traverse the dp array once. Even in the space optimized approach, we still have to go through n elements.
### Space Complexity
- **O(n)**: We use a dp array of size n+1.
#### Space Optimized
- **O(1)**: We use extra variables.

## Solution Code
### Approach
```C#
public class Solution {
    public int NumDecodings(string s) {
        if(s[0]== '0')
            return 0;
        int n = s.Length;
        if(n == 1)
            return 1;
        int[] dp = new int[n+1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i = 2; i <= n;i++){
            int oneDigit = int.Parse(s.Substring(i-1,1));
            if(oneDigit > 0)
                dp[i] += dp[i-1];
            int twoDigit = int.Parse(s.Substring(i-2,2));
            if(10 <= twoDigit && twoDigit <= 26){
                dp[i] += dp[i-2];
            }
        }
        return dp[n];
    }
}
```
### Space Optimized
```C#
public class Solution {
    public int NumDecodings(string s) {
        if(s[0]== '0')
            return 0;
        int n = s.Length;
        if(n == 1)
            return 1;
        int prev2 = 1;
        int prev1 = 1;

        for(int i = 2; i <= n;i++){
            int oneDigit = int.Parse(s.Substring(i-1,1));
            int curr = 0;
            if(oneDigit > 0)
                curr = prev1;
            int twoDigit = int.Parse(s.Substring(i-2,2));
            if(10 <= twoDigit && twoDigit <= 26)
                curr += prev2;
            prev2= prev1;
            prev1 = curr;
        }
        return prev1;
    }
}

