# House Robber

## Problem Statement
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

### Example
Input: nums = [1,2,3,1]
Output: 4

## Approach
I use dynamic programming here. In the dp array, at dp[i] we have 2 choices, skip or include. If skipped, then profit would be amount till i-1 th house. If not skipped, add nums[i] with profit from nums[i-2] house because you cannot use adjacent house.
### Space Optimization
If I visualize it, I only need need to keep track of profit till n-1th house(if we are skipping) and profit till n-2th house(if we are including current house). So you two variables only. profitI1, profitI2.
### Time Complexity
- **O(n)**:We traverse the dp array once. Even in the space optimized approach, we still have to go through n elements.
### Space Complexity
- **O(n)**: We use a dp array of size n.
#### Space Optimized
- **O(1)**: We use extra variables.

## Solution Code
### Approach
```C#
public class Solution {
    public int Rob(int[] nums) {
        int n = nums.Length;
        if(n == 1) 
            return nums[0];
        int[] dp = new int[n];
        dp[0] = nums[0];
        dp[1] = Math.Max(nums[0],nums[1]);
        for(int i = 2; i < n; i++){
            dp[i] = Math.Max(dp[i-1],nums[i]+ dp[i-2]);
        }
        return dp[n-1];
    }
}
```
### Space Optimized
```C#
public class Solution {
    public int Rob(int[] nums) {
        int n = nums.Length;
        if(n == 1) 
            return nums[0];
        int curr;
        int prev2 = nums[0];
        int prev= Math.Max(nums[0],nums[1]);
        for(int i = 2; i < n; i++){
            curr = Math.Max(prev, nums[i] + prev2);
            prev2 = prev;
            prev = curr;
        }
        return prev;
    }
}  }
}

