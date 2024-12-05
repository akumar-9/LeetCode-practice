# Product of Array Except Self Solution

## Problem Statement
Given an array `nums` of length `n`, return an array `output` such that `output[i]` is equal to the product of all the elements of `nums` except `nums[i]`. You must solve it without using division and in O(n) time complexity.

### Example
Input: nums = [1, 2, 3, 4] Output: [24, 12, 8, 6]

## Approach
### 1
We solve this in two passes:
1. In the first pass, calculate the product of all elements to the left of each index and store it in the `prefix` array.
2. In the second pass, calculate the product of all elements to the right of each index and update the `suffix` array.

### 2
We also solve this in two passes:
We will compute the prefix and suffix products in-place, without using extra space for separate `prefix` and `suffix` arrays. The idea is to use the output array for both prefix and suffix products.
### Time Complexity
#### Approach#1 and Approach#2
- **O(n)**: We iterate through the array twice.

### Space Complexity
#### Approach#1
- **O(n)**: We use 2 extra arrays, not counting the output array.
#### Approach#2
- **O(1)**: We only use a few extra variables, not counting the output array.

## Solution Code
### Approach#1
```C#
public class Solution {
    public int[] ProductExceptSelf(int[] nums) {
        int[] prefix = new int[nums.Length];
        int[] suffix = new int[nums.Length];
        int[] answer = new int[nums.Length];
        prefix[0] = 1;
        suffix[nums.Length-1] = 1;
        for(int i = 1; i< nums.Length; i++){
            prefix[i] = nums[i-1]*prefix[i-1];
        }
        for(int i = nums.Length - 2; i>= 0 ; i--){
            suffix[i] = nums[i+1]*suffix[i+1];
        }
        for(int i = 0; i< nums.Length; i++){
            answer[i] = suffix[i]*prefix[i];
        }
        return answer;
    }
}

### Approach#2 (Optimal)
```C#
public class Solution {
    public int[] ProductExceptSelf(int[] nums) {
        int[] prefix = new int[nums.Length];
        int suffix = 1;
        prefix[0] = 1;

        for(int i = 1; i< nums.Length; i++){
            prefix[i] = nums[i-1]*prefix[i-1];
        }

        for(int i = nums.Length - 2; i>= 0 ; i--){
            suffix = nums[i+1]*suffix;
            prefix[i] *= suffix;
        }
        
        return prefix;
    }
}
