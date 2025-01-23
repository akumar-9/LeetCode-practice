# Meeting Rooms (LintCode)

## Problem Statement
Given an array of meeting time `intervals` consisting of start and end times `[(s1,e1),(s2,e2),...] (si < ei)`, determine if a person could attend all meetings.

### Example
Input: intervals = [(0,30),(5,10),(15,20)]Output: false

## Approach
Use the same approach as over-lapping intervals, if the b_start < a_end, then there is conflict(overlap). Return false immediately. 

### Time Complexity
- **O(n)**: We go through the list once so O(n).
### Space Complexity
- **O(1)**: We use extra space few variables.

## Solution Code
```C#
/**
 * Definition of Interval:
 * public class Interval {
 *     public int start, end;
 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 * }
 */

using System;
using System.Collections;
using System.Collections.Generic;

namespace lintcode
{
    class Solution {
        /**
         * @param intervals: an array of meeting time intervals
         * @return: if a person could attend all meetings
         */
        public bool CanAttendMeetings(List<Interval> intervals) {
            Array.Sort(intervals, (a,b) => a.start.CompareTo(b.start));
            int n = intervals.Length;
            for(int i = 1; i < n; i++){
                if(intervals[i].start < intervals[i-1].end){
                    return false;
                }
            }
            return true;
        }
    }
}