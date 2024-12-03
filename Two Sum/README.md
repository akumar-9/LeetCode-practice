# Two Sum Solution

## Problem Statement
Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`. You may assume that each input would have exactly one solution, and you may not use the same element twice.

### Example
Input: nums = [2, 7, 11, 15], target = 9 Output: [0, 1]

## Approach
I used a **hash map** to store the current number as key and its index as value while iterating through the list. For each element, I check if the difference (traget-current[i]) is already in the hash map. If it is, I return the indices.

### Time Complexity
- **O(n)**: We go through the list once, and each lookup in the hash map is O(1).

### Space Complexity
- **O(n)**: We use extra space for the hash map.

## Solution Code
```C#
public class Solution {
    public int[] TwoSum(int[] nums, int target) {
        Dictionary<int,int> seen = new Dictionary<int, int>();
        for(int i =0; i< nums.Length; i++){
            int complement = target - nums[i];
            if(seen.ContainsKey(complement)){
                return new int[] {seen[complement],i};
            }
            else{
                seen.Add(nums[i],i);
            }
        }
        return null;
    }
}