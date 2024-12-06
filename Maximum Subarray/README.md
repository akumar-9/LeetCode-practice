# Two Sum Solution

## Problem Statement
Given an integer array `nums`, find the subarray with the largest sum, and return its sum.



### Example
Input: nums = [-2,1,-3,4,-1,2,1,-5,4] Output: 6

## Approach
I used  **Kadane’s Algorithm** to solve the problem in O(n) time. The idea is to iterate through array while keeping track of max sum ending at current index and global max sum encountered so far.

### Time Complexity
- **O(n)**: We go through the list once so O(n).
### Space Complexity
- **O(1)**: We use extra space few variables.

## Solution Code
```C#
public class Solution {
    public int MaxSubArray(int[] nums) {
        int maxSum = nums[0];
        int curSum = 0;
        foreach(int n in nums){
            curSum = Math.Max(n, curSum+n);
            maxSum = Math.Max(maxSum, curSum);
        }
    return maxSum;
    }
}