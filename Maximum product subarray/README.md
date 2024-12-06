# Maximum Product Subarray Solution

## Problem Statement
Given an integer array `nums`, find a subarray that has the largest product, and return the product.

### Example
Input: nums = [2,3,-2,4] Output: 6

## Approach
Iterate through the array and find both maximum product and the minimum product at each step. Why track min product? A negative min product could be the maximum product if multiplied by another negative.

### Time Complexity
- **O(n)**: We go through the list once so O(n).
### Space Complexity
- **O(1)**: We use extra space few variables.

## Solution Code
```C#
public class Solution{
    public int MaxProduct(int[] nums){
        int answer = nums[0], min= nums[0], max = nums[0], tmp = 0;
        for(int i = 1; i< nums.Length; i++){
            if(nums[i] < 0){
                tmp = min;
                min = max;
                max = tmp;
            }
            min = Math.Min(nums[i], min*nums[i]);
            max = Math.Max(nums[i], max*nums[i]);
            answer = Math.Max(max, answer);
        }
        return answer;
    }
}