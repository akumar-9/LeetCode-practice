# Sum of Two Integers

## Problem Statement
Given two integers `a` and `b`, return the sum of the two integers without using the operators `+` and `-`.


### Example
Input: a = 1, b = 2
Output: 3

## Approach
I use bitwise operation XOR. The XOR operation does addition without carry bit. So account for that. To know which bits generate carry, use AND operator, and since carry will to left of this bit, left shift by 1 position. Do this until the carry becomes zero.

### Time Complexity
- **O(1)**: Bitwise operations take constant time.
### Space Complexity
- **O(1)**: We use extra space few variables.

## Solution Code
```C#
public class Solution {
    public int GetSum(int a, int b) {
        int sumWithoutCarry = a, carry = b;
        while(carry!=0){
            sumWithoutCarry = a ^ b;
            carry = a & b;
            a = sumWithoutCarry;
            b = carry << 1;
        }
        return a;
    }
}