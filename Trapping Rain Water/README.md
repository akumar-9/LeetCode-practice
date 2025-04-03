# Trapping Rain Water

# Problem Statement
Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

### Example
![Problem visualization](image.png)
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

## Approach 1
For each position, find the maximum height to the left and right, then calculate the water that can be trapped there.

Think of each index as a “bowl”:
	- To trap water, there must be taller bars on both sides
	- Water level is limited by the shorter wall
	- Formula: min(leftMax, rightMax) - height[i]

## Approach 2
Instead of recomputing leftMax and rightMax for each index, precompute them.

	- lMax[i] = tallest bar to the left of index i
	- rMax[i] = tallest bar to the right of index i
	- Then use the same formula per index.

## Approach 3
Eliminate extra space using two pointers and dynamic lMax and rMax.

	- Initialize pointers at both ends.
	- Always move the pointer at the shorter wall inward.
	- Track lMax and rMax on the fly.
	- Water trapped is still min(lMax, rMax) - height[i], but we know which side limits it.

### Time Complexity
#### Approach 1
- **O(n^2)**: For each position, finding its left max and right max takes O(n) time.
#### Approach 2
- **O(n)**: We precompute the max(s) so we make 3 passes.
#### Approach 3
- **O(n)**: We track max(s) on the fly.

### Space Complexity
#### Approach 1
- **O(1)**
#### Approach 2
- **O(n)**: The precomputed max(s) take 2 arrays of size n
#### Approach 3
- **O(1)**

## Solution Code
```C#
// Approach 1
public class Solution {
    public int Trap(int[] height) {     
        int Max(int start, int end){
            int max = -1;
            for(int i = start; i < end; i++){
                if(height[i] > max){
                    max = height[i];
                }
            }
            return max;
        }       

        int result = 0;
        int n = height.Length;
        for(int i = 0; i < n; i++){
            int lMax = Max(0,i);
            int rMax = Max(i, n);
            int currLevel = Math.Min(lMax,rMax) - height[i];
            if(currLevel > 0){
                result+= currLevel;
            }
        }
        return result;
    }
}



// Approach 2
public class Solution {
    public int Trap(int[] height) {
        int n = height.Length;
        if(n < 2)   return 0;
        int result = 0;

        int[] lMax = new int[n];
        int[] rMax = new int[n];

        for(int i = 1; i < n; i++){
            lMax[i] = Math.Max(height[i-1], lMax[i-1]);
        }
        for(int i = n-2; i >= 0; i--){           
            rMax[i] = Math.Max(height[i+1], rMax[i+1]);
        }

        for(int i = 0; i < n; i++){
            int currLevel = Math.Min(lMax[i],rMax[i]) - height[i];
            if(currLevel > 0){
                result+= currLevel;
            }
        }
        return result;
    }
}



// Approach 3
public class Solution {
    public int Trap(int[] height) {
        int l = 0, r = height.Length - 1;
        int lMax = height[l], rMax = height[r];
        int result = 0;

        while (l < r) {
            if (lMax < rMax) {
                l++;
                lMax = Math.Max(lMax, height[l]);
                result += lMax - height[l];
            } else {
                r--;
                rMax = Math.Max(rMax, height[r]);
                result += rMax - height[r];
            }
        }

        return result;
    }
}