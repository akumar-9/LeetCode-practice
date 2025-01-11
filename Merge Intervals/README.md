# Merge Intervals

## Problem Statement
Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the `intervals` in the input.

Insert `newInterval` into intervals such that intervals is still sorted in ascending order by `starti` and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` after the insertion.

Note that you don't need to modify `intervals` in-place. You can make a new array and return it.

### Example
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]

## Approach
Sort the intervals using start as the key. This keeps it clean. Two intervals [a_start, e_end] and [b_start, b_end] overlaps if b_start <= a_end. Then the merged interval will [a_start, max(a_end, b_end)]. If two intervals doesn't overlap, then add the current interval to the results.

### Time Complexity
- **O(n)**: We traverse the array once.

### Space Complexity
- **O(n)**: We use an extra array of size n.

## Solution Code
```C#
public class Solution {
    public int[][] Merge(int[][] intervals) {
        List<int[]> results = new List<int[]>();
        int n = intervals.Length;
        Array.Sort(intervals, (a,b) => a[0].CompareTo(b[0]));    // sort with start as key
        int[] current = intervals[0];                           // initial after sorting only
        int i = 1;
        while(i < n){
             if (current[1] < intervals[i][0]) {               // Non-overlapping
                results.Add(current);
                current = intervals[i];
            }
            else {
                current[1] = Math.Max(current[1], intervals[i][1]);     // merge intervals and choose the largest
            }
            i++;
        }
        results.Add(current);   // this line adds the final merged interval if all are overlapping OR the last element if it does not overlap with current

        return results.ToArray();

    }
}