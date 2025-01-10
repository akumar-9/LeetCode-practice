# Insert Interval

## Problem Statement
You are given an array of non-overlapping intervals `intervals` where` intervals[i] = [starti, endi]` represent the start and the end of the `ith` interval and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval` `= [start, end]` that represents the start and end of another interval.

Insert `newInterval` into intervals such that intervals is still sorted in ascending order by `starti` and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` after the insertion.

Note that you don't need to modify `intervals` in-place. You can make a new array and return it.

### Example
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]

## Approach
We don't have to worry about intervals that don't overlap. You can check this by comparing if a_end < b_start (i.e. interval `a` ends before `b` starts). Insert all elements that appears before newInterval and does not overlap. If a_end < b_start is false, then that means `a` ends after `b`starts which means there is an overlap. If an overlap is found, we keep merging the intervals, until there is no overlap. As soon as the a_start > b_ends, the current interval starts after the merged interval ends, meaning no further overlap is possible.

### Time Complexity
- **O(n)**: We traverse the array once.

### Space Complexity
- **O(n)**: We use an extra array of size n.

## Solution Code
```C#
public class Solution {
    public int[][] Insert(int[][] intervals, int[] newInterval) {
        List<int[]> results = new List<int[]>();
        int i = 0;
        int n = intervals.Length;

        while(i<n && intervals[i][1] < newInterval[0]){         // intervals that do not overlap and appear before the newInterval
            results.Add(intervals[i]);
            i++;
        }

        while( i < n && intervals[i][0] <= newInterval[1]){     // Merging takes place here, newInterval is re-calculated until not overlap is found
            newInterval[0] = Math.Min(newInterval[0], intervals[i][0]);
            newInterval[1] = Math.Max(newInterval[1], intervals[i][1]);
            i++;
        }
        results.Add(newInterval);                               // Add the modified, merged, non-overlapping interval to the list

        while(i < n){                                           // Add remaining ones as do not overlap 
            results.Add(intervals[i]);
            i++;
        }
        return results.ToArray();
    }
}