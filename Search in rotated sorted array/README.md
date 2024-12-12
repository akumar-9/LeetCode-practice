# Search in Rotated Sorted Array Solution

## Problem Statement
Given the array `nums` after the possible rotation and an integer `target`, return the index of `target` if it is in `nums`, or -1 if it is not in `nums`.

You must write an algorithm with O(log n) runtime complexity.

### Example
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4

## Approach
I use binary search. At any given time, one half of the array is sorted, the other half is not. Find out the sorted half first. Check if target falls in this range. If yes, continue search on this half. Otherwise, continue search on the other half. This half will become the new sub-problem. 

### Time Complexity
- **O(lgn)**: We half the search space after every iteration once so O(lgn).
### Space Complexity
- **O(1)**: We use extra space few variables.

## Solution Code
```C#
public class Solution {
    public int Search(int[] nums, int target) {
        int l = 0, r=nums.Length-1;
        while(l<=r){
            int mid = l + (r-l)/2;
            if(target == nums[mid]){
                return mid;
            }
            if(nums[l] <= nums[mid]){
                if (nums[l] <= target && target <= nums[mid]){
                    r = mid - 1;
                }
                else{
                    l = mid + 1;
                }
            }
            else{
                if( nums[mid] <= target && target <= nums[r]){
                    l = mid + 1;
                }
                else {
                    r = mid - 1;
                }
            }
        }
        return -1;
    }
}