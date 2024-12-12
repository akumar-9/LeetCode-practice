# Container With Most Water

## Problem Statement
You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the ith line are `(i, 0)` and `(i, height[i])`.
Find two lines that together with the x-axis form a container, such that the container contains the most water.
Return the maximum amount of water a container can store.

## Example
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49

## Approach
I use two pointer technique. At each step, find the current Area i.e width x height. Lines may have unequal length, so take the shorter among the two. Update maxArea. If left height is shorter then move the left pointer forward(towards right pointer), else move the right pointer backward(towards left pointer).

### Time Complexity
- **O(n)**: We process each element once as both pointer move towards each other.
### Space Complexity
- **O(1)**: We use extra space for few variables.

## Solution Code
```C#
public class Solution {
    public int MaxArea(int[] height) {
        int l=0,r=height.Length-1;
        int maxArea =0;
        while(l<r){
            int currArea = (r - l)* Math.Min(height[l], height[r]);
            maxArea = Math.Max(maxArea, currArea);
            if(height[l]<height[r]){
                l++;
            }
            else{
                r--;
            }
        }
        return maxArea;
    }
}