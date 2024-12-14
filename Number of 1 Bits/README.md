# Number of 1 Bits

## Problem Statement
Given a positive integer `n`, write a function that returns the number of set bits in its binary representation (also known as the Hamming weight).

### Example
Input: n = 11 Output: 3

## Approach
### Approach#1
I count the number of times 1 comes in the Least Significant Bit position. I can do this by ANDing `n` with `1`. Then discard the LSB by shifting right by 1 position. I can process every bit by doing this. 
### Approach#2
If I subtract 1 from n, it flips all bits to the left of lowest set bit, including itself. Performing `n&(n-1)` will clear the lowest set bit.
### Time Complexity
### Approach#1
- **O(n)**: We iterate through every bit.
### Approach#2
- **O(k)**: We skip through the zeros, so only depends on the number of 1's in the bit, say `k`.
### Space Complexity
### Both Approach
- **O(1)**: We use extra space only 1 variables.

## Solution Code
### Approach#1
```C#
public class Solution {
    public int HammingWeight(int n) {
        int count = 0;
        while(n!=0){
            count = count + (n & 1);        //check LSB
            n = n >> 1;                    // process next bit
        }
        return count ;
    }
}
```

### Approach#2
```C#
public class Solution {
    public int HammingWeight(int n) {
        int count = 0;
        while(n!=0){
            n = n&(n-1);  // n-1 filps all bits left of lowest set bit.(Basically it is counter). 
            count++; //AND with n will discard this lowest set bit. Now you have a overlapping subproblem.
        }
        return count;
    }
}