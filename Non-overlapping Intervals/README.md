# Non-overlapping Intervals

## Problem Statement
Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

Note that intervals which only touch at a point are non-overlapping. For example, [1, 2] and [2, 3] are non-overlapping.

### Example
Input: intervals = [[1,2],[2,3],[3,4],[1,3]]
Output: 1

## Approach
Sort the intervals using start as the key. This keeps it clean. Two intervals [a_start, e_end] and [b_start, b_end] overlaps if b_start < a_end. Now take the decision of removing the larger interval and retaining the smaller interval.  
### Time Complexity
- **O(n)**: We traverse the array once.

### Space Complexity
- **O(1)**: We use few extra variables.

## Solution Code
```C#
public class Solution {
    public int EraseOverlapIntervals(int[][] intervals) {
        int removeCount = 0;
        int n = intervals.Length;
        if(n==1) return removeCount;
        Array.Sort(intervals, (a,b) => a[0].CompareTo(b[0]));
        int i = 1;
        int prevEnd = intervals[0][1];
        while(i < n){
            if(prevEnd > intervals[i][0]){
                removeCount++;
                prevEnd = Math.Min(prevEnd, intervals[i][1]);
            }
            else{
                prevEnd = intervals[i][1];
            }
            i++;
        }
        return removeCount;
    }
}