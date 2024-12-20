# Longest Increasing Subsequence

## Problem Statement
Given an integer array `nums`, return the length of the longest strictly increasing subsequence.


### Example
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4

## Approach
### 1
I use dynamic programming here. LIS at a given position will be the max of dp[i] or 1 + dp[j] where arr[j] < arra[i]. We check that if there is any number before the current which is less than it. This ensures we are in an increasing order which is a requirement. If yes then we add the current also this increasing subsequence. At each step, track the maxLIS seen so far and update.

### 2
I use Binary Search here. We will will maintain an array `LIS[]` and we will traverese the elements in `nums` and insert/replace them in `LIS[]`. For each element in `nums` we will determine its position in `LIS[]` using binary search. If the element can extend the subsequence then we append it else we replace an element in `LIS[]` with this `num` ensuring sorted order is maintained. It helps to watch TechDose's video on this.
### Time Complexity
#### Approach#1 
- **O(n^2)**:The inner for loop runs 0 to n. This is done for every element in the array
#### Approach#2
- **O(nlogn)**:For each element in nums, we do a binary search in LIS[]
### Space Complexity
#### Approach#1
- **O(n)**: We use 1 extra dp array.
#### Approach#2
- **O(n)**: We use 1 LIS array.

## Solution Code
### Approach#1
```C#
public class Solution {
    public int LengthOfLIS(int[] nums) {
        int maxLIS = 1;
        int[] dp = new int[nums.Length];
        Array.Fill(dp, 1);
        for(int i = 1; i < nums.Length; i++) {
            for(int j = 0; j < i; j++ ){
                if( nums[j] < nums[i]){
                    dp[i]= Math.Max(dp[i], 1+dp[j]);
                }
            }
            maxLIS = Math.Max(dp[i], maxLIS);
        }
        return maxLIS;
    }
}
```
### Approach#2 (Optimal)
```C#
public class Solution {
    public int LengthOfLIS(int[] nums) {
        List<int> LIS = new List<int>();
        for(int i = 0; i < nums.Length; i++) {
            int pos = BinarySearch(LIS,nums[i]);
            if(pos == LIS.Count){
                LIS.Add(nums[i]);
            }
            else
                LIS[pos] = nums[i];
        }
        return LIS.Count;
    }

    public int BinarySearch(List<int> arr, int target){
        if(arr.Count == 0)
            return 0;
        int lo = 0, hi = arr.Count - 1;
        while(lo <= hi){
            int  mid = lo + (hi-lo)/2;
            if(arr[mid] < target){
                lo = mid+1;
            }
            else{
                hi = mid-1;
            }
        }
        return lo;
    }
}

