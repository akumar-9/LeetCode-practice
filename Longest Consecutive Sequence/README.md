# Longest Consecutive Sequence

## Problem Statement
Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.
You must write an algorithm that runs in `O(n)` time.

### Example
Input: nums = [100,4,200,1,3,2]
Output: 4

## Approach
I use hashset here. Trading space for speed. For each element in the hashset, check if the current number is the beginning of a sequence(check if num-1 is present or not). If this is the start of a new sequence then check if num+1, num+2 ... exists and keep track of the length of the current streak. 

### Time Complexity
- **O(n)**: Every element in hashset is traversed.
### Space Complexity
- **O(n)**: Extra space for hashset.

## Solution Code
```C#
public class Solution {
    public int LongestConsecutive(int[] nums) {
        HashSet<int> numSet = new HashSet<int>(nums);
        int maxStreak = 0;

        foreach(int num in numSet){
            if(!numSet.Contains(num-1)){
                int streak = 0;
                while(numSet.Contains(num + streak)){
                    streak++;
                }
                maxStreak = Math.Max(streak, maxStreak);
            }
        }
        return maxStreak;
    }
}