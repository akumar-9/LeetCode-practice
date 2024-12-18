# Climbing Stairs

## Problem Statement
You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

### Example
Input: n = 2
Output: 2

## Approach
### 1
I use dynamic programming here. You can reach the current step either by taking 2 steps from (n-2)th step or 1 step from (n-1)th step. Now we have two subproblems. Apply the same logic. The base case will be n=1 return 1 or n=2 return 2.

### 2
We also solve this using two variables:
This follows the same pattern as fibonacci series. Calculate the previous two values iteratively.
### Time Complexity
#### Approach#1 
- **O(n)**: We iterate once from 1 through n.
#### Approach#2
- **O(n)**: We iterate once from 1 through n.
### Space Complexity
#### Approach#1
- **O(n)**: We use 1 extra dp array.
#### Approach#2
- **O(1)**: We only use a few extra variables.

## Solution Code
### Approach#1
```C#
public class Solution {
    public int ClimbStairs(int n) {
        if( n==1 || n ==2){
            return n;
        }
        int[] dp = new int[n+1];
        dp[1] = 1;
        dp[2] = 2;
        for(int i =3; i<=n;i++){
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
}
```
### Approach#2 (Optimal)
```C#
public class Solution {
   public int ClimbStairs(int n) {
        if(n==1 | n==2)
          return n;
        int prev1 = 1; 
        int prev2 = 2;
        int curr = 0;
        for(int i = 3; i<=n; i++ ){
            curr = prev1 + prev2;
            prev1 = prev2;
            prev2 = curr;
        }
        return curr;
    }
}

