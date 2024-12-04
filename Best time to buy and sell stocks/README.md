# Best Time to Buy and Sell Stock Solution

## Problem Statement
You are given an array `prices` where `prices[i]` is the price of a given stock on the ith day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock. Return the maximum profit you can achieve from this transaction.

### Example
Input: prices = [7, 1, 5, 3, 6, 4] Output: 5 (Buy at 1, Sell at 6)

## Approach
We use a greedy approach:
- Track the minimum price encountered so far.
- Calculate the potential profit by selling on the current day.
- Update the maximum profit if the current potential profit is higher.

### Time Complexity
- **O(n)**: We traverse the list once.

### Space Complexity
- **O(1)**: We only use a few extra variables.

## Solution Code
```C#
public class Solution {
    public int MaxProfit(int[] prices) {
        int minSoFar = prices[0];
        int profit = 0;
        int maxProfit = 0;
        for(int i = 1; i < prices.Length; i++){
            profit = prices[i]-minSoFar;
            maxProfit = Math.Max(profit,maxProfit);
            minSoFar = Math.Min(minSoFar,prices[i]);
        }
        return maxProfit;
    }
}