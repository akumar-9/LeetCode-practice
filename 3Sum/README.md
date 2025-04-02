# 3Sum Solution

## Problem Statement
Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.


### Example
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4

## Approach
Sorting helps. I sort the array to identify duplicates and simplify the process of finding triplets. I then fix one element and find the other two elements using two-pointer technique. One at the start and the other at the end. At each step, check if the sum of these three elements equal to zero. If yes, add the triplet to result list. Otherwise, check adjust the left or right pointer to get closer to the sum.

### Time Complexity
- **O(n^2)**: Sorting take O(nlogn) time and Finding triplets take O(n^2) time. So O(n^2 + nlogn)
### Space Complexity
- **O(1)**: Assuming in-place sorting.

## Solution Code
```C#
public class Solution {
    public IList<IList<int>> ThreeSum(int[] nums) {
        IList<IList<int>> result = new List<IList<int>>();
        Array.Sort(nums);
        for(int i = 0; i< nums.Length; i++){
            if( i > 0 && nums[i] == nums[i-1]) //skip duplicate triplet that start with same num
                continue;   
            int l = i+1;
            int r = nums.Length-1;
            while(l<r){
               int threeSum = nums[i] + nums[l] + nums[r];
                if(threeSum < 0)
                    l++;
                else if(threeSum > 0)
                    r--;
                else{
                    result.Add(new List<int> {nums[i],nums[l], nums[r]});
                    l++;
                    r--;
                    while(nums[l] == nums[l-1] && l < r) // skip duplicates because we don't need a duplicate triplet in result
                        l++;
                    while(nums[r] == nums[r+1] && l < r) //skip duplicates
                        r--;
                }
            }
        }
        return result;
    }
}