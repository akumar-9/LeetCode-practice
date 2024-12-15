# Counting Bits

## Problem Statement
Given an integer `n`, return an array `ans` of length `n + 1` such that for each `i` `(0 <= i <= n)`, `ans[i]` is the number of `1`'s in the binary representation of `i`.
### Example
Input: n = 2 Output: [0,1,1]

## Approach
### Approach#1
Straightforward approach would be to do what we did in the problem Number of 1 Bits for each i; that is i&(i-1) until i == 0;
### Approach#2
We can use the right shift by 1 and check for LSB using &1 approach. If we observe carefully, i >>1 is basically i÷2, for which we have already calculated the 1 bits. Now just check LSB using &1. This is the DP approach.
### Time Complexity
### Approach#1
- **O(nlogn)**: The approach process all 1's in i which is atmost logi.
### Approach#2
- **O(n)**: We process all elements from 0 to n once.
### Space Complexity
### Both Approach
- **O(1)**: We use extra space for few variable in Approach#1 and DP array is the answer array itself for Approach#2.

## Solution Code
### Approach#1
```C#
public class Solution {
    public int[] CountBits(int n) {
        int[] ans = new int[n+1];
        ans[0] = 0;
        for(int i =1;i<=n;i++){
            int count = 0;
            while(i!=0){
                i = i &(i-1);  
                count++;
            }
            ans[i] = count;
        }
        return ans;
    }
}
```
### Approach#2
```C#
public class Solution {
    public int[] CountBits(int n) {
        int[] ans = new int[n+1];
        ans[0] = 0;
        for(int i =1;i<=n;i++){
            ans[i]= ans[i>>1] + (i&1);
        }
        return ans;
    }
}


