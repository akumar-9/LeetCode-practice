# Coin Change

## Problem Statement
You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return`-1`.

You may assume that you have an infinite number of each kind of coin.


### Example
Input: coins = [1,2,5], amount = 11
Output: 3

## Approach
I use dynamic programming approach here. An element in the dp array, represents the minimum number of coins need to make `amount`. The recurrence relation is dp[i] = min(dp[i], dp[i-coin]+1). Declare dp array of size 1 greater than amount. Initialize with big value MAX_INT(or use amount + 1, beacuse we know 1 is the smallest coin and you can make a maximum of `amount` number of coins using 1). Don't forget dp[0] is 0. When returning check if the dp[amount] is not greater than `amount`, if so you know you cant make up the amount so return -1.

### Time Complexity
- **O(k*n)**: The outerloop runs for k coins, innerloop runs for n which is the amount
### Space Complexity
- **O(n)**: DP array is used for size n+1.

## Solution Code
```C#
public class Solution {
    public int CoinChange(int[] coins, int amount) {
        int[] dp = new int[amount+1];
        Array.Fill(dp,amount+1);
        dp[0] = 0;
        foreach(int coin in coins){
            for(int i = coin; i<= amount; i++){
                dp[i] = Math.Min(dp[i],dp[i-coin]+1);
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
    }
}