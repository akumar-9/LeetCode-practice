# Jump Game

## Problem Statement
You are given an integer array `nums`. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.

Return `true` if you can reach the last index, or `false` otherwise.
### Example
Input: nums = [2,3,1,1,4]
Output: true

## Approach
I use greedy approach here. At each step I check the farthest reachable index. If the current index `i` does not fall in this range, then return false because it is unreachable. If the farthest reachable index is greater than last index, return true. Farthest reachable index is obtained by check the current farthest index and current index + max jump length.

### Time Complexity
- **O(n)**: Worst case we go through the list once.

### Space Complexity
- **O(1)**: We use only extra variables.

## Solution Code
```C#
public class Solution {
    public bool CanJump(int[] nums) {
        int farthestReachableIndex = 0;
        for(int i = 0 ; i< nums.Length; i++){
            if(farthestReachableIndex < i){
                return false;
            }
            farthestReachableIndex = Math.Max(farthestReachableIndex, i + nums[i]);
            if(farthestReachableIndex >= nums.Length-1 )
                return true;
        }
        return true;
    }
}