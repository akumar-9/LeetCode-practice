# Minimum in Rotated Sorted Array Solution

## Problem Statement
Given the sorted rotated array `nums` of unique elements, return the minimum element of this array. You must write an algorithm that runs in O(log n) time.

### Example
Input: nums = [3,4,5,1,2] Output: 1

## Approach
I use binary search. At any given time, one half of the array is sorted, the other half is not. The minimum will lie in the unsorted half.

### Time Complexity
- **O(lgn)**: We half the search space after every iteration once so O(lgn).
### Space Complexity
- **O(1)**: We use extra space few variables.

## Solution Code
```C#
public class Solution {
    public int FindMin(int[] nums) {
        int low = 0, hi = nums.Length-1, mid;
        while(low < hi){
            mid = (low+hi)/2;
            if(nums[mid] > nums[hi]){ // check if right half is unsorted
                low = mid+1;
            }
            else{
                hi = mid;
            }
            if(low==hi){
                break;
            }
        }
        return nums[low];
    }
}