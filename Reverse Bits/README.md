# Reverse Bits

## Problem Statement
Reverse bits of a given 32 bits unsigned integer.

### Example
Input: n = 00000010100101000001111010011100
Output:    964176192 (00111001011110000010100101000000)

## Approach
I use the bitwise operators `&`,`|`, `<<` and `>>`. I AND the number with 1 to get the LSB. I left shift the result by 1 position and OR this LSB to the result. Then move to the next bit in the original number by shifting right. (Basically, pop the last bit, push this last bit to result).   
### Time Complexity
- **O(1)**: The algorithm runs for 32 iterations only.
### Space Complexity
- **O(1)**: We use extra space few variables.

## Solution Code
```C#
public class Solution {
    public uint reverseBits(uint n) {
        uint ans = 0;
        uint lsb = 0;
        for(int i=0;i<32;i++){
            lsb = n & 1;  //get LSB
            ans = ans << 1; // Make space for this LSB
            ans = ans | lsb; // Push the LSB
            n = n >> 1;  // Move to the next bit          
        }
        return ans;
    }
}